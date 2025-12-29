# Implementación de pruebas automatizadas

En este tutorial se explicará paso a paso cómo están organizados los archivos de prueba en el proyecto, enfocándose en su configuración y en cómo se gestionan las pruebas de funcionalidades como la autenticación, validación y operaciones sobre los usuarios y base de datos.

## 1. Estructura de archivos de pruebas y configuración

- **vitest.config.mts**: Configuración global para el framework de pruebas **Vitest**, que permite personalizar cómo se ejecutan las pruebas y qué herramientas adicionales o plugins se utilizan. También se establece la recolección de cobertura de código y la configuración del entorno.
  
- **tests/setup.ts**: Archivo de configuración global que se ejecuta antes de las pruebas, encargado de inicializar librerías, configurar el entorno, y preparar las dependencias necesarias, como bases de datos o mocks de APIs.
  
- **tests/helpers/request.ts**: Contiene funciones auxiliares para realizar solicitudes HTTP durante las pruebas, gestionar la autenticación y obtener respuestas JSON que faciliten la comprobación de las pruebas.
  
- **tests/libs/db.test.ts**: Archivo dedicado a probar las operaciones CRUD sobre la base de datos, asegurando que las interacciones con la base de datos funcionen correctamente, con un enfoque en el aislamiento de pruebas mediante la limpieza de registros.

- **tests/libs/auth.test.ts**: Pruebas relacionadas con la autenticación de usuarios, validación de credenciales y la gestión de tokens de sesión, garantizando que los usuarios autenticados accedan solo a recursos permitidos.

- **tests/libs/validations/helpers.test.ts**: Se enfoca en las pruebas de las funciones de validación general del sistema, como la comprobación de formatos y reglas de datos enviados por los usuarios.

- **tests/libs/validations/user.test.ts**: Contiene pruebas de validación específicas para los datos de usuario, como el nombre, correo electrónico, teléfono e imagen de perfil, asegurando que sean validados correctamente antes de ser procesados.

- **tests/api/users/users-list.test.ts**: Realiza pruebas sobre el endpoint encargado de devolver un listado paginado de usuarios, verificando que la paginación y las restricciones de acceso estén correctamente implementadas.

- **tests/api/users/user-profile.test.ts**: Prueba el endpoint de perfil de usuario, asegurando que los usuarios autenticados puedan obtener y actualizar su propio perfil, con validaciones adecuadas para los datos.

- **tests/api/auth/register.test.ts**: Prueba del endpoint de registro de nuevos usuarios, verificando que se validen correctamente los datos (correo electrónico, contraseña, etc.) y que se manejen los errores de manera adecuada.

- **tests/api/auth/credentials.test.ts**: Verifica la autenticación de usuarios mediante correo electrónico y contraseña, asegurando que los errores de autenticación sean gestionados correctamente y que las contraseñas no se filtren en las respuestas.

## 2. `vitest.config.mts`

Este archivo es la configuración de **Vitest**, el framework de pruebas utilizado en este proyecto. Permite personalizar cómo se ejecutan las pruebas y cómo se gestionan ciertos aspectos del entorno de prueba.

### Función

- **Configuración global de Vitest**: Define cómo se ejecutan las pruebas, qué configuraciones de entorno o plugins usar, y si se necesita alguna personalización en el comportamiento de las pruebas.
- **Especificación de pruebas**: Establece opciones como el tiempo máximo de ejecución de una prueba, la recolección de cobertura de código y la configuración de la consola de salida.
- **Integración con otros frameworks**: Permite integraciones con herramientas externas como `@testing-library` o `jest` en caso de ser necesario en el futuro.

## 3. `tests/setup.ts`

Este archivo se ejecuta antes de que las pruebas se inicien. Su función es configurar cualquier cosa necesaria a nivel global para que las pruebas se ejecuten correctamente.

### Función

- **Configuración global para pruebas**: Puede incluir la inicialización de librerías, la configuración de bases de datos, la limpieza de datos entre pruebas o la simulación de configuraciones de entorno.
- **Mocks y spies**: Aquí se pueden simular funciones globales, como las funciones relacionadas con la sesión o las APIs externas utilizadas durante las pruebas.
- **Inicialización de dependencias**: Configura el entorno de prueba, como la conexión con la base de datos de prueba o el establecimiento de variables de entorno específicas.

## 4. `tests/helpers/request.ts`

Este archivo contiene funciones auxiliares que facilitan la interacción con las APIs durante las pruebas. Proporciona funciones que simplifican la creación de solicitudes HTTP, la autenticación de los usuarios y la verificación de las respuestas.

### Función

- **Creación de peticiones HTTP**: Ayuda a crear solicitudes personalizadas (GET, POST, PUT, DELETE) con datos, cabeceras y autenticación adecuados.
- **Autenticación en pruebas**: Permite autenticar a los usuarios simulando una sesión activa.
- **Obtención de respuestas JSON**: Simplifica la obtención de respuestas JSON de las solicitudes, útil para realizar comprobaciones dentro de las pruebas.

