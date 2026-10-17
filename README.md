<!-- prettier-ignore -->
<div align="center">

<img src="./src/assets/nuevo%20logo.jpg" alt="TATSoft" height="96" />

# TATSoft — Sistema de Gestión Empresarial

[![React](https://img.shields.io/badge/React-18.3.1-61DAFB?style=flat-square&logo=react&logoColor=white)](https://react.dev)
[![Vite](https://img.shields.io/badge/Vite-5.4.10-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vitejs.dev)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3.4.14-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-3c873a?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org)
[![Azure SWA](https://img.shields.io/badge/Azure-Static%20Web%20Apps-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/products/app-service/static)

Aplicación web para la gestión integral de operaciones comerciales: preventas, ventas, devoluciones, inventario, zonas geográficas, clientes, productos y usuarios.

[Primeros pasos](#primeros-pasos) • [Arquitectura](#arquitectura) • [Módulos](#módulos-funcionales) • [Microservicios](#microservicios) • [Estado del despliegue](#estado-del-despliegue) • [Seguridad](#seguridad-y-autenticación)

</div>

## Descripción general

**TATSoft** es el frontend de una plataforma empresarial construida con **React + Vite** y estilizada con **Tailwind CSS**. La interfaz sigue el patrón **Atomic Design** y consume una infraestructura de **microservicios** desplegada en Azure, con control de acceso basado en roles (RBAC) para administradores y colaboradores.

> [!IMPORTANT]
> El proyecto se encuentra en **pausa**: las cuentas de los servicios en Azure están suspendidas por falta de pago de los créditos. Consulta la sección [Estado del despliegue](#estado-del-despliegue) antes de intentar desplegar o conectar con las APIs.

## Primeros pasos

### Requisitos previos

- [Node.js](https://nodejs.org/en/download) 18.x o superior
- npm 9.x o superior
- Git

### Instalación

```bash
# 1. Clonar el repositorio
git clone https://github.com/JhoamSebastianMunoz/tatsoft-frontend.git
cd tatsoft-frontend

# 2. Instalar dependencias
npm install

# 3. Iniciar el servidor de desarrollo
npm run dev
```

El servidor se inicia en `http://localhost:5173`. Los proxies definidos en `vite.config.js` redirigen automáticamente las llamadas `/auth-api`, `/users-api`, `/areas-api`, `/products-api` y `/presales-api` hacia los microservicios correspondientes.

### Scripts disponibles

| Comando | Descripción |
| --- | --- |
| `npm run dev` | Inicia el servidor de desarrollo con Vite. |
| `npm run build` | Genera el bundle de producción en `dist/`. |
| `npm run preview` | Previsualiza localmente la build de producción. |
| `npm run lint` | Ejecuta ESLint sobre el código fuente. |

## Stack tecnológico

| Área | Tecnologías |
| --- | --- |
| **Core** | React 18.3.1, React DOM 18.3.1, Vite 5.4.10 |
| **Routing y HTTP** | React Router DOM 7.1.5, Axios 1.7.9 |
| **Estilos e iconos** | Tailwind CSS 3.4.14, PostCSS, Autoprefixer, Lucide React, React Icons, FontAwesome |
| **Mapas** | Leaflet 1.9.4, React-Leaflet 4.2.1, React-Leaflet-Draw, Google Maps API |
| **Visualización** | Recharts 2.15.1, React DatePicker, React Loader Spinner |
| **Calidad de código** | ESLint 9.13.0, plugins de React y hooks |

## Arquitectura

### Estructura de carpetas

```
tatsoft-frontend/
├── public/                     # Assets estáticos
├── src/
│   ├── components/
│   │   ├── atoms/              # Componentes básicos (botones, inputs, logo)
│   │   ├── molecules/          # Combinaciones de átomos (buscador, encabezado)
│   │   ├── organisms/          # Secciones completas (sidebar, formularios, cards)
│   │   ├── pages/              # Páginas y vistas por dominio
│   │   └── Loading/            # Indicadores de carga
│   ├── context/
│   │   ├── AuthContext.jsx     # Estado global de sesión
│   │   └── services/
│   │       ├── ApiService.js   # Clientes HTTP de los microservicios
│   │       └── ImageService.js # Gestión de imágenes
│   ├── assets/                 # Recursos (logo, imágenes)
│   ├── App.jsx                 # Definición de rutas y rutas protegidas
│   ├── main.jsx                # Punto de entrada
│   └── index.css               # Estilos globales
├── index.html
├── vite.config.js              # Configuración de Vite y proxies
├── tailwind.config.js
├── postcss.config.cjs
├── eslint.config.js
└── staticwebapp.config.json    # Configuración de Azure Static Web Apps
```

### Flujo de datos

```
Componente (UI)
      ↓
AuthContext (sesión y roles)
      ↓
ApiService (Axios + interceptor de token)
      ↓
Proxy de Vite (dev) / URL directa (prod)
      ↓
Microservicios en Azure
```

## Módulos funcionales

| Módulo | Descripción | Componentes principales |
| --- | --- | --- |
| **Autenticación** | Login y recuperación de contraseña | `Login`, `RecuperarPassword`, `CodigoVerificacion`, `Restablecer` |
| **Usuarios** | Gestión de cuentas y solicitudes | `GestionUsuarios`, `RegistroUsuario`, `EditarUsuario`, `ListaSolicitudes` |
| **Zonas** | Territorios geográficos y asignaciones | `GestionZonas`, `RegistrarZona`, `ColaboradoresZona`, `AsignacionZonas` |
| **Clientes** | CRM y registro de clientes | `GestionClientes`, `RegistroCliente`, `EditarCliente`, `VerCliente` |
| **Productos** | Catálogo y categorías | `GestionProductos`, `RegistrarProducto`, `EditarProducto`, `GestionCategorias` |
| **Inventario** | Control de stock | `IngresoStock`, `HistorialIngresos` |
| **Preventas** | Pedidos anticipados | `NuevaPreventa`, `HistorialPreventas`, `ConfirmarPreventa` |
| **Ventas** | Registro e historial | `HistorialVentas`, `DetallesVenta` |
| **Devoluciones** | Retornos y créditos | `HistorialDevoluciones`, `ComparativaVentasDevoluciones`, `ResumenDevoluciones` |
| **Estadísticas** | Dashboards y reportes | `RolBasedStats`, `EstadisticasVentas`, `EstadisticasColaborador` |
| **Colaborador** | Perfil y acumulados | `Profile`, `EditarPerfil`, `Acumulados` |

## Microservicios

La aplicación se comunica con cinco microservicios independientes desplegados en **Azure App Services**, cada uno responsable de un dominio de negocio:

| Microservicio | Prefijo local | Dominio |
| --- | --- | --- |
| **Auth** | `/auth-api/*` | Autenticación y emisión de tokens |
| **Users** | `/users-api/*` | Usuarios, roles y asignación de zonas |
| **Areas & Clients** | `/areas-api/*` | Zonas geográficas y clientes |
| **Products** | `/products-api/*` | Catálogo, categorías y stock |
| **Presales** | `/presales-api/*` | Preventas, ventas y devoluciones |

En desarrollo, `ApiService.js` usa estos prefijos y Vite los redirige a cada backend. En producción, `ApiService.js` apunta directamente a las URLs de Azure App Services.

## Estado del despliegue

La infraestructura de despliegue está **correctamente implementada y validada**. El pipeline de CI/CD (`.github/workflows/azure-static-web-apps-*.yml`) publica el frontend en **Azure Static Web Apps** y los cinco microservicios operan en **Azure App Services** con proxies y `staticwebapp.config.json` ya configurados para producción.

> [!WARNING]
> **Despliegue temporalmente en pausa.** El proyecto se encuentra momentáneamente suspendido porque **el pago de los créditos de los servicios de Azure está en pausa**. No se trata de un problema de código ni de arquitectura: tanto el frontend como los microservicios están listos y funcionales, pero los recursos de Azure están detenidos por el estado de la suscripción.

Consecuencias mientras la suscripción permanezca pausada:

- Las URLs de **Azure Static Web Apps** (frontend) no están accesibles.
- Los microservicios en **Azure App Services** están suspendidos.
- Las llamadas a las APIs devuelven errores de conexión, por lo que la aplicación no puede autenticar usuarios ni cargar datos.

Una vez se restablezca el pago de los créditos, el despliegue puede reanudarse sin cambios de código, reejecutando el workflow de CI/CD y reactivando los App Services.

## Seguridad y autenticación

- **Rutas protegidas**: el componente `ProtectedRoute` valida la sesión y el rol antes de renderizar cada vista (`App.jsx`).
- **Contexto centralizado**: `AuthContext` administra el token (persistido en `localStorage`) y el perfil del usuario.
- **Interceptor de token**: cada cliente Axios inyecta el header `Authorization: Bearer <token>` de forma automática.
- **Roles soportados**: `ADMINISTRADOR` y `COLABORADOR`, con rutas restringidas según el rol.
- **Configuración de seguridad**: `staticwebapp.config.json` define cabeceras de seguridad, CORS y redirección de sesiones no autorizadas hacia `/login`.

---

<div align="center">

**TATSoft** — Gestión empresarial inteligente

</div>
