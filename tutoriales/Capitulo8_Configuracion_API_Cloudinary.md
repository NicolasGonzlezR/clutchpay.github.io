# Implementación de Cloudinary con usuarios

En este tutorial se describe el proceso para poder implementar los archivos relacionados con la configuración de pruebas, la gestión de imágenes y la validación de usuarios en el proyecto.

## 1. Estructura de archivos de pruebas y configuración

- **src/libs/cloudinary.ts**: archivo que define la configuración global de cloudinary.

- **src/libs/validations/user.ts**: este archivo anteriormente definido se deberá de actualizarse para incluir la validación de imágenes codificadas.

- **src/app/api/users/[id]/route.ts**: este archivo anteriormente definido se deberá de actualizar para interactuar con cloudinary en el momento que gestione imágenes.

- **tests/libs/cloudinary.test.ts**: tests relacionados con el uso e implementación de cloudinary.

## 2. `src/libs/cloudinary.ts`

Este archivo contiene funciones para gestionar imágenes en Cloudinary, un servicio de almacenamiento en la nube. Las funciones permiten cargar, eliminar y extraer la información relacionada con las imágenes, como sus URLs y `public_id`, lo que facilita la manipulación de archivos multimedia.

### Funciones

  Subir una imagen codificada  a Cloudinary. Permite también especificar una carpeta dentro de Cloudinary y realiza transformaciones automáticas en la imagen antes de su carga, como la redimensión y la mejora de la calidad.  
  Eliminar una imagen de Cloudinary usando su `public_id`.  
  Extraer el `public_id` de una URL de Cloudinary.  
  Subir un archivo PDF codificado a Cloudinary como un recurso bruto (`raw`).  
  Eliminar un archivo PDF de Cloudinary usando su `public_id`.  

## 3. `src/libs/validations/user.ts`

Este archivo se va a retocar para implementar las validaciones necesarias para probar el formato correcto de imagen

## 4. `src/app/api/users/[id]/route.ts`

Este archivo se modifica para interactuar con cloudinary y poder enviar y modificar archivos

## 5. `tests/libs/cloudinary.test.ts`

Este archivo contiene las pruebas unitarias para las funciones relacionadas con Cloudinary, utilizando `vitest` para mockear las llamadas a la API de Cloudinary y asegurar que las funciones se comporten correctamente en diferentes escenarios.

### Pruebas

- **uploadImage**  
  Se prueban tres casos:
  - Subida exitosa de una imagen codificada.
  - Subida exitosa con una carpeta personalizada.
  - Error al intentar subir una imagen.

- **deleteImage**  
  Se prueban tres casos:
  - Eliminación exitosa de una imagen.
  - Caso donde la imagen no se encuentra en Cloudinary.
  - Error al intentar eliminar una imagen.

- **extractPublicId**  
  Se prueban casos para extraer el `public_id` de una URL estándar de Cloudinary y otros casos con URL mal formadas o inválidas.

---
