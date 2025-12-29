# Configuración del Frontend en ClutchPay: Formularios, Validaciones y Estilos

En este tutorial se explicará paso a paso cómo configurar el frontend de ClutchPay, incluyendo formularios de registro e inicio de sesión, validaciones de datos e interacciones con la API de autenticación.  

Al final, tendremos un frontend totalmente funcional, con validaciones en tiempo real, traducción de elementos y un estilo consistente.

1. Estructura de archivos del frontend
    - **validaciones.js**: Contiene funciones de validación para formularios (nombre, apellidos, email, contraseña, teléfono).
    - **auth.js**: Clase Auth que maneja la comunicación con los endpoints de autenticación (login, register, logout, checkSession).
    - **auth-register.js**: Lógica específica del formulario de registro, incluyendo traducción de países, envío de datos y manejo de errores.
    - **auth-login.js**: Lógica específica del formulario de inicio de sesión, con envío de datos y manejo de sesión.
    - **style.css**: Define todos los estilos.

2. Validaciones de formularios con validaciones.js  
    - El archivo validaciones.js contiene funciones independientes que aseguran que los datos ingresados por los usuarios sean correctos antes de enviarlos al backend.

3. Clase de autenticación Auth **(auth.js)**
    - El archivo auth.js centralizará todas las operaciones con el backend:
        - Envia los datos al endpoint /api/auth/callback/credentials y devuelve un objeto indicando éxito o error.
        - Envía los datos del nuevo usuario al endpoint /api/auth/register y devuelve si la operación fue exitosa.
        - Verifica si hay un usuario autenticado activo en la sesión.
        - Cierra la sesión en el backend y redirige al usuario a la página de inicio.

4. Formulario de registro **(auth-register.js)**
    - Este archivo manejará interacciones específicas del formulario de registro:
        - Los elementos `\<option\>` del `\<select\>` se traducen según el idioma guardado en localStorage.
        - Se obtiene el valor de todos los campos (nombre, apellidos, email, contraseña, teléfono, país, imagen).
        - Se llama a authInstance.register(formData) para crear un nuevo usuario en el backend.
        - Si hay errores, se muestran y se habilita nuevamente el botón de envío.
        - Cambia el texto del botón durante el envío para indicar que se está creando la cuenta.

5. Formulario de login **(auth-login.js)**
    - El archivo auth-login.js se encarga del flujo de inicio de sesión:
        - Obtiene los valores de email y contraseña.
        - Llama a authInstance.login(email, password) para autenticar al usuario.
        - Si el login es exitoso, redirige al dashboard.
        - Si hay error, muestra un alert() con el mensaje del backend.
        - Cambia temporalmente el texto del botón durante la petición para indicar carga.

6. Comprobaciones
    - Una vez establecidas todas las funciones anteriores, se harán pruebas sobre el front para login de usuario
