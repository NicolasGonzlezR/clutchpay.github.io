# Implementación de Gestión de Pagos con Stripe

En este tutorial se describe el proceso para implementar la funcionalidad completa de gestión de pagos (payments) en el proyecto, utilizando Stripe como pasarela de pago desde el frontend. Se incluyen la creación de sesiones de checkout, la consulta del estado de los pagos, el listado de pagos del usuario y la obtención del detalle de un pago.

## 1. Estructura de archivos de pagos

- **public/JS/payments.js**: módulo principal para la gestión de pagos en la aplicación.

- **public/JS/dashboard/payments.js**: módulo de gestión de pagos utilizado dentro del dashboard del usuario.

## 2. `public/JS/payments.js`

Este archivo define la clase `PaymentManager`, encargada de manejar todo el flujo de pagos con Stripe desde el frontend.

### Responsabilidades

- Crear sesiones de Stripe Checkout para facturas.
- Consultar el estado de sesiones de pago.
- Listar los pagos asociados al usuario autenticado.
- Obtener el detalle de un pago específico.
- Centralizar el manejo de errores HTTP.

### Dependencias

- **Auth**: instancia utilizada para obtener la variable `API_BASE_URL`.
- **Fetch API**: utilizada para comunicarse con el backend.
- **Cookies de sesión**: enviadas mediante `credentials: 'include'`.

## 3. Clase `PaymentManager`

La clase `PaymentManager` actúa como intermediaria entre la interfaz de usuario y la API de pagos.

### Constructor

- Recibe una instancia de `Auth`.
- Inicializa la URL base de la API (`API_BASE_URL`).

### Métodos

- **createCheckoutSession(invoiceId, options)**  
  Crea una sesión de Stripe Checkout para iniciar un pago.
  - Genera automáticamente las URLs de éxito y cancelación.
  - Envía el ID de la factura al backend.
  - Retorna el ID de la sesión y la URL de pago.

- **getSessionStatus(sessionId)**  
  Consulta el estado de una sesión de Stripe.
  - Valida el formato del ID de sesión (`cs_`).
  - Retorna estado, monto, moneda y factura asociada.

- **listPayments(options)**  
  Lista los pagos del usuario autenticado.
  - Permite filtrar por rol (`payer` o `receiver`).
  - Soporta filtros por método de pago.
  - Incluye paginación y ordenamiento.

- **getPaymentDetail(paymentId)**  
  Obtiene el detalle completo de un pago específico.

## 4. Endpoints consumidos

La clase `PaymentManager` consume los siguientes endpoints del backend:

### Stripe

- **POST /api/payments/stripe/checkout**  
  Crea una sesión de Stripe Checkout.
  - Body: `invoiceId`, `successUrl`, `cancelUrl`

- **GET /api/payments/stripe/session/:sessionId**  
  Obtiene el estado de una sesión de pago.

### Pagos

- **GET /api/payments**  
  Lista los pagos del usuario.
  - Parámetros: `role`, `paymentMethod`, `page`, `limit`, `sortBy`, `sortOrder`

- **GET /api/payments/:id**  
  Obtiene el detalle de un pago específico.

## 5. Manejo de errores

El manejo de errores se centraliza en el método `getErrorMessage`.

### Códigos soportados

- **400**: datos inválidos.
- **401**: usuario no autenticado.
- **403**: permisos insuficientes.
- **404**: recurso no encontrado.
- **409**: la factura ya ha sido pagada.
- **500**: error interno del servidor.

Cada error HTTP se transforma en un mensaje legible para la interfaz de usuario.