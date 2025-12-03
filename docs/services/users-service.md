# 👤 Users Service

El Users Service es el microservicio encargado de la autenticación, autorización y gestión de usuarios en Melodia.

---

## Overview

El Users Service es un microservicio desarrollado en Go que maneja:

- **Autenticación**: Login, registro, logout
- **Autorización**: Generación y validación de JWT tokens
- **Gestión de usuarios**: CRUD de perfiles
- **Roles**: Diferenciación entre oyentes, artistas y admins

<!-- TODO: Agregar descripción más detallada del alcance del servicio -->

**Repositorio**: [Melodia-FIUBA/users-service](https://github.com/Melodia-FIUBA/users-service)

---

## Stack Tecnológico

| Categoría | Tecnología | Versión |
|-----------|------------|---------|
| Lenguaje | Go | <!-- TODO --> 1.21 |
| Framework HTTP | Gin | <!-- TODO --> 1.x |
| ORM | GORM | <!-- TODO --> 1.x |
| Base de datos | PostgreSQL | <!-- TODO --> 15 |
| Autenticación | JWT (golang-jwt) | <!-- TODO --> 5.x |
| Validación | go-playground/validator | <!-- TODO --> 10.x |
| Testing | testify | <!-- TODO --> 1.x |
| Documentación API | Swaggo | <!-- TODO --> - |

<!-- TODO: Actualizar versiones reales -->

---

## Arquitectura del Servicio

<!-- TODO: Agregar diagrama de arquitectura interna del servicio -->
![Arquitectura del Servicio](../assets/diagrams/users-service-architecture.png)

### Estructura del Proyecto

```
users-service/
├── cmd/
│   └── server/
│       └── main.go           # Entry point
├── internal/
│   ├── handlers/             # HTTP handlers
│   │   ├── auth_handler.go
│   │   └── user_handler.go
│   ├── services/             # Lógica de negocio
│   │   ├── auth_service.go
│   │   └── user_service.go
│   ├── repositories/         # Acceso a datos
│   │   └── user_repository.go
│   ├── models/               # Modelos de dominio
│   │   └── user.go
│   ├── middleware/           # Middlewares
│   │   └── auth_middleware.go
│   └── config/               # Configuración
├── pkg/                      # Paquetes exportables
│   └── jwt/
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
    subgraph "Users Service"
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
![Modelo de Datos](../assets/diagrams/users-service-er.png)

### Entidades Principales

| Entidad | Descripción | Campos Principales |
|---------|-------------|-------------------|
| User | Usuario del sistema | id, email, password_hash, role, profile |
| Profile | Información de perfil | display_name, avatar_url, bio |
| Session | Sesión activa | token_id, user_id, expires_at |

### Diagrama ER Simplificado

```mermaid
erDiagram
    USER {
        uuid id PK
        string email UK
        string password_hash
        string role
        boolean is_active
        boolean is_blocked
        timestamp created_at
        timestamp updated_at
    }
    
    PROFILE {
        uuid id PK
        uuid user_id FK,UK
        string display_name
        string avatar_url
        text bio
        string location
    }
    
    SESSION {
        uuid id PK
        uuid user_id FK
        string token_id UK
        timestamp expires_at
        string device_info
    }
    
    USER ||--|| PROFILE : has
    USER ||--o{ SESSION : has
```

<!-- TODO: Completar diagrama con todas las entidades -->

---

## Conexiones con Otros Servicios

```mermaid
graph LR
    Users[👤 Users Service]
    
    Songs[🎵 Songs Service] --> Users
    Admin[⚙️ Admin Service] --> Users
    App[📱 Mobile App] --> Users
    Backoffice[🖥️ Admin Backoffice] --> Users
    
    Users --> |Validación JWT| Songs
    Users --> |Validación JWT| Admin
```

### Consumidores

| Consumidor | Propósito |
|------------|-----------|
| Mobile App | Autenticación de usuarios |
| Admin Backoffice | Autenticación de administradores |
| Songs Service | Validación de tokens |
| Admin Service | Validación de tokens |

---

## Endpoints Principales

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | `/auth/register` | Registrar nuevo usuario | No |
| POST | `/auth/login` | Iniciar sesión | No |
| POST | `/auth/logout` | Cerrar sesión | Requerido |
| POST | `/auth/refresh` | Renovar token | Requerido |
| GET | `/auth/validate` | Validar token (interno) | Token |
| GET | `/users/me` | Obtener perfil actual | Requerido |
| PUT | `/users/me` | Actualizar perfil | Requerido |
| GET | `/users/{id}` | Obtener usuario público | Opcional |
| GET | `/users/{id}/profile` | Obtener perfil público | No |
| PUT | `/users/me/password` | Cambiar contraseña | Requerido |
| POST | `/users/me/avatar` | Subir avatar | Requerido |

<!-- TODO: Completar con todos los endpoints disponibles -->

---

## Sistema de Autenticación

### Flujo de Login

```mermaid
sequenceDiagram
    participant Client
    participant Users as Users Service
    participant DB as PostgreSQL
    
    Client->>Users: POST /auth/login (email, password)
    Users->>DB: Buscar usuario por email
    DB-->>Users: Usuario encontrado
    Users->>Users: Verificar password (bcrypt)
    Users->>Users: Generar JWT token
    Users->>DB: Crear sesión
    Users-->>Client: 200 OK + {access_token, refresh_token}
```

### Estructura del JWT

```json
{
  "header": {
    "alg": "HS256",
    "typ": "JWT"
  },
  "payload": {
    "sub": "user-uuid",
    "email": "user@example.com",
    "role": "artist",
    "exp": 1234567890,
    "iat": 1234567890
  }
}
```

### Roles de Usuario

| Rol | Descripción | Permisos |
|-----|-------------|----------|
| `listener` | Usuario oyente | Escuchar, crear playlists, favoritos |
| `artist` | Artista | Todo de listener + subir música |
| `admin` | Administrador | Todo + gestión de usuarios y contenido |

---

## Decisiones de Implementación

### 1. Go como Lenguaje

<!-- TODO: Completar con justificación real -->

**Decisión**: Usar Go para el servicio de autenticación.

**Razón**: *Pendiente de completar*

**Consecuencias**:

- Excelente performance
- Binarios compilados pequeños
- *Pendiente de completar*

---

### 2. JWT Stateless vs Sessions

<!-- TODO: Completar con justificación real -->

**Decisión**: Usar JWT tokens stateless con refresh tokens.

**Razón**: *Pendiente de completar*

**Trade-offs**:

- ✅ No requiere consulta a DB en cada request
- ⚠️ Revocación de tokens más compleja

---

### 3. Bcrypt para Passwords

<!-- TODO: Completar con configuración real -->

**Decisión**: Usar bcrypt para hash de contraseñas.

**Configuración**:

```go
// Cost factor de bcrypt
const bcryptCost = 12
```

---

### 4. Repository Pattern

<!-- TODO: Completar con justificación real -->

**Decisión**: Usar Repository pattern para acceso a datos.

**Razón**: *Pendiente de completar*

---

## Aprendizajes

### 1. Manejo de Concurrencia en Go

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

### 2. Refresh Token Rotation

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

### 3. Rate Limiting de Login

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
git clone https://github.com/Melodia-FIUBA/users-service.git
cd users-service

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
PORT=8001
ENV=development
DATABASE_URL=postgresql://user:password@localhost:5432/users_db
JWT_SECRET_KEY=your-super-secret-key-min-32-chars
JWT_EXPIRATION_HOURS=24
REFRESH_TOKEN_EXPIRATION_DAYS=7
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

!!! tip "Mocking"
    Los tests usan interfaces para permitir mocking fácil de repositorios y servicios externos.
