# 💳 ClutchPay - Guía Completa de Desarrollo

Esta página consiste en una guía estructurada para la realización de un proyecto con pasarela de pago usando PayPal y Stripe con Next.js. Basándose en el proyecto académico [ClutchPay](https://github.com/GCousido/ClutchPay).

## 📋 Tabla de Contenidos

- [Acerca del Proyecto](#-acerca-del-proyecto)
- [Estructura de la Guía](#-estructura-de-la-guía)
- [Guías por Capítulos](#-guías-por-capítulos)
  - [1. Configuración Inicial](#1-configuración-inicial)
  - [2. Autenticación y Usuarios](#2-autenticación-y-usuarios)
  - [3. Gestión de Facturas](#3-gestión-de-facturas)
  - [4. Sistema de Pagos](#4-sistema-de-pagos)
  - [5. Notificaciones](#5-notificaciones)
  - [6. Testing](#6-testing)
- [Cómo Usar Esta Guía](#-cómo-usar-esta-guía)

---

## 🎯 Acerca del Proyecto

ClutchPay es un proyecto educativo que demuestra la implementación de un sistema completo de pagos en línea utilizando tecnologías modernas. El proyecto integra:

- **Next.js** - Framework full-stack de React
- **PostgreSQL** - Base de datos relacional
- **Prisma ORM** - Gestión de base de datos
- **NextAuth** - Sistema de autenticación
- **Stripe & PayPal** - Pasarelas de pago
- **Docker** - Contenedorización
- **Vitest** - Testing

---

## 📚 Estructura de la Guía

Esta guía está organizada en 16 capítulos que te llevarán paso a paso desde la configuración inicial hasta la implementación completa de un sistema de pagos con notificaciones en tiempo real.

---

## 📖 Guías por Capítulos

### 1. Configuración Inicial

#### [Capítulo 1: Instalación y Configuración](./Mds/Capitulo1_Instalacion.md)
Instalación de herramientas de desarrollo necesarias:
- Visual Studio Code
- Node.js
- Docker Desktop
- Creación del proyecto Next.js

#### [Capítulo 2: Creación de Base de Datos](./Mds/Capitulo2_Creacion_de_base_de_datos.md)
Configuración de la base de datos PostgreSQL:
- Configuración de Docker y Docker Compose
- Implementación de Prisma ORM
- Definición del esquema de base de datos
- Migraciones y seeds

---

### 2. Autenticación y Usuarios

#### [Capítulo 3: API REST y Login](./Mds/Capitulo3_Api_rest_y_login.md)
Sistema de autenticación completo:
- Configuración de NextAuth
- Validación de datos con Zod
- Cifrado de contraseñas
- Gestión de sesiones y JWT

#### [Capítulo 4: Frontend de Login](./Mds/Capitulo4_Frontend_de_login.md)
Interfaz de usuario para autenticación:
- Formularios de login y registro
- Manejo de sesiones en el cliente
- Protección de rutas

#### [Capítulo 5: Backend de Usuarios](./Mds/Capitulo5_Backend_de_usuarios.md)
Gestión completa de usuarios:
- API endpoints para CRUD de usuarios
- Validaciones y seguridad
- Roles y permisos

#### [Capítulo 6: Frontend de Usuarios](./Mds/Capitulo6_Frontend_de_usuarios.md)
Interfaz para gestión de usuarios:
- Listado de usuarios
- Edición de perfiles
- Interfaz de administración

---

### 3. Gestión de Facturas

#### [Capítulo 9: Backend de Facturas](./Mds/Capitulo9_Backend_de_facturas.md)
Sistema backend para facturas:
- Modelos y esquemas de facturas
- API endpoints para gestión de facturas
- Lógica de negocio

#### [Capítulo 10: Frontend de Facturas](./Mds/Capitulo10_Frontend_de_facturas.md)
Interfaz de usuario para facturas:
- Creación de facturas
- Listado y visualización
- Edición y eliminación

---

### 4. Sistema de Pagos

#### [Capítulo 11: Backend de Pagos y Stripe Básico](./Mds/Capitulo11_Backend_de_pagos_y_stripe_basico.md)
Integración inicial con Stripe:
- Configuración de Stripe
- Creación de intents de pago
- Webhooks básicos

#### [Capítulo 12: Conexión con PayPal](./Mds/Capitulo12_Conexion_con_paypal.md)
Integración con PayPal:
- Configuración de PayPal SDK
- Procesamiento de pagos
- Gestión de transacciones

#### [Capítulo 13: Módulos de Front para Pagos](./Mds/Capitulo13_Modulos_de_front_para_pagos.md)
Componentes reutilizables para pagos:
- Módulos de UI para Stripe
- Módulos de UI para PayPal
- Componentes compartidos

#### [Capítulo 14: Frontend de Pagos](./Mds/Capitulo14_Frontend_de_pagos.md)
Interfaz completa de pagos:
- Flujo de checkout
- Selección de método de pago
- Confirmación y estados

---

### 5. Notificaciones

#### [Capítulo 15: Backend de Notificaciones](./Mds/Capitulo15_Backend_de_notificaciones.md)
Sistema de notificaciones backend:
- Arquitectura de notificaciones
- API de notificaciones
- Gestión de eventos

#### [Capítulo 16: Notificaciones en Frontend](./Mds/Capitulo16_Notificaciones_en_frontend.md)
Sistema de notificaciones en tiempo real:
- Implementación de notificaciones push
- Actualizaciones en tiempo real
- UI de notificaciones

---

### 6. Testing

#### [Capítulo 7: Testing usando Vitest](./Mds/Capitulo7_Testing_usando_vitest.md)
Pruebas automatizadas:
- Configuración de Vitest
- Tests unitarios
- Tests de integración
- Buenas prácticas de testing

---

## 🚀 Cómo Usar Esta Guía

1. **Sigue el orden**: Los capítulos están diseñados para seguirse secuencialmente, cada uno construye sobre el anterior.

2. **Requisitos previos**: Asegúrate de completar el Capítulo 1 antes de continuar con los demás.

3. **Práctica**: Cada capítulo incluye ejemplos de código y ejercicios prácticos.

4. **Referencia**: Puedes usar esta guía como referencia para consultar temas específicos.

---

## 🤝 Contribuciones

Este proyecto es educativo y está abierto a contribuciones. Si encuentras errores o tienes sugerencias, no dudes en:
- Abrir un issue
- Enviar un pull request
- Contactar con los mantenedores

---

## 📝 Licencia

Basado en el proyecto académico [ClutchPay](https://github.com/GCousido/ClutchPay).

---

## 📧 Contacto

Para preguntas o comentarios sobre esta guía, puedes contactar a través del repositorio en GitHub.

---

**¡Comienza tu viaje en el desarrollo de sistemas de pago!** 🚀
