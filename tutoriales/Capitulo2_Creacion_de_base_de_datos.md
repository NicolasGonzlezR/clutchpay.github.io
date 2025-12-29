# Capítulo 2: Creación de Base de Datos con Docker y Prisma

En este capítulo se configura la base de datos PostgreSQL utilizando Docker y cómo Prisma ORM para gestionar tu la base de datos de forma eficiente.

---

## 1. Arquitectura del Sistema

ClutchPay utiliza una arquitectura moderna con las siguientes tecnologías:

- **PostgreSQL**: Base de datos relacional para almacenar usuarios, facturas y pagos
- **Docker**: Para contenedorizar PostgreSQL y facilitar el desarrollo
- **Prisma ORM**: Para gestionar el esquema de base de datos y las migraciones
- **Next.js**: Framework full-stack para la aplicación web

---

## 2. Configuración de PostgreSQL con Docker

### El archivo docker-compose.yml

El archivo `docker/docker-compose.yml` define la configuración del contenedor de PostgreSQL:

```yaml
services:
  postgres:
    image: postgres:15
    restart: always
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - "5432:5432"
    volumes:
      - postgres-data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $${POSTGRES_USER} -d $${POSTGRES_DB}"]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  postgres-data:
```

### Explicación de la configuración:

- **image: postgres:15**: Utiliza la imagen oficial de PostgreSQL versión 15
- **restart: always**: El contenedor se reiniciará automáticamente si se detiene
- **environment**: Variables de entorno que configuran:
  - `POSTGRES_USER`: Usuario de la base de datos
  - `POSTGRES_PASSWORD`: Contraseña del usuario
  - `POSTGRES_DB`: Nombre de la base de datos
- **ports**: Mapea el puerto 5432 del contenedor al puerto 5432 del host
- **volumes**: Persiste los datos en un volumen llamado `postgres-data`
- **healthcheck**: Verifica que PostgreSQL esté listo para aceptar conexiones

### Iniciar la base de datos:

```bash
cd docker
docker-compose up -d
```

El flag `-d` ejecuta el contenedor en segundo plano (detached mode).

### Verificar que el contenedor está corriendo:

```bash
docker ps
```

### Detener la base de datos:

```bash
docker-compose down
```

---

## 3. Modelo de Datos de ClutchPay

### Descripción general del modelo

ClutchPay es una aplicación de gestión de facturas y pagos que incluye:

- **Usuarios**: Personas que emiten y reciben facturas
- **Facturas**: Documentos que representan deudas entre usuarios
- **Pagos**: Transacciones que liquidan las facturas
- **Notificaciones**: Alertas sobre eventos importantes
- **Contactos**: Relaciones entre usuarios para facilitar transacciones

### El archivo prisma/schema.prisma

Este archivo define el esquema completo de la base de datos utilizando Prisma ORM:

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

- **generator client**: Configura el cliente de Prisma para JavaScript/TypeScript
- **datasource db**: Define PostgreSQL como base de datos y usa la variable de entorno `DATABASE_URL`

---

## 4. Modelos de la Base de Datos

### Modelo User (Usuario)

```prisma
model User {
  id                  Int       @id @default(autoincrement())
  email               String    @unique
  password            String    @db.VarChar(255)
  name                String
  surnames            String
  phone               String?   @db.VarChar(20)
  country             String?
  imageUrl            String?
  emailNotifications  Boolean   @default(true)
  createdAt           DateTime  @default(now())
  updatedAt           DateTime  @updatedAt

  issuedInvoices    Invoice[] @relation("IssuerUser")
  owedInvoices      Invoice[] @relation("DebtorUser")

  contacts     User[] @relation("UserContacts")
  contactOf    User[] @relation("UserContacts")

  notifications  Notification[]

  @@map("users")
}
```

**Características principales:**
- `id`: Identificador único autoincrementable
- `email`: Correo electrónico único para autenticación
- `password`: Contraseña hasheada (máximo 255 caracteres)
- `emailNotifications`: Preferencia de notificaciones por email (activada por defecto)
- **Relaciones**:
  - `issuedInvoices`: Facturas que el usuario ha emitido
  - `owedInvoices`: Facturas que el usuario debe pagar
  - `contacts` y `contactOf`: Relación auto-referencial para la lista de contactos
  - `notifications`: Notificaciones del usuario

