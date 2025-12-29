# Configuración de Autenticación y Base de Datos en ClutchPay

En este tutorial se guiará paso a paso para configurar todo el sistema de autenticación y la conexión a la base de datos de ClutchPay.

1. Instalación de dependencias
    Comenzaremos instalando varias librerías esenciales:
    - NextAuth para manejar la autenticación.
    - Una librería de cifrado para proteger las contraseñas.
    - Zod junto a una librería de validación de teléfonos para asegurarnos de que los datos del usuario siempre sean correctos.

2. Creación del cliente de Prisma
    Después configuraremos el cliente de Prisma.
    Se exportará este cliente para usarlo desde cualquier parte de la aplicación sin problemas.

3. Validaciones de datos con Zod
    Antes de permitir que los usuarios se registren, es fundamental validar toda la información que envían.
    En esta sección veremos:
    - Cómo validar correos electrónicos.
    - Cómo asegurar contraseñas fuertes siguiendo varios criterios.
    - Cómo corregir, formatear y validar números de teléfono internacionales.
    - Y cómo preparar un validador completo para un usuario nuevo.

4. Configuración de NextAuth
    A continuación configuraremos el sistema de autenticación.
    - Se explicará cómo funciona el proveedor de credenciales, que permite iniciar sesión usando email y contraseña.
    - Cómo se verifica la existencia de un usuario.
    - Cómo se comprueba su contraseña comparando el hash almacenado.
    - Cómo se agregan datos personalizados dentro del token JWT.
    - Y cómo estos datos se exponen en la sesión disponible en el cliente.

5. Extender los tipos de NextAuth

    En este punto veremos cómo añadir propiedades personalizadas al usuario y a la sesión, para que todo esté correctamente tipado tanto en el backend como en el frontend.

6. Creación de rutas de autenticación
    Luego configuraremos las rutas de API que manejarán:
    - Todo el flujo de NextAuth (inicio de sesión, cierre de sesión, callbacks, etc).
    - Un endpoint independiente para registrar nuevos usuarios.

    Se explicará cómo funciona el proceso de registro completo:
    - Validar los datos enviados.
    - Verificar si el correo ya está registrado.
    - Cifrar la contraseña antes de guardarla.
    - Manejar errores comunes como duplicación de usuarios.
    - Responder al cliente sin exponer datos sensibles.

7. Variables de entorno
    Aquí prepararemos las variables esenciales para:
    - La conexión a la base de datos.
    - La URL de NextAuth.
    - Y la clave secreta para firmar los tokens JWT.

    También se mostrará cómo generar un secreto seguro para producción.

8. Inicialización de Prisma
    - Después se inicializará Prisma generando el cliente y creando las tablas en la base de datos.
    - Además, veremos cómo abrir Prisma Studio para visualizar los datos de manera gráfica.

9. Pruebas básicas con registro e inicio de sesión

    Para finalizar, se probará el flujo completo:
    - Registraremos un usuario nuevo.
    - Intentaremos iniciar sesión con él.
    - Y verificaremos que el backend devuelve una sesión válida.

    Con estas pruebas confirmaremos que todo está funcionando tal como se espera.
