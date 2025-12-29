# Cambios Frontend para Gestión de Facturas

En este tutorial se harán varios cambios a archivos previamente establecidos para poder dotar de una mayor modularidad a la aplicación y dotarla también de nuevas funciones como el modo
claro o oscuro de css. Además se incorporarán los cambios para poder crear facturas.

## 1. Archivos modificados / añadidos

- **public/JS/dashboard/core.js**: Núcleo del dashboard. Maneja inicialización, ruteo interno entre módulos, y provee una API simple para los módulos (mostrar modales, manejar sesión, fetch helpers con `credentials: 'include'`).

- **public/JS/dashboard/invoices.js**: Lógica de interfaz para listado, creación, edición y detalle de facturas. Consume los endpoints `/api/invoices` y `/api/invoices/:id`.

- **public/JS/dashboard/profile.js**: Gestión del perfil de usuario en el dashboard.

- **public/JS/dashboard/contacts.js**: Manejo de la lista de contactos y su relación con facturas (selección de deudor/emisor).

- **public/JS/dashboard/mobile.js**: Adaptaciones y manejo de eventos para vistas móviles del dashboard.

- **public/JS/notifications.js**: Sistema de toasts/alertas para feedback de acciones (éxito/error/aviso), usado por todos los módulos.

- **public/JS/theme.js**: Manejador de tema (light/dark), persiste la preferencia en `localStorage` y aplica `data-theme` al `documentElement`.

- **public/main.html** / **public/index.html** (o el HTML del dashboard): Actualizados para cargar los nuevos módulos y respetar carga condicional de scripts.

- **public/JS/validaciones.js**: Actualizaciones del cliente para validar formularios antes de enviar (coincide con zod/validaciones del servidor pero orientado a UX inmediata).

## 2. `public/JS/dashboard/core.js`

Núcleo del dashboard. Responsabilidades principales:

- Inicializar la aplicación dentro del DOM del dashboard.
- Registrar y cargar módulos (`invoices`, `contacts`, `profile`, etc.).
- Proveer un wrapper de `fetch` que incluye `credentials: 'include'`, normaliza errores y parsing de respuestas.
- Ofrecer utilidades compartidas: paginación, manejo de formularios (form-to-json), conversión de archivos a base64 y un event-bus/simple API para que los módulos interactúen.

## 3. `public/JS/dashboard/invoices.js`

Lógica de interfaz para la gestión de facturas:

- Listados con filtros (estado, página, límite), búsquedas y paginación.
- Formularios de creación y edición con validación previa usando `validaciones.js`.
- Conversión opcional de PDFs a base64 para envío en `POST /api/invoices`.
- Vista de detalle que muestra metadatos, vista previa o enlace del PDF y pagos asociados.
- Acciones del recurso: crear, actualizar, cancelar (PUT/DELETE según permisos), y marcar pagos; además manejo de estados UI cuando la factura tiene pago registrado.

## 4. `public/JS/dashboard/profile.js`

Gestión del perfil de usuario dentro del dashboard:

- Mostrar y editar datos del usuario.
- Integración con avatar/imagen si aplica (subida/preview).
- Notificar cambios a otros módulos si necesario (por ejemplo, actualización de nombre en listas).

## 5. `public/JS/dashboard/contacts.js`

Administración de contactos y su uso en facturas:

- CRUD de contactos (crear, listar, editar, eliminar).
- Búsqueda y paginación de contactos.
- Selección de `debtor`/`issuer` al crear o editar facturas.

## 6. `public/JS/dashboard/mobile.js`

Adaptaciones para vistas móviles y mejoras de interacción táctil:

- Manejo de menús, colapsables y navegación simplificada para pantallas pequeñas.
- Ajustes en comportamiento de modales y reducción de payloads cuando procede.
- Interacción optimizada para controles táctiles.

## 7. `public/JS/notifications.js`

Sistema de toasts/alertas centralizado:

- API simple: `success(msg)`, `error(msg)`, `info(msg)`.
- Control de queue de notificaciones, tiempos de expiración y cierre manual.
- Accesibilidad: roles/atributos ARIA para que lectores de pantalla detecten los mensajes.

## 8. `public/JS/theme.js`

Gestión de tema (light/dark):

- Funciones `getTheme()` y `setTheme('light'|'dark')`.
- Persistencia en `localStorage` y respetar la preferencia del sistema cuando no existe preferencia guardada.
- Aplicar `data-theme` (o clase) en `document.documentElement` y animaciones/transiciones suaves.

## 9. `public/JS/validaciones.js`

Validaciones en cliente orientadas a UX:

- Reglas esenciales: required, formatos numéricos, rangos, validación de fechas y límites.
- Mensajes inline coherentes con las reglas del servidor (`src/libs/validations`) para evitar confusión.
- Helpers para normalizar campos antes de enviar (trimming, casting numérico, formato de fechas).

## 10. `public/main.html` / `public/index.html`

Actualizaciones en el HTML del dashboard:

- Inclusión y orden de carga de scripts modulares (`core.js` y módulos del dashboard).
- Marcas para puntos de montaje de los módulos y toggles de tema/menú.
- Consideraciones para carga condicional en mobile o rutas internas del dashboard.

