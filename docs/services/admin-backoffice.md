# 🖥️ Admin Backoffice

**Repositorio**: [Melodia-FIUBA/admin-backoffice](https://github.com/Melodia-FIUBA/admin-backoffice)

El Admin Backoffice es el panel de administración web de Melodia, utilizado por el equipo de operaciones para gestionar usuarios, contenido y configuraciones del sistema.

---

## Diagrama de Arquitectura

```mermaid
graph LR
<<<<<<< HEAD
    Admin[🖥️ Admin Backoffice]

    Admin --> Users[👤 Users Service]
    Admin --> Songs[🎵 Content Service]
    Admin --> AdminSvc[⚙️ Admin Service]

    Users --> |Autenticación Admin| Admin
    Songs --> |Gestión de Contenido| Admin
    AdminSvc --> |Operaciones Admin| Admin
=======
    subgraph Frontend
        Admin[🖥️ Admin Backoffice (Next.js)]
        Admin --> Cookies[(Cookies)]
    end

    subgraph APIs
        UsersAPI[👤 Users API]
        SongsBackofficeAPI[🎵 Songs Backoffice API]
        UsersBackofficeAPI[⚙️ Users Backoffice Backoffice API]
    end

    Admin --> |Login / Logout| UsersAPI
    Admin --> |Gestión Usuarios| UsersBackofficeAPI
    Admin --> |Catálogo, Bloqueos, Métricas| SongsBackofficeAPI

    UsersAPI --> |Endpoints|
        Login[/api/v1/auth/login/]
        Logout[/api/v1/auth/logout/]
        Sessions[/api/v1/sessions/]

    UsersBackofficeAPI --> |Endpoints|
        ListUsers[/api/v1/users/]
        CrudUsersId[/api/v1/users/:id/]

    SongsBackofficeAPI --> |Endpoints|
        Search[/search/]
        CollectionsId[/collections/:id/]
        SongsId[/songs/:id/]
        PlaylistsId[/playlists/:id/]
        Appearances[/songs|collections/:id/appearances/]
        CoverDownload[/storage/download-url/]
        Blocks[/admin/blocks/ ...]
        Audit[/songs|collections/:id/audit/]
        Metrics[/artists|users|songs|collections/:id/metrics/]
>>>>>>> 1807b19249b3474f07fb1be9cb408a0c6f8743ba
```

Notas:
- Las URLs base se configuran vía variables de entorno en GCP: MELODIA_USERS_API_URL, MELODIA_SONGS_BACKOFFICE_API_URL y MELODIA_USERS_BACKOFFICE_API_URL.
- La autenticación se maneja con endpoints de login/logout y cookies.

---

## Tech Stack

Basado en package.json y la estructura del proyecto.

| Categoría     | Tecnología                   | Versión            |
| ------------- | ---------------------------- | ------------------ |
| Framework     | Next.js                      | 16.0.1             |
| Lenguaje      | TypeScript                   | ^5 (20.x tipos)    |
| React         | React                        | 19.2.0             |
| UI Components | Chakra UI                    | @chakra-ui/react 3.28.1 |
| Estilos       | Tailwind CSS                 | ^4 (con @tailwindcss/postcss) |
| Temas         | next-themes                  | 0.4.6              |
| Formularios   | react-hook-form              | 7.66.0             |
| Iconos        | react-icons                  | 5.5.0              |
| Charts        | Recharts                     | 3.5.0              |
| Charts (UI)   | @chakra-ui/charts            | 3.30.0             |
| Visualización | react-svg-worldmap           | 2.0.0-alpha.16     |
| Exportación   | xlsx                         | 0.18.5             |
| Linter        | eslint + eslint-config-next  | ^9 + 16.0.1        |
| Testing       | -                            | No configurado     |

---

## Estructura y Rutas Principales

- App Router (Next.js):
  - app/layout.tsx, app/globals.css
  - app/page.tsx (home previo al login)
  - app/login/page.tsx (login)
  - app/admin/page.tsx y app/admin/layout.tsx (Home del Backoffice)
  - app/admin/userpanel/page.tsx (Panel de Metricas de Usuarios)
  - app/admin/users/page.tsx y app/admin/users/[id]/page.tsx (Usuarios)
  - app/admin/artistpanel/[id]/page.tsx (Panel de Metricas de Artista)
  - app/admin/catalog/page.tsx (Catálogo)
  - app/admin/catalog/[type]/[id]/page.tsx y edit-policy/page.tsx (Vistas Detalladas de Contenido)
  - app/api/config/route.ts (Obtención de variables de entorno del servidor)

- Componentes relevantes:
  - components/users/* (tabla, acciones, bloqueos)
  - components/catalog/* (tabs de disponibilidad, bloqueo, auditoría, métricas, edición, mapa)
  - components/metrics/* (KPI usuarios, colecciones, canciones, artistas)
  - components/ui/* (provider de Chakra, color-mode, tooltip, toaster)

- Librerías internas:
  - lib/config/envs.ts (lectura de variables de entorno)
  - lib/log/* (login/logout/cookies)
  - lib/users/* (get, edit, delete, block)
  - lib/catalog/* (búsqueda, detalles, auditoría, disponibilidad, bloqueos, edición, cover)
  - lib/metrics/* (artistas, catálogo, usuarios)
  - lib/utils/* (exportación a Excel, estados efectivos)

---

## Decisiones Clave y Features Destacadas

### 1. Next.js App Router
**Decisión**: Se eligió Next.js con App Router sobre Pages Router.
**Razón**: Recomendado por la catedra y experiencias previas

Detalles técnicos:
- Estructura en app/ con layouts por sección (admin, catalog, users).
- Uso de React 19.2 y Next 16.0.1, alineados con App Router.
- CSS global (app/globals.css) y composición por secciones.

### 2. Chakra UI como sistema de componentes
**Decisión**: Usar Chakra UI para UI con theming y componentes accesibles.
**Razón**: Interfaz visualmente agrasable y sencilla de manejar

Notas:
- Uso de `@chakra-ui/charts` para gráficos.

---

## DevOps, Testing 


### Testing
No hay configuración de testing para el backoffice web.

### DevOps
Se utilizó Google Cloud Provider para realizar el hosting cloud de la web, utilizando un servicio de contenedor Docker


---

## Decisiones de arquitectura tomadas

- Separación por dominios en lib/ (users, catalog, metrics, log), alineado con los microservicios de backend referenciados por las variables de entorno.
- App Router y layouts por sección para aislar UI/estado por contexto (admin, catalog, users).
- Manejo de autenticación por endpoints y cookies.
- Uso de Chakra UI + Tailwind CSS 4 para UI y estilos utilitarios combinados.
- Visualización con Recharts y `@chakra-ui/charts` para métricas, y `react-svg-worldmap` para disponibilidad geográfica.

---

## Funcionalidades incompletas o por pulir, errores conocidos

- Errores conocidos en la entrega final: No se realiza busqueda por artista en la vista de catálogo (aunque fue conversado con los profesores)

---

## Problemas encontrados y lecciones aprendidas

- Integración de múltiples APIs con rutas heterogéneas y seguridad por cookies: Ocurria ocasionalmente que se tenía un diseño mock desde el frontend de una posible respuesta del backend, pero luego dicha "idea" no terminaba siendo la desarrollada por el backend, implicando refactors a la web.

---

## Anexos: Mapa de archivos clave

- app/admin/users/page.tsx y components/users/* para gestión de usuarios
- app/admin/catalog/* y lib/catalog/* para catálogo, auditoría, disponibilidad y bloqueos
- app/admin/artistpanel/[id]/page.tsx para panel de artistas
- lib/log/* para login/logout/cookies
- lib/metrics/* y components/metrics/* para KPIs y gráficos
- lib/config/envs.ts para configuración de entornos
