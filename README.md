# 📚 Hub de Documentación & Especificaciones Técnicas — Turnos_ya

Bienvenido al centro principal de documentación, especificaciones de arquitectura y contratos de interfaz del ecosistema **Turnos_ya**. Este repositorio centraliza el **Project Brief**, la **Matriz de Roles**, los contratos **OpenAPI 3.0 (Domain-Driven Design)**, la colección de **Postman**, el **Sistema de Diseño Visual** y las especificaciones técnicas de cada subsistema.

---

## 📌 Tabla de Contenidos

1. [📋 Project Brief y Propuesta de Valor](#-1-project-brief)
2. [👥 Equipo de Trabajo y Roles](#-2-equipo-de-trabajo-y-definición-de-roles)
3. [🗓️ Cronograma e Hitos del Proyecto](#-3-agenda-de-trabajo-y-cronograma)
4. [🧭 Índice General del Ecosistema](#-4-índice-general-del-ecosistema)
5. [📑 Especificación OpenAPI 3.0 (Modular / DDD)](#-5-especificación-openapi-30-modular--ddd)
6. [🛠️ Herramientas y Scripts del Contrato](#-6-herramientas-y-scripts-para-la-especificación)
7. [🧪 Pruebas de Integración con Postman](#-7-pruebas-con-postman)

---

## 📋 1. Project Brief

### Visión y Misión
* **Visión:** Convertirse en la plataforma referente y de máxima agilidad para el descubrimiento, reserva y gestión de turnos en tiempo real, inspirada en la simplicidad e inmediatez de los modelos *on-demand*.
* **Misión:** Transformar y digitalizar la experiencia de reserva tanto para los prestadores de servicios como para los clientes, eliminando barreras de comunicación, esperas innecesarias y superposiciones de agenda mediante una plataforma accesible desde Web y dispositivos Móviles.

### Propuesta de Solución y Arquitectura de Seguridad
**Turnos_ya** ofrece una solución integral multiplataforma compuesta por una API RESTful centralizada, un portal Web SPA y una aplicación Móvil nativa:
* **Autonomía 24/7 y Comunidad:** Exploración de comercios verificados, seguimiento de favoritos (`❤️`), recepción de comunicados/promociones y aviso de días cerrados por feriado.
* **Bloqueo Temporal Transaccional (*Hold Tokens*):** Reserva temporal de 10 minutos que previene colisiones de reservas simultáneas (*overbooking*).
* **Seguridad de Grado Bancario:** Autenticación híbrida (Credenciales + Google OAuth 2.0), **2FA TOTP con Google Authenticator** (secretos y códigos de respaldo cifrados con **AES-256-GCM**), códigos OTP por email protegidos con **HMAC-SHA256**, cambio de contraseña sin fricción para cuentas OAuth y control remoto de dispositivos vinculados (`UserSession`).
* **Infraestructura de Correos y Tiempo Real:** Despacho de emails transaccionales mediante **Resend HTTP API (puerto 443)** con fallback automático a **Nodemailer SMTP**, notificaciones en vivo por **Server-Sent Events (SSE)** en Web y notificaciones locales/push en Móvil.
* **Gobernanza y Cuenta Raíz Inmutable (`turnosyapp@gmail.com`):** Jerarquía RBAC de triple capa donde la Cuenta Raíz posee inmunidad absoluta contra eliminación o cambio de rol y detenta la autoridad exclusiva para promover, degradar o dar de baja a administradores secundarios.

---

## 👥 2. Equipo de Trabajo y Definición de Roles

| Integrante | Rol Principal | Especialidad / Enfoque | Responsabilidades Clave |
| :--- | :--- | :--- | :--- |
| **Jeremías Collaud** | **Tech Lead & Backend Architect** | Arquitectura de Software, Backend RESTful, Seguridad & Cloud | • Diseño e implementación de la Arquitectura Limpia de 3 Capas en Node.js, Express y TypeScript.<br>• Modelado relacional en Prisma ORM + MySQL y caché multi-tier (`CacheService`).<br>• Seguridad avanzada: JWT, Google OAuth 2.0, 2FA TOTP (AES-256-GCM), sesiones remotas, jerarquía de Cuenta Raíz e integración con Resend HTTP API + SMTP.<br>• Co-diseño del contrato OpenAPI 3.0, suites Jest y despliegues en Render / Vercel / Aiven. |
| **Emmanuel Román** | **Frontend Web Lead & UI/UX Designer** | Desarrollo Web SPA & Sistema de Diseño Visual | • Arquitectura y desarrollo de la SPA en React 19 + TypeScript + Vite 8.<br>• Sistema de Diseño CSS nativo con layout de `1440px`, grilla de 4 columnas, Eje Izquierdo Unificado, View Transitions API y accesibilidad WCAG.<br>• Vistas de cliente, panel operativo de dueño (`Dashboard`) y Cockpit Ejecutivo de Administración (`SystemAdmin` de 7 módulos). |
| **Miqueas Müller** | **Mobile Lead, QA & Integración de Sistemas** | Desarrollo Móvil & Aseguramiento de Calidad (QA) | • Desarrollo del cliente móvil multiplataforma en React Native 0.88 + Expo SDK 58 (Android / iOS).<br>• Modo dual Cliente/Dueño (`MainTabs` ↔ `OwnerTabs`), geolocalización GPS (`expo-location`), asistente táctil con Hold Tokens y notificaciones.<br>• Aseguramiento de calidad (QA): Suites de pruebas con Vitest, validación Spectral Linter y colecciones Postman. |

---

## 🗓️ 3. Agenda de Trabajo y Cronograma

| Fase / Hito | Alcance y Entregables | Estado |
| :--- | :--- | :---: |
| **Fase 1: Análisis y Arquitectura Base** | Project Brief, Modelo Entidad-Relación, Stack Tecnológico y Design System. | **Completado** ✅ |
| **Fase 2: Contrato OpenAPI & Backend API** | Especificación OpenAPI 3.0 (DDD), Clean Architecture, Hold Tokens, 2FA TOTP, Sesiones, Resend API, SSE, Comunidad, Auditoría y suites Jest (87 tests). | **Completado** ✅ |
| **Fase 3: Frontend Web SPA & Cockpit Admin** | SPA React 19 + Vite 8, layout 1440px (4 columnas), View Transitions, SSE, Panel de Dueño, Cockpit Admin de 7 módulos y suites Vitest (27 tests). | **Completado** ✅ |
| **Fase 4: Frontend Mobile & Experiencia Dual** | App React Native 0.88 + Expo SDK 58, modo dual Cliente/Dueño, GPS, favoritos, 2FA y suites Vitest (30 tests). | **Completado** ✅ |
| **Fase 5: Despliegue Cloud & Auditoría Integral** | Despliegue en producción (Vercel + Render + Aiven + Resend), blindaje de Cuenta Raíz, pruebas de estrés y documentación final. | **Completado** ✅ |

---

## 🧭 4. Índice General del Ecosistema

| Módulo / Documento | Descripción Técnica | Enlace Directo |
| :--- | :--- | :--- |
| 🖥️ **Backend RESTful API** | Servidor Node.js + Express + Prisma + MySQL. Clean Architecture, DIP, JWT, Google OAuth, 2FA TOTP, Resend API + SMTP, SSE y suites Jest. | [backend-api.md](./backend-api.md) \| [Repositorio Backend](../Turnos_ya_backend-api-main/README.md) |
| 🌐 **Frontend Web SPA** | Aplicación Web en React 19 + Vite 8 + TypeScript. Layout 1440px, 4 columnas, SSE, Dashboard de Dueño y Cockpit Admin (`SystemAdmin`). | [frontend-web.md](./frontend-web.md) \| [Repositorio Web](../Turnos_ya_frontend_web-main/README.md) |
| 📱 **Frontend Mobile** | Aplicación móvil en React Native 0.88 + Expo SDK 58 + TypeScript. Modo dual Cliente/Dueño, GPS, Hold Tokens y seguridad 2FA. | [frontend-mobile.md](./frontend-mobile.md) \| [Repositorio Mobile](../Turnos_ya_frontend_mobile-main/README.md) |
| 🎨 **Design System** | Sistema de diseño visual propietario: variables CSS, paleta Mercado Libre, tipografía Plus Jakarta Sans y componentes modulares. | [design-system.md](./design-system.md) |
| 📑 **Contrato OpenAPI 3.0** | Especificación formal del contrato de la API RESTful particionado en dominios DDD. | [openapi.yaml](./openapi.yaml) |
| 🧪 **Colección Postman** | Colección exportada de endpoints con scripts automáticos para pruebas de integración. | [postman_collection.json](./postman_collection.json) |

---

## 📑 5. Especificación OpenAPI 3.0 (Modular / DDD)

* **`openapi.yaml`**: Punto de entrada principal (*entrypoint*) que consolida los componentes y módulos mediante referencias `$ref`.
* **`components/`**: Esquemas transversales reutilizables (`errors.yaml` bajo norma **RFC 7807**, `pagination.yaml` y `security.yaml`).
* **`modules/`**: Dominios de negocio (`auth`, `users`, `businesses`, `services`, `schedules`, `appointments`, `staff`, `reviews`).

---

## 🛠️ 6. Herramientas y Scripts para la Especificación

```bash
npm install                # Instalar herramientas (Redocly, Prism, Spectral)
npm run docs:preview       # Previsualización interactiva en http://localhost:8080
npm run mock               # Servidor Mock simulado en http://localhost:4040
npm run lint               # Auditoría de contrato OpenAPI con Spectral Linter
npm run generate:types     # Generación automática de tipos TypeScript
```

---

## 🧪 7. Pruebas con Postman

1. Abre **Postman** y selecciona **Import** -> [`postman_collection.json`](./postman_collection.json).
2. Ejecuta la petición **Login** dentro de la carpeta `Auth` para almacenar automáticamente el JWT en `{{authToken}}`.
3. Ejecuta las peticiones protegidas de comercios, bloqueos temporales (`Hold Appointment`), comunidad y administración.
