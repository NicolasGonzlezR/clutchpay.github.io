# Implementación de Gestión de Facturas

En este tutorial se describe el proceso para implementar la funcionalidad completa de gestión de facturas (invoices) en el proyecto, incluyendo creación, actualización, eliminación y almacenamiento de PDFs en Cloudinary.

## 1. Estructura de archivos de pruebas y configuración

- **prisma/schema.prisma**: schema actualizado con modelo `Invoice`

- **src/libs/validations/invoice.ts**: archivo que define los schemas de validación para facturas usando Zod.

- **src/app/api/invoices/route.ts**: endpoint para listar y crear facturas.

- **src/app/api/invoices/[id]/route.ts**: endpoint para obtener, actualizar y eliminar facturas específicas.

## 2. `prisma/schema.prisma`

Este archivo contiene el modelo `Invoice` que permite gestionar facturas y sus pagos asociados. Las relaciones establecidas permiten vincular facturas con usuarios (emisor y deudor) y rastrear pagos.

### Modelos

- **Invoice**: Representa una factura con campos como número de factura, usuarios relacionados, monto, estado, fechas y URL del PDF almacenado en Cloudinary.

### Relaciones

- Una factura tiene un emisor (`issuer`) y un deudor (`debtor`), ambos usuarios.
- Una factura puede tener un pago asociado.
- Un usuario puede emitir múltiples facturas y ser deudor en múltiples facturas.

## 3. `src/libs/validations/invoice.ts`

Este archivo contiene los schemas de validación para operaciones de facturas:

### Schemas

- **invoiceCreateSchema**: Valida los datos necesarios para crear una factura, incluyendo números, montos, fechas y PDF en base64.

- **invoiceUpdateSchema**: Valida los datos para actualizar una factura, permitiendo actualizar campos como asunto, descripción y monto.

- **paymentCreateSchema**: Valida los datos necesarios para registrar un pago en una factura.

## 4. `src/app/api/invoices/route.ts`

Este archivo maneja las operaciones sobre la colección de facturas.

### Endpoints

- **GET /api/invoices**: Lista todas las facturas del usuario autenticado (como emisor o deudor) con paginación.
  - Parámetros: `page`, `limit`, `status`, `role`

- **POST /api/invoices**: Crea una nueva factura.
  - Body: invoiceNumber, issuerUserId, debtorUserId, subject, amount, etc.
  - El PDF debe enviarse codificado.

## 5. `src/app/api/invoices/[id]/route.ts`

Este archivo maneja operaciones sobre facturas individuales.

### Endpoints

- **GET /api/invoices/:id**: Obtiene los detalles de una factura específica incluyendo información de pagos.
  - Solo el emisor o deudor pueden acceder.

- **PUT /api/invoices/:id**: Actualiza una factura.
  - Solo el emisor puede actualizar.
  - No se pueden actualizar facturas que ya tienen un pago registrado.
  - Permite reemplazar el PDF.

- **DELETE /api/invoices/:id**: Cancela o elimina una factura.
  - Solo el emisor puede cancelar.
  - Elimina el PDF de Cloudinary .