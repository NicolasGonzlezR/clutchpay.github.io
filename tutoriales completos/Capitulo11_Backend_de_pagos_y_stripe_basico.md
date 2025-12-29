# Implementación de Gestión de Pagos y Sesiones en Stripe

Este tutorial se configura para manejar los pagos de facturas a través de **Stripe**, junto con la gestión de sesiones de pago y verificación del estado de los pagos.

## 1. Estructura de archivos de pruebas y configuración

- **src/libs/validations/payment.ts**: Define los schemas de validación para los pagos utilizando **Zod**. Estos incluyen las validaciones para la lista de pagos con filtros, rangos de monto y fechas de pago.

- **src/libs/validations/stripe.ts**: Define los schemas de validación para las operaciones relacionadas con **Stripe**, como la creación de sesiones de pago y la validación de eventos de Stripe Webhooks.

- **src/libs/stripe.ts**: Archivo que gestiona la interacción con la API de **Stripe**, creando sesiones de pago, verificando firmas de webhooks y mapeando estados de sesiones. Contiene funciones para crear una sesión de pago en Stripe, manejar errores y convertir montos de pago entre formato decimal y centavos.

- **src/app/api/payments/route.ts**: Este archivo maneja las operaciones para obtener una lista paginada de los pagos realizados o recibidos por el usuario autenticado. Soporta filtros como el método de pago, el rango de monto y fechas, y permite ordenar los resultados.

- **src/app/api/payments/[id]/route.ts**: Permite acceder a los detalles de un pago específico, asegurando que solo el pagador (deudor) o el receptor (emisor) de la factura puedan consultar el pago.

- **src/app/api/payments/stripe/checkout/route.ts**: Crea una sesión de pago de **Stripe Checkout** para un pago de factura. Solo el deudor (quien debe la factura) puede iniciar el pago. La factura debe tener un estado pendiente o vencido para ser pagada.

- **src/app/api/payments/stripe/session/[sessionId]/route.ts**: Recupera el estado y los detalles de una sesión de pago de **Stripe** usando el `sessionId`. Solo el pagador o receptor involucrado en la sesión de pago puede acceder a la información.

## 2. `prisma/schema.prisma`

Este archivo contiene el modelo `Invoice` y sus relaciones con los pagos, permitiendo gestionar facturas y asociarlas con usuarios. Este modelo está relacionado con el pago de facturas y su seguimiento.

### Modelos

- **Invoice**: Representa una factura con campos como número de factura, usuarios relacionados, monto, estado, fechas de emisión y vencimiento, y URL del PDF en **Cloudinary**.

### Relaciones

- Una factura tiene un emisor (`issuer`) y un deudor (`debtor`), ambos usuarios.
- Una factura puede tener un pago asociado.
- Un usuario puede emitir múltiples facturas y ser deudor en múltiples facturas.

## 3. `src/libs/validations/invoice.ts`

Este archivo contiene los schemas de validación para las operaciones relacionadas con las facturas.

### Schemas

- **invoiceCreateSchema**: Valida los datos necesarios para crear una factura, incluyendo número de factura, monto, fechas y PDF.
- **invoiceUpdateSchema**: Valida los datos necesarios para actualizar una factura, como el asunto, la descripción y el monto.
- **paymentCreateSchema**: Valida los datos necesarios para registrar un pago de una factura.

## 4. `src/app/api/invoices/route.ts`

Este archivo gestiona las operaciones sobre la colección de facturas, permitiendo crear y listar facturas.

### Endpoints

- **GET /api/invoices**: Lista todas las facturas del usuario autenticado (como emisor o deudor) con paginación.
  - Parámetros: `page`, `limit`, `status`, `role`.

- **POST /api/invoices**: Crea una nueva factura.
  - Body: `invoiceNumber`, `issuerUserId`, `debtorUserId`, `subject`, `amount`, etc.

## 5. `src/app/api/invoices/[id]/route.ts`

Este archivo maneja las operaciones sobre facturas individuales.

### Endpoints

- **GET /api/invoices/:id**: Obtiene los detalles de una factura específica, incluyendo información sobre los pagos asociados.
  - Solo el emisor o deudor pueden acceder a la factura.

- **PUT /api/invoices/:id**: Actualiza una factura.
  - Solo el emisor puede actualizar la factura.
  - No se pueden actualizar facturas que ya tengan un pago registrado.
  - Permite reemplazar el PDF de la factura.

- **DELETE /api/invoices/:id**: Cancela o elimina una factura.
  - Solo el emisor puede cancelar la factura.
  - Elimina el PDF de la factura de **Cloudinary**.

## 6. `src/app/api/payments/route.ts`

Este archivo maneja las operaciones sobre la colección de pagos de facturas, permitiendo consultar y filtrar pagos según criterios como el rol de usuario, el método de pago y el rango de monto.

### Endpoints

- **GET /api/payments**: Obtiene una lista paginada de pagos realizados por el usuario autenticado (como pagador o receptor).
  - Parámetros: `role` (valor `payer` o `receiver`), `paymentMethod`, `minAmount`, `maxAmount`, `paymentDateFrom`, `paymentDateTo`, `sortBy`, `sortOrder`.

## 7. `src/app/api/payments/[id]/route.ts`

Este archivo maneja las operaciones sobre pagos individuales, permitiendo consultar los detalles de un pago específico.

### Endpoints

- **GET /api/payments/:id**: Obtiene los detalles de un pago específico.
  - Solo el pagador o el receptor de la factura pueden acceder al pago.

## 8. `src/app/api/payments/stripe/checkout/route.ts`

Este archivo maneja la creación de sesiones de pago utilizando **Stripe Checkout** para una factura.

### Endpoints

- **POST /api/payments/stripe/checkout**: Crea una sesión de pago de Stripe para que el deudor pague una factura.
  - Parámetros: `invoiceId`, `successUrl`, `cancelUrl`.
  - Solo el deudor de la factura puede iniciar el pago.
  - Verifica que la factura esté en estado **PENDING** o **OVERDUE** para poder ser pagada.

## 9. `src/app/api/payments/stripe/session/[sessionId]/route.ts`

Este archivo permite recuperar el estado y los detalles de una sesión de pago de **Stripe** utilizando el `sessionId`.

### Endpoints

- **GET /api/payments/stripe/session/:sessionId**: Obtiene el estado de una sesión de pago de Stripe y detalles sobre la factura asociada.
  - Solo el pagador o el receptor de la factura pueden acceder a la sesión.
  - Devuelve el estado de la sesión, el monto y la información de la factura.
