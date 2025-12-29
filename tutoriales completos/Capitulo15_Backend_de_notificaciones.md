# Implementación de Gestión de Notificaciones

En este tutorial se describe el proceso para implementar la funcionalidad completa de gestión de notificaciones en el proyecto, incluyendo creación, lectura, actualización, eliminación y envío de correos electrónicos relacionados con facturas y pagos.

## 1. Estructura de archivos de notificaciones y configuración

- **src/libs/notifications.ts**: Contiene la lógica principal para crear, formatear y enviar notificaciones, tanto in-app como por email.

- **src/libs/email/templates/**: Contiene las plantillas de emails para distintos tipos de notificaciones (`InvoiceIssuedEmail`, `PaymentReceivedEmail`, etc.).

- **src/app/api/notifications/route.ts**: Endpoint para listar, marcar como leídas y eliminar notificaciones de manera masiva.

- **src/app/api/notifications/[id]/route.ts**: Endpoint para obtener, actualizar y eliminar notificaciones específicas.

- **src/libs/validations/notification.ts**: Schemas de validación usando Zod para las operaciones de notificaciones.

## 2. `src/libs/notifications.ts`

Este archivo contiene toda la lógica de notificaciones de la aplicación.

### Funcionalidades principales

- **Creación de notificaciones in-app**: Para eventos como facturas emitidas, pagos recibidos, facturas canceladas y pagos vencidos o atrasados.

- **Envío de correos electrónicos**: Se utilizan plantillas React y datos del usuario para enviar notificaciones por email si el usuario tiene habilitadas las notificaciones por correo.

- **Formato de mensajes**: Los mensajes incluyen placeholders como `{invoiceNumber}`, `{issuerName}`, `{debtorName}`, `{amount}`, `{currency}`, `{dueDate}` que se reemplazan con los datos reales.

- **Formateo de respuesta**: Se construyen objetos listos para la API con el mensaje formateado, estado de lectura y datos de la factura asociada.

### Funciones importantes

- **notifyInvoiceIssued(invoice: InvoiceWithUsers)**: Notifica al deudor que se ha emitido una nueva factura.

- **notifyPaymentReceived(invoice: InvoiceWithUsers)**: Notifica al emisor que se ha recibido un pago.

- **notifyInvoiceCanceled(invoice: InvoiceWithUsers, reason?: string)**: Notifica al deudor que la factura ha sido cancelada.

- **notifyPaymentDue(invoice: InvoiceWithUsers)**: Notifica al deudor que una factura está próxima a vencer.

- **notifyPaymentOverdue(invoice: InvoiceWithUsers)**: Notifica al deudor que una factura está vencida.

- **formatNotificationResponse(notification)**: Formatea una notificación para la respuesta de la API.

- **cleanupOldReadNotifications(daysOld: number = 30)**: Elimina notificaciones leídas antiguas.

- **checkAndNotifyPaymentDue(daysBeforeDue: number = 3)** y **checkAndNotifyPaymentOverdue()**: Funciones de scheduler para enviar notificaciones automáticamente según fechas de vencimiento.

## 3. `src/libs/validations/notification.ts`

Este archivo contiene los schemas de validación para operaciones de notificaciones:

### Schemas

- **notificationListQuerySchema**: Valida los parámetros de consulta al listar notificaciones (paginación, tipo, estado de lectura, orden).

- **notificationBulkReadSchema**: Valida los datos para marcar notificaciones como leídas de forma masiva.

- **notificationBulkDeleteSchema**: Valida los datos para eliminar notificaciones de forma masiva.

- **notificationIdParamSchema**: Valida que el parámetro `id` de la ruta sea un número válido.

- **notificationUpdateSchema**: Valida la actualización de una notificación individual (por ejemplo, marcar como leída).

## 4. `src/app/api/notifications/route.ts`

Este archivo maneja operaciones sobre la colección de notificaciones.

### Endpoints

- **GET /api/notifications**: Lista todas las notificaciones del usuario autenticado con paginación y filtros.
  - Parámetros: `page`, `limit`, `read`, `type`, `sortBy`, `sortOrder`.

- **PATCH /api/notifications**: Marca notificaciones como leídas.
  - Body: `notificationIds` (IDs a marcar) o `markAllAsRead` (marcar todas como leídas).

- **DELETE /api/notifications**: Elimina notificaciones.
  - Body: `notificationIds` (IDs a eliminar) o `deleteAllRead` (eliminar todas las leídas).

## 5. `src/app/api/notifications/[id]/route.ts`

Este archivo maneja operaciones sobre notificaciones individuales.

### Endpoints

- **GET /api/notifications/:id**: Obtiene los detalles de una notificación específica incluyendo la factura asociada.
  - Solo el usuario propietario puede acceder.

- **PATCH /api/notifications/:id**: Actualiza el estado de lectura de una notificación específica.
  - Body: `read` (boolean).

- **DELETE /api/notifications/:id**: Elimina una notificación específica.
  - Solo el usuario propietario puede eliminarla.