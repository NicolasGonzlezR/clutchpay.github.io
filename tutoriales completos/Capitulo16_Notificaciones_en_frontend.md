# Implementación del Sistema de Notificaciones

En este tutorial se describe el proceso para implementar la funcionalidad completa del sistema de notificaciones en el proyecto, que incluye la gestión de notificaciones internas para eventos como la creación y cancelación de facturas, y la visualización de notificaciones en la interfaz de usuario.

## 1. Estructura de Archivos de Pruebas y Configuración

- **public/JS/internal-notifications.js**: Este archivo maneja la lógica para el sistema de notificaciones internas, permitiendo la visualización, actualización (marcar como leídas) y eliminación de notificaciones.
  
- **public/JS/dashboard-usuario.js**: Se integra la lógica del sistema de notificaciones con el dashboard del usuario, permitiendo la inicialización y manejo global del sistema de notificaciones.

- **app/api/invoices/route.ts**: Aquí se realiza la notificación cuando se crea una nueva factura, informando a los usuarios sobre la emisión de la misma.

- **app/api/invoices/[id]/route.ts**: Se envía una notificación cuando una factura es cancelada o eliminada.

- **public/main.html**: Se configura la interfaz de usuario con un botón que abre un modal para mostrar las notificaciones.

## 2. `public/JS/internal-notifications.js`

Este archivo contiene la implementación del sistema de notificaciones internas de la aplicación. El sistema permite visualizar las notificaciones en un modal, marcar las notificaciones como leídas y eliminar las notificaciones leídas.

### Funcionalidades principales

- **Inicialización**: El sistema de notificaciones se inicializa con la creación de una instancia de `InternalNotifications`. Esta instancia maneja todas las operaciones relacionadas con la obtención, visualización y actualización de las notificaciones.
  
- **Obtención de notificaciones**: Mediante la función `fetchNotifications`, el sistema obtiene las notificaciones desde el backend. Los datos recuperados incluyen el número de notificaciones no leídas, y la lista de notificaciones que se deben mostrar.

- **Interacción con el Modal**: El modal de notificaciones permite a los usuarios visualizar todas las notificaciones disponibles. Además, los usuarios pueden realizar acciones como marcar todas las notificaciones como leídas o eliminar las notificaciones leídas.

- **Acciones sobre notificaciones**: Se han añadido funcionalidades para:
  - **Marcar como leídas**: Permite al usuario marcar notificaciones específicas o todas las notificaciones como leídas.
  - **Eliminar notificaciones**: Permite eliminar todas las notificaciones leídas, ayudando a mantener limpio el sistema.

## 3. `public/JS/dashboard-usuario.js`

Este archivo se encarga de integrar el sistema de notificaciones en el dashboard del usuario, proporcionando la lógica necesaria para inicializar el sistema de notificaciones y permitir su acceso a través de la interfaz de usuario.

### Cambios realizados

- **Inicialización del sistema de notificaciones**: Se ha añadido la creación de una instancia de `InternalNotifications` al cargar la página. La instancia se inicializa y se hace accesible globalmente para manejar las interacciones con las notificaciones.

  - **Objetivo**: Permitir que los usuarios puedan acceder y manipular el sistema de notificaciones desde cualquier parte del dashboard.

- **Acceso global**: La instancia de `notificationSystem` se hace accesible globalmente a través de `window.notificationSystem`, lo que permite su uso desde otras partes de la interfaz de usuario que necesiten interactuar con las notificaciones.

## 4. `app/api/invoices/route.ts`

Este archivo maneja las operaciones de la API relacionadas con las facturas. Una de las principales funcionalidades agregadas es la notificación cuando se crea una nueva factura.

### Cambios realizados

- **Notificación al crear una factura**: Se ha integrado la función `notifyInvoiceIssued(invoice)` para enviar una notificación a los usuarios relacionados cuando una factura es creada. Esta notificación informa sobre la emisión de la factura, garantizando que los usuarios estén al tanto de la nueva factura.

- **Contexto de uso**: La notificación se envía después de que una factura ha sido creada correctamente, asegurando que los usuarios, como el emisor o el deudor de la factura, reciban la notificación correspondiente.

- **Funcionalidad adicional**: Además de crear facturas, se asegura que el sistema de notificaciones esté bien integrado en el proceso de la creación, activando notificaciones automáticamente al generar nuevas facturas.

### Endpoint relevante

- **POST /api/invoices**: Este endpoint se encarga de crear una nueva factura y notificar a los usuarios sobre la emisión de la misma.

## 5. `app/api/invoices/[id]/route.ts`

Este archivo maneja las operaciones sobre facturas individuales, como obtener detalles, actualizar o eliminar facturas. En esta sección se ha añadido la capacidad de notificar a los usuarios cuando una factura es cancelada.

### Cambios realizados

- **Notificación de cancelación de factura**: Cuando una factura es cancelada o eliminada, se llama a la función `notifyInvoiceCanceled(invoice)`, lo que garantiza que los usuarios sean notificados sobre la cancelación.

- **Contexto de uso**: Esta notificación se envía automáticamente después de que una factura ha sido cancelada correctamente, informando a los usuarios sobre el cambio en el estado de la factura.

### Endpoint relevante

- **DELETE /api/invoices/:id**: Este endpoint se utiliza para cancelar o eliminar una factura, y en el proceso se envía una notificación a los usuarios relacionados.

## `public/main.html`

Este archivo contiene el botón y el modal para manejar la visualización de notificaciones en la interfaz de usuario. Los cambios realizados aseguran que los usuarios puedan acceder a sus notificaciones de manera fácil y rápida.

### Cambios realizados

- **Botón de notificaciones**: Se añadió un botón con el ícono de campana que permite a los usuarios abrir el modal de notificaciones. El botón también incluye un contador de notificaciones no leídas, que se actualiza dinámicamente según las notificaciones disponibles.

- **Modal de notificaciones**: Se implementó un modal que muestra la lista de notificaciones cuando el usuario hace clic en el botón de notificaciones. Este modal también permite al usuario realizar acciones como marcar las notificaciones como leídas o eliminarlas si ya han sido leídas.

- **Diseño del modal**: El diseño es sencillo, con un encabezado para indicar que se trata de notificaciones, botones para marcar todas como leídas o eliminar las leídas, y un área donde se listan las notificaciones.

### Elementos relevantes

- **Botón de notificaciones**: Se muestra un ícono con un contador de notificaciones no leídas.
- **Modal**: Contiene opciones para marcar todas las notificaciones como leídas o eliminarlas.