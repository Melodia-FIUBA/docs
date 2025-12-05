# 🎵 Melodia

## Descripción

**Melodia** es una plataforma de streaming de música desarrollada como proyecto académico para la materia Ingeniería de Software 2 de la Facultad de Ingeniería de la Universidad de Buenos Aires (FIUBA).

La plataforma permite a los usuarios escuchar música, crear playlists, seguir a artistas y descubrir nueva música. Los artistas pueden subir su contenido, gestionar su perfil y acceder a estadísticas de reproducción. Los administradores cuentan con un panel completo para gestionar usuarios, contenido y configuraciones del sistema.

📄 **[Enunciado del Trabajo Práctico](enunciado.md)**

🎬 **[Video Demo (Pending)]()** <!-- TODO: Reemplazar con link real del video demo -->

---

## 👥 Equipo

| Nombre                    | Rol                       | GitHub                        |
| ------------------------- | ------------------------- | ----------------------------- |
| Agustín García Dresch     | Frontend Mobile Developer | -                             |
| Franco Daniel Capra       | Backend Developer         | -                             |
| Grabriel Fernan Carniglia | Frontend Web Developer    | -                             |
| Santiago Janon            | Frontend Mobile Developer | -                             |
| Theo Miguel               | Backend Developer         | https://github.com/TheoMiguel |

---

## 📑 Tabla de Contenidos

### [Arquitectura e Infraestructura](architecture.md)

Visión general de la arquitectura del sistema, infraestructura en GCP y comunicación entre servicios.

### Roadmap y Checkpoints

Progreso del proyecto organizado por checkpoints de desarrollo. Cada sprint entre los checkpoints fué de 3 semanas.

- [Checkpoint 1](checkpoints/checkpoint-1.md)
- [Checkpoint 2](checkpoints/checkpoint-2.md)
- [Checkpoint 3](checkpoints/checkpoint-3.md)
- [Checkpoint 4](checkpoints/checkpoint-4.md)

### Servicios y Repositorios

- 📱 [Mobile App](services/mobile-app.md) - Aplicación móvil React Native para usuarios (oyentes y artistas)
- 🖥️ [Admin Backoffice](services/admin-backoffice.md) - Panel web Next.js de administración
- 🎵 [Content Service](services/songs-service.md) - Microservicio Python/Flask para gestión de canciones y playlists
- 👤 [Users Service](services/users-service.md) - Microservicio Go para autenticación y gestión de usuarios
- ⚙️ [Admin Service](services/admin-service.md) - Microservicio Go para operaciones administrativas

### [Decisiones de Arquitectura](decisions-and-learnings.md)

Decisiones técnicas de alto nivel y justificaciones.

### [Problemas Conocidos y Features Incompletas](known-issues.md)

Bugs identificados, funcionalidades pendientes y deuda técnica.