### Modelo Invoice (Factura)

```prisma
model Invoice {
  id                Int       @id @default(autoincrement())
  invoiceNumber     String    @unique
  issuerUserId      Int
  debtorUserId      Int
  subject           String    @db.Text
  description       String    @db.Text
  amount            Decimal   @db.Decimal(10, 2)
  status            InvoiceStatus @default(PENDING)
  issueDate         DateTime  
  dueDate           DateTime?
  invoicePdfUrl     String
  createdAt         DateTime  @default(now())
  updatedAt         DateTime  @updatedAt

  issuerUser        User      @relation("IssuerUser", fields: [issuerUserId], references: [id])
  debtorUser        User      @relation("DebtorUser", fields: [debtorUserId], references: [id])

  payment          Payment?
  notifications  Notification[]

  @@index([issuerUserId])
  @@index([debtorUserId])
  @@map("invoices")
}
```

**Características principales:**
- `invoiceNumber`: Número de factura único
- `amount`: Monto con precisión decimal (10 dígitos, 2 decimales)
- `status`: Estado de la factura (PENDING, PAID, OVERDUE, CANCELED)
- `invoicePdfUrl`: URL del PDF de la factura
- **Relaciones**:
  - `issuerUser`: Usuario que emite la factura
  - `debtorUser`: Usuario que debe pagar la factura
  - `payment`: Pago asociado (relación uno a uno opcional)
- **Índices**: En `issuerUserId` y `debtorUserId` para mejorar el rendimiento de las consultas

### Modelo Payment (Pago)

```prisma
model Payment {
  id                Int       @id @default(autoincrement())
  invoiceId         Int       @unique
  paymentDate       DateTime
  paymentMethod     PaymentMethod
  paymentReference  String?
  receiptPdfUrl     String
  subject           String?   @db.Text
  createdAt         DateTime  @default(now())
  updatedAt         DateTime  @updatedAt

  invoice           Invoice   @relation(fields: [invoiceId], references: [id], onDelete: Restrict)

  @@index([invoiceId])
  @@map("payments")
}
```

**Características principales:**
- `invoiceId`: Relación única con una factura (un pago por factura)
- `paymentMethod`: Método de pago (PAYPAL, VISA, MASTERCARD, OTHER)
- `receiptPdfUrl`: URL del comprobante de pago
- `onDelete: Restrict`: Previene la eliminación de facturas que tienen pagos asociados

### Modelo Notification (Notificación)

```prisma
model Notification {
  id        Int      @id @default(autoincrement())
  userId    Int
  invoiceId Int
  type      NotificationType
  read      Boolean  @default(false)
  createdAt DateTime @default(now())

  user      User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  invoice   Invoice  @relation(fields: [invoiceId], references: [id], onDelete: Restrict)
}
```

**Características principales:**
- `type`: Tipo de notificación (INVOICE_ISSUED, PAYMENT_DUE, PAYMENT_OVERDUE, PAYMENT_RECEIVED, INVOICE_CANCELED)
- `read`: Estado de lectura de la notificación
- `onDelete: Cascade`: Las notificaciones se eliminan cuando se elimina el usuario

---

## 5. Enumeraciones (Enums)

### InvoiceStatus

```prisma
enum InvoiceStatus {
  PENDING    // Factura pendiente de pago
  PAID       // Factura pagada
  OVERDUE    // Factura vencida
  CANCELED   // Factura cancelada
}
```

### PaymentMethod

```prisma
enum PaymentMethod {
  PAYPAL
  VISA
  MASTERCARD
  OTHER
}
```

### NotificationType

```prisma
enum NotificationType {
  INVOICE_ISSUED      // Notificación cuando se emite una factura
  PAYMENT_DUE         // Recordatorio de pago próximo a vencer
  PAYMENT_OVERDUE     // Notificación de pago vencido
  PAYMENT_RECEIVED    // Confirmación de pago recibido
  INVOICE_CANCELED    // Notificación de factura cancelada
}
```

