# Implementación del Flujo de Pagos y Recibos

En este tutorial se describe el proceso para implementar el flujo completo de procesamiento de pagos en ClutchPay, incluyendo la recepción de pagos vía Stripe Checkout, la generación de recibos en PDF, y la distribución de fondos mediante PayPal Payouts.

El flujo está diseñado para ser **seguro y tolerante a fallos**, permitiendo manejar pagos síncronos y asíncronos (como PayPal vía Stripe).


## 1. Estructura de archivos de pagos y recibos

- **src/libs/pdf-generator.ts**: librería encargada de generar recibos de pago en formato PDF con branding de ClutchPay.

- **src/libs/paypal.ts**: integración con PayPal Payouts para transferir fondos al emisor de la factura, incluyendo simulación en entornos de desarrollo.

- **src/app/api/payments/stripe/webhook/route.ts**: endpoint webhook que procesa eventos de Stripe relacionados con pagos exitosos, pagos asíncronos y expiraciones.

## 2. `src/libs/pdf-generator.ts`

Este archivo contiene la lógica para generar recibos de pago en formato PDF utilizando **PDFKit**, aplicando estilos, colores y estructura visual consistente con la marca ClutchPay.

### Funcionalidad principal

- Genera un **recibo electrónico** en formato PDF.
- Incluye información de:
  - Pago
  - Factura
  - Pagador y receptor
- Aplica branding visual (colores, encabezado, logotipo).
- Devuelve un `Buffer` listo para ser almacenado o subido a un proveedor externo (ej. Cloudinary).

### Interfaz de datos

- **ReceiptData**:
  - Referencia de pago
  - Fecha de pago
  - Monto y moneda
  - Método de pago
  - Número de factura
  - Asunto
  - Datos del pagador y receptor

### Características clave

- Encabezado con efecto de gradiente
- Soporte para logotipo dinámico
- Diseño en dos columnas para detalles de pago y factura
- Sección de partes involucradas (payer / receiver)
- Pie de página con aviso legal

## 3. `src/libs/paypal.ts`

Este archivo implementa la integración con **PayPal Payouts SDK**, permitiendo transferir automáticamente fondos al emisor de la factura una vez confirmado el pago en Stripe.

### Configuración

Variables de entorno requeridas:

- `PAYPAL_CLIENT_ID`
- `PAYPAL_CLIENT_SECRET`
- `PAYPAL_MODE` (`sandbox` o `live`)

El entorno se selecciona automáticamente según la configuración.

### Funcionalidades

- **createPayPalPayout**:
  - Crea un payout a un email de PayPal
  - Convierte montos de centavos a formato decimal
  - Genera un `sender_batch_id` único
  - Devuelve información del batch y la transacción

- **getPayoutStatus**:
  - Consulta el estado de un payout batch existente

- **calculateNetAfterFees**:
  - Calcula el monto neto después de comisiones estimadas

- **isValidPayPalEmail**:
  - Valida el formato de un email de PayPal

### Modo simulación

Cuando las credenciales de PayPal no están configuradas:

- Los payouts se **simulan automáticamente**
- Se devuelven respuestas exitosas para permitir desarrollo y testing local
- No se bloquea el flujo principal de pagos

## 4. `src/app/api/payments/stripe/webhook/route.ts`

Este archivo implementa el **webhook de Stripe**, encargado de procesar eventos relacionados con pagos realizados mediante Stripe Checkout.
