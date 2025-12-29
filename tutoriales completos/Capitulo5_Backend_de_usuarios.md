# Configuración del Backend: Validaciones, Seguridad y Endpoints de Usuarios

En este tutorial se explicará paso a paso cómo está organizado el backend encargado de validar usuarios, gestionar autenticación, controlar el acceso y ofrecer endpoints relacionados con perfiles y contactos.

1. Estructura de archivos del backend
    - validations/users.ts: Se añadirán funciones referentes a las nuevas validaciones respecto a perfiles de usuario, así como los esquemas utilizados para crear o actualizar perfiles y añadir contactos.
    - api-helpers.ts: Reúne funciones útiles para el backend, como la comprobación del usuario autenticado, la validación general de datos recibidos, el control de permisos entre usuarios y la gestión centralizada de errores y paginación.
    - /api/users/route.ts: Controla el endpoint encargado de devolver un listado paginado de todos los usuarios registrados, asegurando que solo usuarios con sesión pueden acceder.
    - /api/users/[id]/route.ts: Gestiona la obtención y actualización del perfil individual de un usuario, garantizando que cada persona solo pueda acceder o modificar su propia información.
    - /api/users/[id]/contacts/route.ts: Implementa el sistema de contactos entre usuarios, permitiendo consultar la lista de contactos o añadir nuevos, siempre comprobando identidades y validaciones necesarias.

2. Validaciones de datos con validations/users.ts
    Este archivo se actualizará para incluir las reglas que aseguren que los datos de edición enviados por el usuario sean correctos antes de llegar a la base de datos:
    Se actualizarán los esquemas que controlan cómo se editan y cómo se añaden contactos en relaciones muchos a muchos.

3. Herramientas de autenticación, autorización y manejo de errores (api-helpers.ts)
    Este archivo centralizará varias tareas críticas del backend:
    - Comprueba si el usuario que realiza la petición tiene una sesión activa.
    - Verifica que los usuarios solo puedan acceder o modificar su propia información, salvo en entornos de desarrollo.
    - Convierte cualquier error del sistema o de validación en una respuesta consistente y clara para el cliente.
    - Valida los cuerpos de las peticiones usando los esquemas previamente definidos.
    - Gestiona paginación a partir de parámetros como página, límite y desplazamiento.

4. Listado de usuarios (api/users/route.ts)
    Este archivo controlará el endpoint que devuelve un listado paginado de usuarios:
    - Solo permite el acceso si existe una sesión activa.
    - Analiza los parámetros de la URL para determinar página, límite y desplazamiento.
    - Consulta cuántos usuarios hay en total.
    - Devuelve un conjunto paginado con información esencial del usuario: correo, nombre, apellidos, teléfono, país, imagen, fecha de creación y actualización.

5. Gestión de perfiles individuales (api/users/[id]/route.ts)
    Este archivo estará centrado en la gestión del perfil personal de cada usuario, tanto para consultarlo como para actualizarlo.
    Para la lectura del perfil:
    - Comprueba que la persona esté autenticada.
    - Verifica que el usuario acceda solo a su propio perfil.
    - Devuelve los datos del perfil sin incluir información sensible.
    Para la actualización:
    - Se confirma la identidad del usuario.
    - Se reciben los datos enviados desde el cliente y se validan con las reglas establecidas.
    - Se actualizan únicamente los campos permitidos.
    - Se devuelve el perfil modificado.

6. Gestión de contactos entre usuarios (api/users/[id]/contacts/route.ts)
    Aquí se encontrará el sistema que permite a un usuario mantener una lista de contactos.

    - Para consultar los contactos:
        - Se exige autenticación.
        - Se interpreta el identificador del usuario directamente desde el path.
        - Solo se permite acceder a la propia lista de contactos.
        - Se obtiene el número total de contactos y se aplica paginación.
        - Se devuelven los datos esenciales de cada contacto.

    - Para añadir un nuevo contacto:
        - Se validan los datos enviados en el cuerpo de la petición.
        - Se impide que un usuario se añada a sí mismo.
        - Se comprueba que el contacto exista.
        - Se revisa que no esté ya en la lista de contactos.
        - Se agrega la relación en la base de datos y se devuelve la información del contacto añadido.
        - Si se detectan duplicidades o errores de validación, se responde de forma clara y estructurada.
