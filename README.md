# 🏢 Sistema de Control de Asistencia — OliverTech

<div align="center">

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)

**Sistema completo de registro y control de asistencia con geolocalización, notificaciones push en tiempo real y panel administrativo web.**

[📡 Backend](#-backend) · [💻 Panel Admin](#-panel-administrativo) · [📱 App Móvil](#-aplicación-móvil)

</div>

---

## 📋 Descripción General

Sistema multiplataforma para la gestión de asistencia de personal, compuesto por tres componentes integrados:

- **API REST** con más de 70 endpoints organizados en 14 módulos
- **Panel administrativo web** con dashboard, reportes y gestión completa
- **App móvil** con registro de asistencia por geolocalización y notificaciones push

---

## ✨ Funcionalidades principales

| Funcionalidad | Descripción |
|---|---|
| 📍 Geofencing | Validación de ubicación GPS con radio configurable en metros |
| 🔔 Notificaciones push | Envío en tiempo real via Firebase Cloud Messaging |
| 👥 Gestión de grupos | Organización de empleados en grupos con inscripción masiva a eventos |
| 📅 Eventos | Registro de asistencia a eventos especiales con GPS |
| ⏰ Horarios | Turnos configurables con tolerancia de tardanza |
| 📊 Reportes | KPIs de asistencia, puntualidad y horas trabajadas |
| 🌙 Modo oscuro | Soporte en panel web y app móvil |
| 🔐 Autenticación JWT | Control de acceso por roles (Admin, Supervisor, Empleado) |

---

## 🏗️ Arquitectura del Sistema

```
┌─────────────────────────────────────────────────────┐
│                   CLIENTES                          │
│                                                     │
│   ┌──────────────────┐    ┌──────────────────┐     │
│   │  Panel Admin Web │    │   App Móvil       │     │
│   │  Angular 21      │    │   Flutter         │     │
│   └────────┬─────────┘    └────────┬──────────┘     │
└────────────┼─────────────────────┼───────────────────┘
             │                     │
             ▼                     ▼
┌─────────────────────────────────────────────────────┐
│                  API REST                           │
│             Node.js + Express                       │
│           JWT Auth · Sequelize ORM                  │
└──────────────────────┬──────────────────────────────┘
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
    ┌──────────┐ ┌──────────┐ ┌──────────┐
    │PostgreSQL│ │ Firebase │ │   OSM    │
    │    DB    │ │   FCM    │ │Nominatim │
    └──────────┘ └──────────┘ └──────────┘
```

---

## 📡 Backend

**Repositorio:** [`attendance-system-api`](https://github.com/Oliverzam/attendance-system-api)

### Stack
- **Runtime:** Node.js + Express.js
- **ORM:** Sequelize v6 + PostgreSQL
- **Auth:** JWT + bcryptjs
- **Notificaciones:** Firebase Admin SDK (FCM)
- **Contenedores:** Docker + docker-compose
- **Geolocalización:** Fórmula Haversine + OpenStreetMap Nominatim

### Módulos de la API

| Módulo | Endpoints | Descripción |
|---|---|---|
| Auth | `/api/auth` | Login con cédula o email |
| Empleados | `/api/empleados` | CRUD + roles y cargos |
| Asistencias | `/api/asistencias` | Entrada, salida, geofencing |
| Horarios | `/api/horarios` | Turnos y asignación |
| Grupos | `/api/grupos` | Organización de personal |
| Eventos | `/api/eventos` | Eventos especiales |
| Lugares | `/api/lugares` | Zonas de geofencing |
| Notificaciones | `/api/notificaciones` | Push broadcast e individual |
| Reportes | `/api/asistencias/mi-resumen` | KPIs del empleado |

### Instalación rápida

```bash
git clone https://github.com/Oliverzam/attendance-system-api
cd attendance-system-api
cp .env.example .env
# Configurar variables en .env
docker-compose up -d
```

---

## 💻 Panel Administrativo

**Repositorio:** [`attendance-system-admin`](https://github.com/Oliverzam/attendance-system-admin)

### Stack
- **Framework:** Angular 21 (standalone components)
- **UI:** Angular Material 21 + Material 3
- **Lenguaje:** TypeScript
- **Gráficas:** Chart.js
- **Mapas:** Leaflet.js + OpenStreetMap

### Módulos del panel

- 📊 **Dashboard** — métricas en tiempo real con gráficas semanales
- 👥 **Empleados** — CRUD con asignación de horario y lugar
- ✅ **Asistencias** — registro con filtros y exportación
- ⏰ **Horarios** — gestión de turnos con horario de almuerzo
- 👫 **Grupos** — organización y asignación masiva a eventos
- 📍 **Lugares** — zonas de geofencing con mapa interactivo
- 📅 **Eventos** — gestión con inscripción individual y por grupos
- 🔔 **Notificaciones** — broadcast e individual con historial
- 📈 **Reportes** — ranking de asistencia con barras de progreso

### Instalación

```bash
git clone https://github.com/Oliverzam/attendance-system-admin
cd attendance-system-admin
npm install
ng serve
```

---

## 📱 Aplicación Móvil

**Repositorio:** [`attendance-system-app`](https://github.com/Oliverzam/attendance-system-app)

### Stack
- **Framework:** Flutter (Dart)
- **Notificaciones:** Firebase Cloud Messaging
- **Mapas:** flutter_map + OpenStreetMap
- **Calendario:** table_calendar
- **Geolocalización:** geolocator

### Pantallas

| Pantalla | Descripción |
|---|---|
| 🔐 Login | Autenticación con cédula o email |
| 🏠 Home | Perfil, estado del día y accesos rápidos |
| ✅ Asistencia | Cronómetro, mapa GPS, flujo entrada/almuerzo/salida |
| 📅 Eventos | Calendario con eventos inscritos y registro de asistencia |
| 📊 Reportes | KPIs personales con barras de progreso |
| 🔔 Notificaciones | Historial con swipe para archivar |

### Instalación

```bash
git clone https://github.com/Oliverzam/attendance-system-app
cd attendance-system-app
flutter pub get
flutter run
```

---

## 👨‍💻 Autor

**Oliver Zamora Fajardo**
Ingeniero en Software — Universidad Técnica del Norte

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Oliver%20Zamora-blue?style=flat&logo=linkedin)](https://linkedin.com/in/oliver-zamora-fajardo)
[![GitHub](https://img.shields.io/badge/GitHub-Oliverzam-black?style=flat&logo=github)](https://github.com/Oliverzam)
📧 oliverzafa05@gmail.com

---

<div align="center">
<strong>OliverTech © 2026</strong>
</div>
