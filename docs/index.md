# 🎵 Melodia

Bienvenido a la documentación técnica de **Melodia**, una plataforma de streaming de música desarrollada como proyecto académico. Este sitio contiene toda la información necesaria para entender la arquitectura, los servicios, y las decisiones técnicas tomadas durante el desarrollo.

Melodia permite a los usuarios escuchar música, crear playlists, seguir a artistas, y descubrir nueva música. Los artistas pueden subir su contenido, gestionar su perfil y acceder a estadísticas de reproducción. Los administradores cuentan con un panel completo para gestionar usuarios, contenido y configuraciones del sistema.

<!-- TODO: Agregar descripción más detallada del proyecto una vez definido el alcance final -->

---

## 🧩 Componentes del Sistema

| Componente | Tecnología | Descripción | Repositorio |
|------------|------------|-------------|-------------|
| 📱 Mobile App | React Native | Aplicación móvil para usuarios (artistas y oyentes) | [mobile-app](https://github.com/Melodia-FIUBA/mobile-app) |
| 🖥️ Admin Backoffice | Next.js | Panel web de administración | [admin-backoffice](https://github.com/Melodia-FIUBA/admin-backoffice) |
| 🎵 Songs Service | Python/Flask | Microservicio para gestión de canciones y colecciones | [songs-service](https://github.com/Melodia-FIUBA/songs-service) |
| 👤 Users Service | Go | Microservicio para autenticación y gestión de usuarios | [users-service](https://github.com/Melodia-FIUBA/users-service) |
| ⚙️ Admin Service | Go | Microservicio para operaciones administrativas | [admin-service](https://github.com/Melodia-FIUBA/admin-service) |

---

## 👥 Equipo

<!-- TODO: Agregar información del equipo -->

| Nombre | Rol | GitHub |
|--------|-----|--------|
| *Pendiente* | - | - |
| *Pendiente* | - | - |
| *Pendiente* | - | - |
| *Pendiente* | - | - |
| *Pendiente* | - | - |

---

## 🚀 Navegación Rápida

<div class="grid cards" markdown="1">

-   :material-architecture:{ .lg .middle } **Arquitectura**

    ---

    Conoce la arquitectura del sistema, infraestructura en GCP y patrones de diseño

    [:octicons-arrow-right-24: Ver Arquitectura](architecture.md)

-   :material-road-variant:{ .lg .middle } **Roadmap**

    ---

    Revisa los checkpoints del proyecto y el progreso del desarrollo

    [:octicons-arrow-right-24: Ver Roadmap](roadmap.md)

-   :material-api:{ .lg .middle } **Contratos de API**

    ---

    Documentación interactiva de las APIs de los servicios

    [:octicons-arrow-right-24: Ver APIs](api-contracts.md)

-   :material-lightbulb:{ .lg .middle } **Decisiones y Aprendizajes**

    ---

    Decisiones técnicas tomadas y lecciones aprendidas

    [:octicons-arrow-right-24: Ver Decisiones](decisions-and-learnings.md)

</div>

---

## 📊 Diagrama de Contexto

<!-- TODO: Agregar diagrama de contexto general creado en draw.io -->
![Diagrama de Contexto](assets/diagrams/context-diagram.png)

!!! note "Nota"
    El diagrama de contexto muestra una visión de alto nivel del sistema y sus interacciones con actores externos.
