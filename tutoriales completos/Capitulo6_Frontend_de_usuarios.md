# Configuración del Frontend para usuarios de ClutchPay

En este tutorial se añadirán los archivos de front necesarios para el manejo de perifles de usuario y contactos. Así como traducciones y hojas de estilo referentes a estas.

1. Estructura de archivos del frontend
    - i18n.js: Se añaden las traducciones del apartado de perfil de usuario.
    - main.html: Archivo de front para visualizar y manejar el perfil de usuario
    - style.css: Se corregirán y modificarán algunos detalles de los estilos.
    - dashboard_usuario.css: Archivo de estilo para el dashboard mostrado en main.html.
    - dashboard_usuario.js. Se encarga de la lógica de interacción con bacend por parte del usuario.

2. Correcciones  
    Se realizarán las correcciones necesarias sobre style.css para mejorar visibilidad y se actualizarán las traducciones de i18n.js

3. Archivo para visualizar dashboard  (main.html)
    - Se establecerá el archivo main al que se dirigen los usuarios una vez autenticados
    - Se listan los datos del usuario.
    - Se a ofrecen los formularios para añadir contactos o editar perfil.
    - Se muestra la lista sobre la que visualizar contactos.

4. Formulario de registro (dashboard_usuario.css)  
    Este archivo manejará el estilo referente a main.html.

5. Formulario de login (dashboard_usuario.js)  
    Archivo encargado de centralizar el manejo de transacciones con la base de datos, sus acciones serán las de:
    - Comprueba credenciales de usuario registrado.
    - Lista y filtra contactos.
    - Conectar con el backend par abuscar la lista de contactos así como editar perfil.
    - Permitir hacer log out.
