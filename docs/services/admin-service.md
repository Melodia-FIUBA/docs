# ⚙️ Admin Service

El Admin Service es el microservicio encargado de las operaciones administrativas en Melodia.

---

## Overview

El Admin Service es un microservicio desarrollado en Go que proporciona funcionalidades exclusivas para administradores:

- **Gestión de usuarios**: Bloquear/desbloquear, modificar roles
- **Gestión de contenido**: Moderar canciones, álbumes
- **Métricas y estadísticas**: Datos agregados del sistema
- **Logs de auditoría**: Registro de acciones administrativas

<!-- TODO: Agregar descripción más detallada del alcance del servicio -->

**Repositorio**: [Melodia-FIUBA/admin-service](https://github.com/Melodia-FIUBA/admin-service)

---

## Stack Tecnológico

| Categoría | Tecnología | Versión |
|-----------|------------|---------|
| Lenguaje | Go | <!-- TODO --> 1.21 |
| Framework HTTP | Gin | <!-- TODO --> 1.x |
| ORM | GORM | <!-- TODO --> 1.x |
| Base de datos | PostgreSQL | <!-- TODO --> 15 |
| Validación | go-playground/validator | <!-- TODO --> 10.x |
| Testing | testify | <!-- TODO --> 1.x |
| Documentación API | Swaggo | <!-- TODO --> - |

<!-- TODO: Actualizar versiones reales -->

---

## Arquitectura del Servicio

<!-- TODO: Agregar diagrama de arquitectura interna del servicio -->
![Arquitectura del Servicio](../assets/diagrams/admin-service-architecture.png)

### Estructura del Proyecto

```
admin-service/
├── cmd/
│   └── server/
│       └── main.go           # Entry point
├── internal/
│   ├── handlers/             # HTTP handlers
│   │   ├── users_handler.go
│   │   ├── content_handler.go
│   │   └── stats_handler.go
│   ├── services/             # Lógica de negocio
│   │   ├── moderation_service.go
│   │   └── stats_service.go
│   ├── repositories/         # Acceso a datos
│   │   └── audit_repository.go
│   ├── models/               # Modelos de dominio
│   │   └── audit_log.go
│   ├── middleware/           # Middlewares
│   │   └── admin_auth.go
│   └── config/               # Configuración
├── pkg/                      # Paquetes exportables
├── migrations/               # Migraciones SQL
├── tests/                    # Tests
├── Dockerfile
├── go.mod
└── go.sum
```

<!-- TODO: Actualizar con estructura real del proyecto -->

### Capas de la Aplicación

```mermaid
graph TB
    subgraph "Admin Service"
        Handlers[Handlers Layer]
        Services[Services Layer]
        Repos[Repositories Layer]
        DB[(PostgreSQL)]
    end
    
    Handlers --> Services
    Services --> Repos
    Repos --> DB
```

---

## Modelo de Datos

<!-- TODO: Agregar diagrama ER creado en draw.io o dbdiagram.io -->
![Modelo de Datos](../assets/diagrams/admin-service-er.png)

### Entidades Principales

| Entidad | Descripción | Campos Principales |
|---------|-------------|-------------------|
| AuditLog | Registro de acciones admin | action, admin_id, target, timestamp |
| BlockRecord | Registro de bloqueos | type, target_id, reason, blocked_by |
| SystemConfig | Configuraciones del sistema | key, value, updated_by |

### Diagrama ER Simplificado

```mermaid
erDiagram
    AUDIT_LOG {
        uuid id PK
        string action
        uuid admin_id
        string target_type
        uuid target_id
        json details
        timestamp created_at
    }
    
    BLOCK_RECORD {
        uuid id PK
        string target_type
        uuid target_id
        string reason
        uuid blocked_by FK
        timestamp blocked_at
        timestamp unblocked_at
    }
    
    SYSTEM_CONFIG {
        string key PK
        string value
        uuid updated_by FK
        timestamp updated_at
    }
```

<!-- TODO: Completar diagrama con todas las entidades -->

---

## Conexiones con Otros Servicios

```mermaid
graph LR
    Admin[⚙️ Admin Service]
    
    Admin --> Users[👤 Users Service]
    Admin --> Songs[🎵 Songs Service]
    Backoffice[🖥️ Admin Backoffice] --> Admin
    
    Users --> |Validación JWT Admin| Admin
    Admin --> |Bloquear usuarios| Users
    Admin --> |Bloquear contenido| Songs
```

### Dependencias

| Servicio | Propósito | Tipo de Comunicación |
|----------|-----------|---------------------|
| Users Service | Validar JWT de admin, gestionar usuarios | HTTP REST |
| Songs Service | Gestionar contenido (bloqueos, etc.) | HTTP REST |

---

## Endpoints Principales

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/admin/users` | Listar todos los usuarios | Admin |
| GET | `/admin/users/{id}` | Detalle de usuario | Admin |
| PUT | `/admin/users/{id}/block` | Bloquear usuario | Admin |
| PUT | `/admin/users/{id}/unblock` | Desbloquear usuario | Admin |
| PUT | `/admin/users/{id}/role` | Cambiar rol de usuario | Admin |
| GET | `/admin/songs` | Listar todas las canciones | Admin |
| PUT | `/admin/songs/{id}/block` | Bloquear canción | Admin |
| PUT | `/admin/songs/{id}/unblock` | Desbloquear canción | Admin |
| GET | `/admin/stats/overview` | Estadísticas generales | Admin |
| GET | `/admin/stats/users` | Estadísticas de usuarios | Admin |
| GET | `/admin/stats/content` | Estadísticas de contenido | Admin |
| GET | `/admin/audit-logs` | Logs de auditoría | Admin |

<!-- TODO: Completar con todos los endpoints disponibles -->

---

## Sistema de Auditoría

### Tipos de Acciones Registradas

```go
const (
    ActionUserBlocked   = "USER_BLOCKED"
    ActionUserUnblocked = "USER_UNBLOCKED"
    ActionRoleChanged   = "ROLE_CHANGED"
    ActionSongBlocked   = "SONG_BLOCKED"
    ActionSongUnblocked = "SONG_UNBLOCKED"
    ActionConfigChanged = "CONFIG_CHANGED"
)
```

### Formato de Log

```json
{
  "id": "uuid",
  "action": "USER_BLOCKED",
  "admin_id": "admin-uuid",
  "target_type": "user",
  "target_id": "user-uuid",
  "details": {
    "reason": "Violación de términos de servicio",
    "previous_state": "active"
  },
  "created_at": "2024-01-01T12:00:00Z"
}
```

---

## Decisiones de Implementación

### 1. Servicio Separado para Admin

<!-- TODO: Completar con justificación real -->

**Decisión**: Crear un servicio dedicado para operaciones administrativas.

**Razón**: *Pendiente de completar*

**Consecuencias**:

- Mejor separación de concerns
- Escalamiento independiente
- *Pendiente de completar*

---

### 2. Comunicación con Otros Servicios

<!-- TODO: Completar con justificación real -->

**Decisión**: Usar REST síncrono para operaciones admin.

**Razón**: *Pendiente de completar*

**Alternativas consideradas**: Message queue, gRPC

---

### 3. Auditoría Completa

<!-- TODO: Completar con implementación real -->

**Decisión**: Registrar todas las acciones administrativas.

**Implementación**:

- Middleware que intercepta todas las operaciones
- Log persistido en base de datos
- Retención de logs: *pendiente de definir*

---

### 4. Permisos Granulares

<!-- TODO: Completar con decisión real -->

**Decisión**: *Pendiente de completar*

---

## Aprendizajes

### 1. Manejo de Operaciones Cross-Service

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

### 2. Auditoría sin Impactar Performance

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

### 3. Consistencia en Operaciones Distribuidas

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

## Setup Local

### Requisitos

- Go 1.21+
- Docker y Docker Compose
- Make (opcional)

### Instalación

```bash
# Clonar repositorio
git clone https://github.com/Melodia-FIUBA/admin-service.git
cd admin-service

# Instalar dependencias
go mod download

# Configurar variables de entorno
cp .env.example .env
# Editar .env con valores correctos
```

### Ejecutar con Docker Compose

```bash
# Levantar servicios (app + postgres)
docker-compose up -d

# Ver logs
docker-compose logs -f app

# Ejecutar migraciones
docker-compose exec app ./migrate up
```

### Ejecutar Localmente

```bash
# Compilar
go build -o bin/server cmd/server/main.go

# Ejecutar
./bin/server

# O directamente
go run cmd/server/main.go
```

### Variables de Entorno

```bash
# .env.example
PORT=8003
ENV=development
DATABASE_URL=postgresql://user:password@localhost:5432/admin_db
USERS_SERVICE_URL=http://localhost:8001
SONGS_SERVICE_URL=http://localhost:8002
JWT_SECRET_KEY=your-super-secret-key-min-32-chars
```

<!-- TODO: Agregar todas las variables de entorno necesarias -->

---

## Testing

```bash
# Ejecutar todos los tests
go test ./...

# Ejecutar con coverage
go test ./... -cover -coverprofile=coverage.out

# Ver reporte de coverage
go tool cover -html=coverage.out

# Ejecutar tests específicos
go test ./internal/services/... -v
```

<!-- TODO: Actualizar comandos según configuración real -->

!!! tip "Tests de Integración"
    Los tests de integración requieren que los servicios de Users y Songs estén disponibles (o mockeados).