---

## 6. Variables de Entorno

Antes de ejecutar las migraciones, asegúrate de configurar tus variables de entorno. Crea un archivo `.env` en la raíz del proyecto:

```env
# PostgreSQL Configuration
POSTGRES_USER=clutchpay_user
POSTGRES_PASSWORD=tu_password_seguro
POSTGRES_DB=clutchpay_db

# Prisma Database URL
DATABASE_URL="postgresql://clutchpay_user:tu_password_seguro@localhost:5432/clutchpay_db?schema=public"
```

**Nota importante**: La `DATABASE_URL` debe seguir el formato:
```
postgresql://[usuario]:[contraseña]@[host]:[puerto]/[nombre_db]?schema=public
```

---

## 7. Ejecutar Migraciones con Prisma

### Crear y aplicar la migración inicial

Una vez que tengas el contenedor de PostgreSQL corriendo y las variables de entorno configuradas, ejecuta:

```bash
npx prisma migrate dev --name init
```

Este comando realiza las siguientes acciones:

1. **Crea la migración**: Genera archivos SQL en `prisma/migrations/` basados en tu esquema
2. **Aplica la migración**: Ejecuta el SQL contra tu base de datos
3. **Genera el cliente Prisma**: Crea/actualiza el cliente de Prisma para usar en tu código
4. **Registra la migración**: Guarda un registro en la tabla `_prisma_migrations`

**Salida esperada:**
```
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
Datasource "db": PostgreSQL database "clutchpay_db"

Applying migration `20251113114156_init`

The following migration(s) have been created and applied from new schema changes:

migrations/
  └─ 20251113114156_init/
    └─ migration.sql

Your database is now in sync with your schema.

✔ Generated Prisma Client (v5.x.x) to ./node_modules/@prisma/client
```

### Verificar las migraciones

Puedes ver el estado de tus migraciones con:

```bash
npx prisma migrate status
```

---

## 8. Explorar la Base de Datos con Prisma Studio

Prisma Studio es una interfaz gráfica que te permite visualizar y editar los datos de tu base de datos de forma visual.

### Iniciar Prisma Studio

```bash
npx prisma studio
```

Esto abrirá automáticamente tu navegador en `http://localhost:5555` donde podrás:

- **Ver todas las tablas**: Users, Invoices, Payments, Notifications
- **Explorar registros**: Navegar por los datos existentes
- **Crear registros**: Añadir nuevos usuarios, facturas, etc.
- **Editar registros**: Modificar datos existentes
- **Eliminar registros**: Borrar datos (respetando las restricciones de la base de datos)

### Características de Prisma Studio:

- **Interfaz intuitiva**: Navega por tus datos de forma visual
- **Filtros y búsqueda**: Encuentra registros rápidamente
- **Relaciones**: Visualiza y navega por las relaciones entre tablas
- **Sin SQL**: Modifica datos sin escribir consultas SQL

---

## 9. Comandos Útiles de Prisma

### Generar el cliente Prisma

```bash
npx prisma generate
```

### Resetear la base de datos (¡Cuidado! Elimina todos los datos)

```bash
npx prisma migrate reset
```

### Ver el esquema en formato visual

```bash
npx prisma studio
```

### Crear una nueva migración

```bash
npx prisma migrate dev --name nombre_descriptivo
```

### Aplicar migraciones en producción

```bash
npx prisma migrate deploy
```

### Formatear el archivo schema.prisma

```bash
npx prisma format
```

---

## 10. Resumen del Flujo de Trabajo

1. **Iniciar la base de datos**:
   ```bash
   cd docker
   docker-compose up -d
   ```

2. **Configurar variables de entorno**:
   - Crear archivo `.env` con `DATABASE_URL`

3. **Ejecutar migraciones**:
   ```bash
   npx prisma migrate dev --name init
   ```

4. **Explorar la base de datos**:
   ```bash
   npx prisma studio
   ```

5. **Desarrollar tu aplicación**:
   - Usa el cliente Prisma generado en `node_modules/@prisma/client`
---