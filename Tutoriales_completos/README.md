# clutchpay.github.io
Esta página consiste en una guía estructurada para la realización de un proyecto con pasarela de pago PayPal usando Stripe y Next. Basándose en el proyecto académico https://github.com/GCousido/ClutchPay.
# ClutchPay - Guía de Desarrollo Completa

Bienvenido a la documentación completa de **ClutchPay**, un sistema de gestión de facturas y pagos desarrollado con Next.js, PostgreSQL, Prisma, Stripe y PayPal.

Esta guía te llevará paso a paso desde la instalación inicial hasta la implementación completa de un sistema de facturación con pagos, notificaciones y más.

---

## 📋 Tabla de Contenidos

### **Parte I: Configuración Inicial**
- [Capítulo 1: Instalación y Configuración](#capítulo-1-instalación-y-configuración)
- [Capítulo 2: Creación de Base de Datos](#capítulo-2-creación-de-base-de-datos)

### **Parte II: Autenticación**
- [Capítulo 3: API REST y Login](#capítulo-3-api-rest-y-login)
- [Capítulo 4: Frontend de Login](#capítulo-4-frontend-de-login)

### **Parte III: Gestión de Usuarios**
- [Capítulo 5: Backend de Usuarios](#capítulo-5-backend-de-usuarios)
- [Capítulo 6: Frontend de Usuarios](#capítulo-6-frontend-de-usuarios)

### **Parte IV: Testing**
- [Capítulo 7: Testing usando Vitest](#capítulo-7-testing-usando-vitest)

### **Parte V: Cloudinary**
- [Capítulo 8: Configuración API Cloudinary](#capítulo-8-configuración-api-cloudinary)


### **Parte VI: Sistema de Facturas**
- [Capítulo 9: Backend de Facturas](#capítulo-9-backend-de-facturas)
- [Capítulo 10: Frontend de Facturas](#capítulo-10-frontend-de-facturas)

### **Parte VII: Sistema de Pagos**
- [Capítulo 11: Backend de Pagos y Stripe Básico](#capítulo-11-backend-de-pagos-y-stripe-básico)
- [Capítulo 12: Conexión con PayPal](#capítulo-12-conexión-con-paypal)
- [Capítulo 13: Módulos de Front para Pagos](#capítulo-13-módulos-de-front-para-pagos)
- [Capítulo 14: Frontend de Pagos](#capítulo-14-frontend-de-pagos)

### **Parte VIII: Sistema de Notificaciones**
- [Capítulo 15: Backend de Notificaciones](#capítulo-15-backend-de-notificaciones)
- [Capítulo 16: Notificaciones en Frontend](#capítulo-16-notificaciones-en-frontend)

---

## Capítulo 1: Instalación y Configuración

[Ver documentación completa →](Mds/Capitulo1_Instalacion.md)

### 📖 Contenido
En este capítulo inicial aprenderás a configurar tu entorno de desarrollo en Windows y Linux.

### 🎯 Objetivos
- Instalar Visual Studio Code
- Configurar Node.js y npm
- Instalar y configurar Docker Desktop
- Crear un nuevo proyecto Next.js

### 🛠️ Herramientas
- Visual Studio Code
- Node.js (versión LTS)
- Docker Desktop
- Next.js

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_1-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1cZAgeoiAKJmvFhJjj4KHtgBh5W1XCvaK/view)
---

## Capítulo 2: Creación de Base de Datos

[Ver documentación completa →](Mds/Capitulo2_Creacion_de_base_de_datos.md)

### 📖 Contenido
Configuración de PostgreSQL con Docker y Prisma ORM para gestionar la base de datos.

### 🎯 Objetivos
- Configurar PostgreSQL usando Docker Compose
- Implementar Prisma ORM
- Diseñar el esquema de base de datos
- Ejecutar migraciones

### 🛠️ Tecnologías
- PostgreSQL 15
- Docker & Docker Compose
- Prisma ORM
- Variables de entorno

### 📊 Modelos principales
- Usuario (User)
- Factura (Invoice)
- Pago (Payment)
- Notificación (Notification)

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_2-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/17o8G4ifomvbx7ssnYtdQdjmexg0ZQOGd/view)
---

## Capítulo 3: API REST y Login

[Ver documentación completa →](Mds/Capitulo3_Api_rest_y_login.md)

### 📖 Contenido
Implementación del sistema completo de autenticación con NextAuth y validaciones.

### 🎯 Objetivos
- Configurar NextAuth.js para autenticación
- Implementar validaciones con Zod
- Crear endpoints de registro e inicio de sesión
- Implementar cifrado de contraseñas
- Configurar JWT y sesiones

### 🔐 Características
- Autenticación con email y contraseña
- Validación de datos con Zod
- Cifrado de contraseñas con bcrypt
- Tokens JWT personalizados
- Protección de rutas API

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_3-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1BTh_bb3FTOXluSeu1g4q2U1_BQKS57rX/view)
---

## Capítulo 4: Frontend de Login

[Ver documentación completa →](Mds/Capitulo4_Frontend_de_login.md)

### 📖 Contenido
Desarrollo del frontend para autenticación con formularios, validaciones y estilos.

### 🎯 Objetivos
- Crear formularios de registro e inicio de sesión
- Implementar validaciones en tiempo real
- Integrar con la API de autenticación
- Aplicar estilos y diseño responsive

### 💻 Archivos principales
- `validaciones.js` - Validaciones del lado del cliente
- `auth.js` - Clase para comunicación con API
- `auth-register.js` - Lógica del formulario de registro
- `auth-login.js` - Lógica del formulario de login
- `style.css` - Estilos globales

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_4-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1Pc8kiXbZaYcWCwVzkARTC65ulXRxo_YJ/view)
---

## Capítulo 5: Backend de Usuarios

[Ver documentación completa →](Mds/Capitulo5_Backend_de_usuarios.md)

### 📖 Contenido
Desarrollo de endpoints para gestión de perfiles y contactos de usuarios.

### 🎯 Objetivos
- Crear endpoints RESTful para usuarios
- Implementar sistema de contactos
- Añadir validaciones y autorización
- Gestionar perfiles de usuario

### 📡 Endpoints
- `GET /api/users` - Listar usuarios (paginado)
- `GET /api/users/[id]` - Obtener perfil
- `PUT /api/users/[id]` - Actualizar perfil
- `GET /api/users/[id]/contacts` - Listar contactos
- `POST /api/users/[id]/contacts` - Añadir contacto

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_5-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1pai1iow8CWJIYfomDnTJhaFKPRc5dq4g/view)
---

## Capítulo 6: Frontend de Usuarios

[Ver documentación completa →](Mds/Capitulo6_Frontend_de_usuarios.md)

### 📖 Contenido
Implementación del dashboard de usuario con gestión de perfil y contactos.

### 🎯 Objetivos
- Crear dashboard de usuario
- Implementar edición de perfil
- Desarrollar sistema de contactos
- Añadir traducciones (i18n)

### 💻 Archivos principales
- `main.html` - Página del dashboard
- `dashboard_usuario.js` - Lógica de interacción
- `dashboard_usuario.css` - Estilos del dashboard
- `i18n.js` - Sistema de traducciones

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_6-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1h3pcOMqv2crFC6WtW0MqGpBwOUpc_lJb/view)
---

## Capítulo 7: Testing usando Vitest

[Ver documentación completa →](Mds/Capitulo7_Testing_usando_vitest.md)

### 📖 Contenido
Implementación de pruebas automatizadas para garantizar la calidad del código.

### 🎯 Objetivos
- Configurar Vitest para testing
- Crear pruebas unitarias e integración
- Testear validaciones y autenticación
- Implementar pruebas de API

### 🧪 Archivos de pruebas
- `vitest.config.mts` - Configuración de Vitest
- `tests/setup.ts` - Setup global
- `tests/libs/auth.test.ts` - Pruebas de autenticación
- `tests/libs/validations/` - Pruebas de validaciones
- `tests/api/users/` - Pruebas de endpoints de usuarios

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_7-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1ZpAc6rTvYDtspJ2K7KzrqjDR_ePoguqB/view)
---

## Capítulo 8: Configuración API Cloudinary

[Ver documentación completa →](Capitulo8_Configuracion_API_Cloudinary.md)

### 📖 Contenido
Implementación de Cloudinary para la gestión de archivos multimedia en el proyecto.

### 🎯 Objetivos
- Configurar Cloudinary para almacenamiento de archivos
- Implementar funciones para subir y eliminar imágenes
- Validar imágenes codificadas en base64
- Integrar Cloudinary con perfiles de usuario
- Crear pruebas para las funciones de Cloudinary

### 🛠️ Tecnologías
- Cloudinary - Almacenamiento en la nube
- Base64 encoding - Para imágenes
- Transformaciones automáticas - Redimensión y optimización

### 📁 Archivos principales
- `src/libs/cloudinary.ts` - Configuración y funciones de Cloudinary
- `src/libs/validations/user.ts` - Validación de imágenes
- `src/app/api/users/[id]/route.ts` - Integración con API de usuarios
- `tests/libs/cloudinary.test.ts` - Pruebas unitarias

### ⚙️ Funcionalidades
- **uploadImage**: Subir imagen codificada con transformaciones automáticas
- **deleteImage**: Eliminar imagen usando public_id
- **extractPublicId**: Extraer public_id de URL de Cloudinary
- **uploadPDF**: Subir archivos PDF como recursos raw
- **deletePDF**: Eliminar archivos PDF

### 🧪 Pruebas
- Subida exitosa de imágenes
- Eliminación de imágenes
- Extracción de public_id
- Manejo de errores
- URLs mal formadas

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_8-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1MwWlUK_pl6q0oXbP_nZHsaJsYGOUQA-9/view)
---


## Capítulo 9: Backend de Facturas

[Ver documentación completa →](Mds/Capitulo9_Backend_de_facturas.md)

### 📖 Contenido
Implementación completa del sistema de gestión de facturas con almacenamiento en Cloudinary.

### 🎯 Objetivos
- Crear modelo de factura en Prisma
- Implementar CRUD de facturas
- Integrar Cloudinary para PDFs
- Validar datos con Zod

### 📡 Endpoints
- `GET /api/invoices` - Listar facturas (con filtros)
- `POST /api/invoices` - Crear factura
- `GET /api/invoices/[id]` - Obtener factura
- `PUT /api/invoices/[id]` - Actualizar factura
- `DELETE /api/invoices/[id]` - Eliminar factura

### 📋 Estados de factura
- `PENDING` - Pendiente
- `PAID` - Pagada
- `OVERDUE` - Vencida
- `CANCELED` - Cancelada

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_9-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1yLY1gJ5-hidYi6tph8oSwSJVF0UphdNo/view)
---

## Capítulo 10: Frontend de Facturas

[Ver documentación completa →](Mds/Capitulo10_Frontend_de_facturas.md)

### 📖 Contenido
Desarrollo de la interfaz de usuario para gestión de facturas con tema claro/oscuro.

### 🎯 Objetivos
- Crear interfaz modular para facturas
- Implementar listado con filtros
- Desarrollar formularios de creación/edición
- Añadir tema claro/oscuro
- Integrar sistema de notificaciones

### 💻 Módulos principales
- `dashboard/core.js` - Núcleo del dashboard
- `dashboard/invoices.js` - Gestión de facturas
- `dashboard/profile.js` - Gestión de perfil
- `dashboard/contacts.js` - Gestión de contactos
- `theme.js` - Manejo de temas
- `notifications.js` - Sistema de toasts

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_10-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/151mDDEO7EZVTxDuPrB5VJaKwplLPzhFu/view)
---

## Capítulo 11: Backend de Pagos y Stripe Básico

[Ver documentación completa →](Mds/Capitulo11_Backend_de_pagos_y_stripe_basico.md)

### 📖 Contenido
Integración con Stripe para procesar pagos de facturas de forma segura.

### 🎯 Objetivos
- Integrar Stripe Checkout
- Crear sesiones de pago
- Implementar webhooks de Stripe
- Gestionar estados de pago

### 📡 Endpoints
- `GET /api/payments` - Listar pagos (con filtros)
- `GET /api/payments/[id]` - Obtener pago
- `POST /api/payments/stripe/checkout` - Crear sesión de pago
- `GET /api/payments/stripe/session/[sessionId]` - Estado de sesión
- `POST /api/payments/stripe/webhook` - Webhook de Stripe

### 💳 Características
- Pagos seguros con Stripe
- Soporte para múltiples monedas
- Manejo de pagos asíncronos
- Validación de webhooks

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_11-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1ve8-hBIT_dlMfSAkqUxUfR04qXxBN4FC/view)
---

## Capítulo 12: Conexión con PayPal

[Ver documentación completa →](Mds/Capitulo12_Conexion_con_paypal.md)

### 📖 Contenido
Implementación del flujo completo de pagos con distribución de fondos vía PayPal Payouts.

### 🎯 Objetivos
- Integrar PayPal Payouts
- Generar recibos en PDF
- Procesar webhooks de Stripe
- Implementar distribución de fondos

### 💰 Flujo de pago
1. Usuario crea sesión de pago con Stripe
2. Stripe procesa el pago
3. Webhook notifica el pago exitoso
4. Sistema genera recibo en PDF
5. Se transfieren fondos al emisor vía PayPal
6. Se actualiza el estado de la factura

### 📄 Características
- Generación de recibos con PDFKit
- Almacenamiento en Cloudinary
- PayPal Payouts para emisores
- Tolerancia a fallos y reintentos

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_12-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1gRXScOlgj24rNUSBcQ3MHsJkxaLG4OFi/view)
---

## Capítulo 13: Módulos de Front para Pagos

[Ver documentación completa →](Mds/Capitulo13_Modulos_de_front_para_pagos.md)

### 📖 Contenido
Desarrollo de la clase PaymentManager para gestionar pagos desde el frontend.

### 🎯 Objetivos
- Crear módulo de gestión de pagos
- Implementar integración con Stripe Checkout
- Desarrollar consulta de estados de pago
- Añadir listado de pagos

### 💻 Archivos principales
- `payments.js` - Clase PaymentManager
- `dashboard/payments.js` - Módulo de pagos del dashboard

### 🔧 Métodos de PaymentManager
- `createCheckoutSession()` - Crear sesión de pago
- `getSessionStatus()` - Consultar estado de sesión
- `getPayments()` - Listar pagos del usuario
- `getPaymentById()` - Obtener detalle de pago

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_13-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1qky9tmaBxlbVod3NX29vL4LKCKkYpOmf/view)
---

## Capítulo 14: Frontend de Pagos

[Ver documentación completa →](Mds/Capitulo14_Frontend_de_pagos.md)

### 📖 Contenido
Integración completa del sistema de pagos en la interfaz de usuario.

### 🎯 Objetivos
- Integrar botones de pago en facturas
- Implementar redirección a Stripe Checkout
- Manejar callbacks de pago
- Mostrar recibos de pago
- Listar historial de pagos

### 🔄 Flujo de pago
1. Usuario selecciona "Pagar factura"
2. Se crea sesión de Stripe
3. Redirección a Stripe Checkout
4. Usuario completa el pago
5. Retorno a la app con estado
6. Actualización de UI y notificación

### 📊 Visualización
- Lista de pagos realizados/recibidos
- Filtros y ordenamiento
- Descarga de recibos
- Estados visuales de pago

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_14-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1EwVtZDg7ltEgO4Tw2Q83U4XuEqvJwJJT/view)
---

## Capítulo 15: Backend de Notificaciones

[Ver documentación completa →](Mds/Capitulo15_Backend_de_notificaciones.md)

### 📖 Contenido
Sistema completo de notificaciones in-app y por email.

### 🎯 Objetivos
- Crear sistema de notificaciones
- Implementar envío de emails
- Desarrollar plantillas de notificación
- Añadir notificaciones automáticas

### 📡 Endpoints
- `GET /api/notifications` - Listar notificaciones
- `PUT /api/notifications/mark-read` - Marcar como leídas
- `DELETE /api/notifications` - Eliminar múltiples
- `GET /api/notifications/[id]` - Obtener notificación
- `PUT /api/notifications/[id]` - Actualizar notificación
- `DELETE /api/notifications/[id]` - Eliminar notificación

### 🔔 Tipos de notificación
- Factura emitida
- Pago recibido
- Factura cancelada
- Pago próximo a vencer
- Pago vencido

### 📧 Características
- Notificaciones in-app
- Emails con plantillas React
- Scheduler para notificaciones automáticas
- Limpieza de notificaciones antiguas

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_15-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/14llUQ7yHvnbKTSxrDJlThQ12WHn2_0FK/view)
---

## Capítulo 16: Notificaciones en Frontend

[Ver documentación completa →](Mds/Capitulo16_Notificaciones_en_frontend.md)

### 📖 Contenido
Implementación del sistema de notificaciones en la interfaz de usuario.

### 🎯 Objetivos
- Crear módulo de notificaciones internas
- Implementar modal de notificaciones
- Añadir badge con contador
- Integrar con eventos del sistema

### 💻 Archivos principales
- `internal-notifications.js` - Sistema de notificaciones
- `dashboard-usuario.js` - Integración con dashboard
- `main.html` - UI de notificaciones

### 🔔 Funcionalidades
- Visualización en tiempo real
- Contador de no leídas
- Marcar como leídas
- Eliminar notificaciones
- Acceso desde modal

### 🔗 Integración
- Notificaciones al crear facturas
- Notificaciones al cancelar facturas
- Notificaciones de pagos
- Sistema de eventos global

### 🎥 Video Tutorial
[![Ver Video](https://img.shields.io/badge/▶️_Ver_Video-Tutorial_Capítulo_16-red?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1wc_ONUymg6GEmPO-fZ-ECPmVvMNvpKsp/view)
---

## 🚀 Tecnologías Utilizadas

### Backend
- **Next.js** - Framework full-stack
- **PostgreSQL** - Base de datos
- **Prisma ORM** - Gestión de BD
- **NextAuth.js** - Autenticación
- **Zod** - Validación de datos
- **bcryptjs** - Cifrado de contraseñas

### Frontend
- **HTML5 / CSS3** - Estructura y estilos
- **JavaScript ES6+** - Lógica del cliente
- **Sistema modular** - Arquitectura escalable
- **i18n** - Internacionalización

### Servicios externos
- **Stripe** - Procesamiento de pagos
- **PayPal** - Distribución de fondos
- **Cloudinary** - Almacenamiento de archivos
- **Resend** - Envío de emails

### Testing
- **Vitest** - Framework de pruebas
- **@testing-library** - Testing utilities

### DevOps
- **Docker** - Contenedorización
- **Docker Compose** - Orquestación

---

## 📝 Convenciones del Proyecto

### Estructura de directorios
```
proyecto/
├── src/
│   ├── app/
│   │   └── api/          # Endpoints de API
│   └── libs/             # Librerías y utilidades
│       ├── validations/  # Schemas de validación
│       └── ...
├── public/
│   ├── JS/               # JavaScript del cliente
│   │   └── dashboard/    # Módulos del dashboard
│   └── CSS/              # Hojas de estilo
├── prisma/
│   └── schema.prisma     # Esquema de BD
├── tests/                # Pruebas automatizadas
└── docker/               # Configuración Docker
```

### Nomenclatura
- **Archivos**: kebab-case (`user-profile.ts`)
- **Clases**: PascalCase (`PaymentManager`)
- **Funciones**: camelCase (`createInvoice`)
- **Constantes**: UPPER_SNAKE_CASE (`API_BASE_URL`)

---

## 🤝 Contribuciones

Este proyecto es educativo y está diseñado para aprender desarrollo full-stack moderno. Siéntete libre de:
- Reportar problemas
- Sugerir mejoras
- Compartir tu experiencia
- Adaptar el código a tus necesidades

---

## 📄 Licencia

Este material es de uso educativo. Consulta los términos de las dependencias utilizadas.

---

## 📚 Recursos Adicionales

### Documentación oficial
- [Next.js](https://nextjs.org/docs)
- [Prisma](https://www.prisma.io/docs)
- [NextAuth.js](https://next-auth.js.org)
- [Stripe](https://stripe.com/docs)
- [PayPal](https://developer.paypal.com)

### Herramientas
- [VS Code](https://code.visualstudio.com)
- [Docker](https://docs.docker.com)
- [Vitest](https://vitest.dev)

---
