# Cómo desplegar en GitHub Pages

Esta guía te mostrará cómo publicar tu sitio web de ClutchPay Tutoriales en GitHub Pages.

## Pasos para desplegar

### 1. Crear un repositorio en GitHub

1. Ve a [GitHub](https://github.com) e inicia sesión
2. Haz clic en el botón **"+"** en la esquina superior derecha y selecciona **"New repository"**
3. Nombra tu repositorio (por ejemplo: `clutchpay-tutoriales` o `tutorial-completo`)
4. Marca el repositorio como **Public**
5. **NO** marques la opción "Add a README file" (ya tienes uno)
6. Haz clic en **"Create repository"**

### 2. Subir tus archivos al repositorio

Abre PowerShell o Git Bash en la carpeta `Tutoriales_completos` y ejecuta:

```bash
# Inicializar repositorio Git
git init

# Añadir todos los archivos
git add .

# Hacer commit
git commit -m "Initial commit: ClutchPay Tutoriales multipágina"

# Cambiar la rama a main (si es necesario)
git branch -M main

# Conectar con tu repositorio remoto (reemplaza TU-USUARIO y TU-REPOSITORIO)
git remote add origin https://github.com/TU-USUARIO/TU-REPOSITORIO.git

# Subir los archivos
git push -u origin main
```

### 3. Configurar GitHub Pages

1. Ve a tu repositorio en GitHub
2. Haz clic en **"Settings"** (Configuración)
3. En el menú lateral, haz clic en **"Pages"**
4. En **"Source"** (Fuente):
   - Selecciona la rama **"main"**
   - Selecciona la carpeta **"/docs"** (importante: no usar root)
5. Haz clic en **"Save"**

### 4. Acceder a tu sitio web

Después de unos minutos, tu sitio estará disponible en:

```
https://TU-USUARIO.github.io/TU-REPOSITORIO/
```

Por ejemplo: `https://nicolas.github.io/clutchpay-tutoriales/`

GitHub Pages te mostrará la URL exacta en la sección de Pages.

## Estructura de archivos

Tu repositorio tiene esta estructura organizada:

```
/
├── docs/                          # Sitio web (HTML/CSS)
│   ├── index.html
│   ├── styles.css
│   ├── capitulo1.html
│   ├── capitulo2.html
│   ├── ...
│   └── capitulo16.html
├── tutoriales/                    # Documentación Markdown
│   ├── Capitulo1_Instalacion.md
│   ├── Capitulo2_Creacion_de_base_de_datos.md
│   ├── ...
│   └── Capitulo16_Notificaciones_en_frontend.md
├── .nojekyll
├── .gitignore
├── README.md
└── GITHUB_PAGES.md (este archivo)
```

## Actualizar el sitio

Cada vez que quieras actualizar tu sitio:

```bash
# Añadir cambios
git add .

# Hacer commit
git commit -m "Descripción de los cambios"

# Subir cambios
git push origin main
```

Los cambios se reflejarán automáticamente en tu sitio web en unos minutos.

## Solución de problemas

### El sitio no se muestra correctamente

1. Verifica que el archivo `.nojekyll` esté en la raíz del repositorio
2. Asegúrate de que la carpeta `docs/` contenga `index.html`
3. En GitHub Pages Settings, verifica que esté configurado para usar la carpeta `/docs`
4. Revisa que todas las rutas en los archivos HTML sean relativas (sin `/` al inicio)

### Los estilos no se cargan

- Verifica que `styles.css` esté en la carpeta `docs/`
- Revisa que los enlaces en los archivos HTML sean: `<link rel="stylesheet" href="styles.css">`

### Los archivos Markdown (.md) no se muestran

Los archivos `.md` no se renderizan automáticamente en HTML. Son referencias para documentación. Los capítulos están en los archivos `.html`.

## Dominio personalizado (opcional)

Si quieres usar un dominio personalizado:

1. Ve a **Settings → Pages**
2. En **"Custom domain"**, ingresa tu dominio
3. Configura los registros DNS según las instrucciones de GitHub

## Más información

- [Documentación oficial de GitHub Pages](https://docs.github.com/es/pages)
- [Configurar un dominio personalizado](https://docs.github.com/es/pages/configuring-a-custom-domain-for-your-github-pages-site)