## 5. `tests/libs/db.test.ts`

Este archivo contiene pruebas relacionadas con la base de datos, específicamente con las interacciones de la aplicación con la base de datos. Generalmente, se enfoca en comprobar que las operaciones de base de datos (CRUD) funcionen correctamente.

### Función

- **Pruebas de base de datos**: Verifica que las operaciones CRUD (Crear, Leer, Actualizar, Eliminar) se realicen correctamente.
- **Aislamiento entre pruebas**: Se asegura de que los datos de las pruebas no interfieran entre sí, limpiando los registros de la base de datos antes o después de las pruebas.
- **Simulación de datos**: Permite crear y eliminar usuarios, productos o cualquier otra entidad necesaria para las pruebas.

## 6. `tests/libs/auth.test.ts`

Este archivo prueba las funcionalidades relacionadas con la autenticación, como el manejo de tokens, la validación de credenciales y la gestión de la sesión del usuario.

### Función

- **Autenticación de usuarios**: Verifica que el sistema valide correctamente las credenciales de los usuarios y gestione correctamente los tokens.
- **Control de sesión**: Asegura que solo los usuarios autenticados puedan acceder a los endpoints protegidos.
- **Comprobaciones de seguridad**: Valida que el sistema maneje adecuadamente situaciones como el inicio de sesión con credenciales incorrectas o la expiración del token de sesión.

## 7. `tests/libs/validations/helpers.test.ts`

Este archivo contiene pruebas de las funciones de validación generales utilizadas en el sistema. Estas validaciones se aplican a los datos que los usuarios envían a través de las peticiones.

### Función

- **Pruebas de validación**: Verifica que las funciones de validación (como la verificación de formato de email, contraseñas seguras, etc.) funcionen correctamente.
- **Cobertura de validaciones generales**: Asegura que se estén validando correctamente los datos que el usuario envía en las peticiones.

## 8. `tests/libs/validations/user.test.ts`

Este archivo se enfoca en las pruebas de validación de los datos específicos del usuario, como la comprobación de un formato correcto de nombre, teléfono, país, etc.

### Función

- **Validación de datos de usuario**: Verifica que los datos del perfil de usuario sean validados correctamente antes de ser almacenados en la base de datos.
- **Pruebas de validación específicas**: Asegura que campos como nombre, correo electrónico, teléfono, imagen de perfil, etc., cumplan con las reglas de validación antes de ser procesados.

## 9. `tests/api/users/users-list.test.ts`

Este archivo contiene pruebas para el endpoint que devuelve un listado de usuarios, asegurando que el sistema maneje correctamente la paginación, el acceso y la autorización de la consulta de usuarios.

### Función

- **Listado de usuarios**: Asegura que el endpoint de listado de usuarios funcione correctamente, devolviendo una lista de usuarios paginada.
- **Autenticación y autorización**: Verifica que solo los usuarios autenticados puedan acceder al listado de usuarios.
- **Paginación**: Verifica que la respuesta del listado de usuarios sea paginada correctamente según los parámetros solicitados.

## 10. `tests/api/users/user-profile.test.ts`

Este archivo prueba el endpoint de perfil de usuario, cubriendo tanto la obtención del perfil como la actualización de los datos.

### Función

- **Obtención y actualización del perfil de usuario**: Verifica que los usuarios autenticados puedan consultar y actualizar sus perfiles correctamente.
- **Seguridad y permisos**: Asegura que los usuarios solo puedan acceder y modificar su propio perfil, a menos que se esté ejecutando en un entorno de desarrollo.
- **Validación de datos**: Verifica que se realicen validaciones adecuadas a los datos proporcionados durante la actualización del perfil (como formato de teléfono, correo, etc.).

## 11. `tests/api/auth/register.test.ts`

Este archivo contiene las pruebas del endpoint de registro de usuarios, asegurando que los usuarios puedan registrarse correctamente y que el sistema valide los datos correctamente.

### Función

- **Registro de nuevos usuarios**: Verifica que los usuarios puedan registrarse correctamente utilizando datos válidos.
- **Validación de datos de registro**: Asegura que los campos de registro sean validados correctamente, como el correo electrónico, la contraseña y otros campos opcionales.
- **Comprobación de errores**: Asegura que el sistema maneje correctamente los errores, como contraseñas débiles o correos duplicados.

## 12. `tests/api/auth/credentials.test.ts`

Este archivo prueba la autenticación de los usuarios mediante las credenciales (correo electrónico y contraseña), utilizando el proveedor de credenciales de NextAuth.

### Función

- **Autenticación con credenciales**: Verifica que los usuarios puedan autenticarse correctamente con su correo electrónico y contraseña.
- **Manejo de errores de autenticación**: Asegura que el sistema devuelva un error adecuado cuando las credenciales sean incorrectas o estén vacías.
- **Verificación de seguridad**: Se asegura de que la contraseña del usuario no se devuelva en las respuestas y de que el sistema maneje correctamente los casos de inicio de sesión fallidos.

---
