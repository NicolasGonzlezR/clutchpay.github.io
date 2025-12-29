# Guía de Instalación y Configuración de Herramientas para Desarrollo

En este tutorial se instalarán y configurarán las herramientas necesarias para el entorno de desarrollo en **Windows** y **Linux**. Cubriremos la instalación de **Visual Studio Code**, **Node.js**, **Docker Desktop** y la creación de un nuevo proyecto Next.js usando **npx**.

---

## 1. Instalación de Visual Studio Code

### En Windows

1. **Descargar Visual Studio Code**:
   - Visita la [página oficial de Visual Studio Code](https://code.visualstudio.com/).
   - Haz clic en el botón **"Download for Windows"**.

2. **Instalar Visual Studio Code**:
   - Abre el archivo `.exe` descargado.
   - Durante la instalación, asegúrate de marcar las opciones:
     - **"Add to PATH"** (esto permitirá ejecutar VS Code desde la terminal).
     - **"Register code as an editor for supported file types"** (esto facilita abrir archivos directamente desde el explorador de Windows).
     - **"Add Open with Code to context menu"** (esto agrega la opción de abrir con VS Code en el menú contextual).

3. **Lanzar Visual Studio Code**:
   - Una vez completada la instalación, abre **Visual Studio Code** desde el menú de inicio o ejecutando `code` en la terminal.

### En Linux (Ubuntu/Debian)

1. **Instalar Visual Studio Code**:
   - Abre una terminal y ejecuta los siguientes comandos:

   ```bash
   sudo apt update
   sudo apt install software-properties-common apt-transport-https wget
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
   sudo apt update
   sudo apt install code
   ```

---

## 2. Instalación de Node.js

### En Windows

1. **Descargar Node.js**:
   - Visita la [página oficial de Node.js](https://nodejs.org/).
   - Descarga la versión **LTS** (Long-Term Support) para Windows.

2. **Instalar Node.js**:
   - Abre el archivo `.msi` descargado y sigue las instrucciones del instalador.

3. **Verificar instalación**:
   - Una vez que la instalación haya terminado, abre una terminal (cmd o PowerShell) y verifica que Node.js y npm (Node Package Manager) se han instalado correctamente:

   ```bash
   node -v
   npm -v
   ```
   
   Deberías ver la versión de Node.js y npm instalados.

### En Linux (Ubuntu/Debian)

1. **Instalar Node.js**:
   - Abre una terminal y ejecuta los siguientes comandos:

   ```bash
   sudo apt update
   sudo apt install nodejs npm
   ```

2. **Verificar instalación**:
   - Verifica que Node.js y npm se han instalado correctamente:

   ```bash
   node -v
   npm -v
   ```
   
   Deberías ver la versión instalada de Node.js y npm.

---

## 3. Instalación de Docker Desktop

### En Windows

1. **Descargar Docker Desktop**:
   - Visita la [página oficial de Docker](https://www.docker.com/products/docker-desktop).
   - Haz clic en el botón de descarga para Windows.

2. **Instalar Docker Desktop**:
   - Abre el archivo `.exe` descargado y sigue las instrucciones en el instalador.
   - Asegúrate de habilitar la opción **"Enable WSL 2"** si se te solicita.

3. **Configurar Docker Desktop**:
   - Una vez instalado, abre Docker Desktop. Docker necesitará habilitar el **Windows Subsystem for Linux 2 (WSL 2)**, lo que permite ejecutar Docker en un entorno de Linux dentro de Windows.
   - Si no tienes WSL 2, Docker te guiará en su instalación.

4. **Verificar instalación**:
   - Abre una terminal de PowerShell o cmd y ejecuta:

   ```bash
   docker --version
   ```
   
   Verifica que Docker esté funcionando correctamente.

### En Linux (Ubuntu/Debian)

1. **Instalar Docker**:
   - Abre una terminal y ejecuta los siguientes comandos:

   ```bash
   sudo apt update
   sudo apt install docker.io
   ```

2. **Habilitar Docker para iniciar al arrancar**:
   - Ejecuta el siguiente comando para habilitar Docker al iniciar el sistema:

   ```bash
   sudo systemctl enable --now docker
   ```

3. **Verificar instalación**:
   - Verifica que Docker está instalado correctamente:

   ```bash
   docker --version
   ```
   
   También puedes probar ejecutando un contenedor de prueba:

   ```bash
   sudo docker run hello-world
   ```

---

## 4. Crear un Nuevo Proyecto con Next.js

### Crear un Proyecto de Next.js con npx create-next-app

1. **Abrir Visual Studio Code**:
   - Abre una terminal en Visual Studio Code presionando `Ctrl + \`` (la tecla de la tilde).

2. **Crear un Nuevo Proyecto con Next.js**:
   - En la terminal de VS Code, ejecuta el siguiente comando para crear un nuevo proyecto usando npx (se recomienda usar npx para obtener siempre la última versión):

   ```bash
   npx create-next-app@latest my-next-project
   ```
   
   Esto descargará e instalará la plantilla de Next.js más reciente y creará una carpeta llamada `my-next-project`.

3. **Ingresar a la Carpeta del Proyecto**:
   - Una vez que el proyecto esté creado, ingresa a la carpeta del proyecto:

   ```bash
   cd my-next-project
   ```

4. **Iniciar el Servidor de Desarrollo**:
   - Para verificar que todo está funcionando correctamente, ejecuta el siguiente comando para iniciar el servidor de desarrollo:

   ```bash
   npm run dev
   ```

5. **Ver el Proyecto en el Navegador**:
   - Abre tu navegador y accede a [http://localhost:3000](http://localhost:3000). Deberías ver la página de inicio predeterminada de Next.js.