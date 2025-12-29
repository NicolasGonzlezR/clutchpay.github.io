# Implementación de Nuevas Funcionalidades en el Dashboard de usuario respecto a pagos con Stripe

En este tutorial se  describe las modificaciones implementadas en los archivos del proyecto, específicamente las referentes a nuevas funcionalidades añadidas para la gestión de pagos, la navegación y el manejo de estados de pago.

## 1. Archivos Modificados

- **public/JS/dashboard/invoices.js**
- **public/JS/dashboard_usuario.js**
- **public/main.html**

## 2. `public/JS/dashboard/invoices.js`

En este archivo se han implementado varias modificaciones relacionadas con la gestión de facturas y pagos. Las nuevas funcionalidades incluyen la carga de información del deudor, la obtención del recibo de pago cuando una factura es pagada y la integración con el sistema de pagos de Stripe para procesar pagos de facturas. Además, se maneja la visualización de los detalles relacionados con cada factura.

### 2.1. Cargar Información del Deudor
Se ha añadido una funcionalidad para cargar la información del deudor de una factura, que se obtiene desde la API usando el `debtorUserId`. Esto se hace en caso de que el usuario quiera ver los detalles del deudor asociado a la factura. La información que se muestra incluye el nombre completo o el correo electrónico del deudor.

### 2.2. Cargar Recibo de Pago
Cuando la factura tiene el estado **PAID**, se agrega una lógica que permite cargar el recibo de pago asociado. Para esto, el sistema realiza dos solicitudes para obtener los pagos del pagador y del receptor. Si el recibo está disponible, se extrae la URL del PDF del recibo para que el usuario pueda consultarlo.

### 2.3. Manejo de Pago con Stripe
Se ha integrado una funcionalidad que permite a los usuarios pagar las facturas utilizando Stripe. Al hacer clic en el botón de pago, se crea una sesión de pago a través de la API de Stripe. Si el proceso es exitoso, el usuario es redirigido a la página de pago de Stripe. En caso de error, se muestra un mensaje informando al usuario y el botón de pago se restaura a su estado original.

## 3. `public/JS/dashboard_usuario.js`

En este archivo se han realizado cambios para mejorar la navegación entre secciones del dashboard y gestionar los estados de pago del usuario. Ahora, el sistema permite al usuario navegar dinámicamente entre las pestañas, y maneja los parámetros de pago de la URL para mostrar mensajes relacionados con el estado del pago (exitoso o cancelado).

### 3.1. Inicialización de Pagos
Se ha añadido la inicialización de la gestión de pagos dentro del dashboard. Esto se hace llamando a `dashboardPayments.init()` para preparar el sistema para la carga y visualización de pagos.

### 3.2. Navegación entre Pestañas
Se ha implementado la lógica para que el usuario pueda navegar entre las diferentes pestañas del dashboard. Al hacer clic en una pestaña, la interfaz se actualiza para reflejar la sección activa, proporcionando una experiencia de usuario más dinámica.

### 3.3. Manejo de Parámetros de Pago en la URL
Cuando el usuario es redirigido desde Stripe después de realizar un pago, se han añadido verificaciones para comprobar el estado del pago. Dependiendo de si el pago fue exitoso o cancelado, se muestra un mensaje correspondiente al usuario y se limpia la URL para evitar la visualización de parámetros sensibles.

## 4. `public/main.html`

En este archivo se han realizado modificaciones relacionadas con la visualización de pagos en el dashboard del usuario. Se ha añadido una nueva sección para mostrar los pagos realizados, con la opción de ordenarlos por fecha o cantidad. Además, se ha agregado un mensaje que se muestra cuando no hay pagos disponibles.

### 4.1. Sección de Pagos
Se ha añadido una nueva sección de pagos al archivo `main.html`, donde los usuarios pueden ver todos los pagos asociados a sus facturas. Esta sección permite ordenar los pagos por fecha o por cantidad. Si no hay pagos registrados, se muestra un mensaje indicándole al usuario que cuando realice pagos, estos aparecerán aquí.

### 4.2. Filtros para Ordenar Pagos
Dentro de la nueva sección de pagos, se ha añadido un selector que permite al usuario ordenar los pagos por **Fecha de Pago** o **Cantidad**. Además, el sistema permite invertir el orden de la lista, con un botón que alterna entre los modos ascendente y descendente.
