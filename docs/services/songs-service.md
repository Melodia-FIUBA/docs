# 🎵 Songs Service

El Songs Service es el microservicio encargado de gestionar toda la lógica relacionada con canciones, álbumes, playlists y colecciones en Melodia.

---

## Overview

El Songs Service es un microservicio desarrollado en Python con Flask que maneja:

- **Canciones**: CRUD, búsqueda, streaming
- **Álbumes**: Agrupación de canciones por artista
- **Playlists**: Colecciones personalizadas de usuarios
- **Favoritos**: Canciones marcadas por usuarios
- **Disponibilidad**: Bloqueos por admin, restricciones por región

<!-- TODO: Agregar descripción más detallada del alcance del servicio -->

**Repositorio**: [Melodia-FIUBA/songs-service](https://github.com/Melodia-FIUBA/songs-service)

---

## Stack Tecnológico

| Categoría | Tecnología | Versión |
|-----------|------------|---------|
| Lenguaje | Python | <!-- TODO --> 3.11 |
| Framework | Flask | <!-- TODO --> 3.x |
| ORM | SQLAlchemy | <!-- TODO --> 2.x |
| Migraciones | Alembic | <!-- TODO --> 1.x |
| Base de datos | PostgreSQL | <!-- TODO --> 15 |
| Storage | Google Cloud Storage | <!-- TODO --> - |
| Validación | Marshmallow | <!-- TODO --> 3.x |
| Testing | pytest | <!-- TODO --> 7.x |
| Documentación API | Flask-RESTX / OpenAPI | <!-- TODO --> - |

<!-- TODO: Actualizar versiones reales -->

---

## Arquitectura del Servicio

<!-- TODO: Agregar diagrama de arquitectura interna del servicio -->
![Arquitectura del Servicio](../assets/diagrams/songs-service-architecture.png)

### Estructura del Proyecto

```
songs-service/
├── app/
│   ├── __init__.py
│   ├── models/           # Modelos SQLAlchemy
│   │   ├── song.py
│   │   ├── album.py
│   │   ├── playlist.py
│   │   └── ...
│   ├── routes/           # Endpoints de la API
│   │   ├── songs.py
│   │   ├── albums.py
│   │   ├── playlists.py
│   │   └── ...
│   ├── services/         # Lógica de negocio
│   │   ├── song_service.py
│   │   ├── storage_service.py
│   │   └── ...
│   ├── schemas/          # Schemas de validación
│   └── utils/            # Utilidades
├── migrations/           # Migraciones de Alembic
├── tests/               # Tests
├── config.py            # Configuración
├── requirements.txt
└── Dockerfile
```

<!-- TODO: Actualizar con estructura real del proyecto -->

### Capas de la Aplicación

```mermaid
graph TB
    subgraph "Songs Service"
        Routes[Routes Layer]
        Services[Services Layer]
        Models[Models Layer]
        DB[(PostgreSQL)]
        GCS[Cloud Storage]
    end
    
    Routes --> Services
    Services --> Models
    Models --> DB
    Services --> GCS
```

---

## Modelo de Datos

<!-- TODO: Agregar diagrama ER creado en draw.io o dbdiagram.io -->
![Modelo de Datos](../assets/diagrams/songs-service-er.png)

### Entidades Principales

| Entidad | Descripción | Relaciones |
|---------|-------------|------------|
| Song | Canción individual | Pertenece a Album, tiene Artista |
| Album | Colección de canciones de un artista | Tiene muchas Songs |
| Playlist | Colección personalizada | Pertenece a User, tiene muchas Songs |
| Favorite | Marcador de favorito | Pertenece a User, referencia Song |

### Diagrama ER Simplificado

```mermaid
erDiagram
    SONG {
        uuid id PK
        string title
        string artist_id FK
        uuid album_id FK
        string storage_url
        int duration_seconds
        boolean is_blocked
        timestamp created_at
    }
    
    ALBUM {
        uuid id PK
        string title
        string artist_id
        string cover_url
        timestamp release_date
    }
    
    PLAYLIST {
        uuid id PK
        string name
        string user_id FK
        boolean is_public
        timestamp created_at
    }
    
    PLAYLIST_SONG {
        uuid playlist_id PK,FK
        uuid song_id PK,FK
        int position
    }
    
    ALBUM ||--o{ SONG : contains
    PLAYLIST ||--o{ PLAYLIST_SONG : has
    SONG ||--o{ PLAYLIST_SONG : in
```

<!-- TODO: Completar diagrama con todas las entidades -->

---

## Conexiones con Otros Servicios

```mermaid
graph LR
    Songs[🎵 Songs Service]
    
    Songs --> Users[👤 Users Service]
    Songs --> GCS[☁️ Cloud Storage]
    
    Users --> |Validación JWT| Songs
    GCS --> |Almacenamiento Audio| Songs
```

### Dependencias

| Servicio/Recurso | Propósito | Tipo de Comunicación |
|------------------|-----------|---------------------|
| Users Service | Validar JWT tokens | HTTP REST |
| Cloud Storage | Almacenar archivos de audio | SDK de GCS |
| Cloud SQL | Persistencia de datos | Conexión directa |

---

## Endpoints Principales

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/songs` | Listar canciones | Opcional |
| POST | `/songs` | Crear canción | Requerido (Artista) |
| GET | `/songs/{id}` | Obtener canción | Opcional |
| PUT | `/songs/{id}` | Actualizar canción | Requerido (Owner) |
| DELETE | `/songs/{id}` | Eliminar canción | Requerido (Owner) |
| GET | `/songs/{id}/stream` | URL de streaming | Requerido |
| GET | `/albums` | Listar álbumes | Opcional |
| POST | `/albums` | Crear álbum | Requerido (Artista) |
| GET | `/playlists` | Listar playlists del usuario | Requerido |
| POST | `/playlists` | Crear playlist | Requerido |
| POST | `/playlists/{id}/songs` | Agregar canción a playlist | Requerido (Owner) |
| GET | `/artists/{id}/songs` | Canciones de un artista | Opcional |
| GET | `/search` | Búsqueda de canciones | Opcional |

<!-- TODO: Completar con todos los endpoints disponibles -->

---

## Sistema de Disponibilidad

### Bloqueo por Administrador

Los administradores pueden bloquear canciones que violen políticas:

```python
# Ejemplo de lógica de bloqueo
class Song:
    is_blocked: bool = False
    blocked_reason: str | None = None
    blocked_at: datetime | None = None
    blocked_by: str | None = None  # admin_id
```

### Restricciones por Región

<!-- TODO: Completar si aplica -->

*Pendiente de implementar*

---

## Decisiones de Implementación

### 1. Arquitectura en Capas

<!-- TODO: Completar con justificación real -->

**Decisión**: Usar arquitectura en capas (Routes → Services → Models).

**Razón**: *Pendiente de completar*

**Consecuencias**:

- Separación clara de responsabilidades
- Facilita testing unitario
- *Pendiente de completar*

---

### 2. Alembic para Migraciones

<!-- TODO: Completar con justificación real -->

**Decisión**: Usar Alembic para gestión de migraciones de base de datos.

**Razón**: *Pendiente de completar*

---

### 3. URLs Firmadas para Streaming

<!-- TODO: Completar con implementación real -->

**Decisión**: Usar URLs firmadas de GCS para streaming de audio.

**Implementación**:

```python
# Ejemplo simplificado
def get_signed_url(blob_name: str, expiration_minutes: int = 15):
    bucket = storage_client.bucket(BUCKET_NAME)
    blob = bucket.blob(blob_name)
    return blob.generate_signed_url(
        expiration=timedelta(minutes=expiration_minutes),
        method="GET"
    )
```

---

### 4. Soft Delete vs Hard Delete

<!-- TODO: Completar con decisión real -->

**Decisión**: *Pendiente de completar*

---

## Aprendizajes

### 1. Manejo de Archivos Grandes

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

### 2. Optimización de Queries de Búsqueda

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

### 3. Manejo de Transacciones

<!-- TODO: Completar con aprendizaje real -->

**Problema**: *Pendiente de completar*

**Solución**: *Pendiente de completar*

**Aprendizaje**: *Pendiente de completar*

---

## Setup Local

### Requisitos

- Python 3.11+
- Docker y Docker Compose
- Google Cloud SDK (opcional, para testing con GCS)

### Instalación

```bash
# Clonar repositorio
git clone https://github.com/Melodia-FIUBA/songs-service.git
cd songs-service

# Crear entorno virtual
python -m venv venv
source venv/bin/activate  # Linux/Mac
# o: venv\Scripts\activate  # Windows

# Instalar dependencias
pip install -r requirements.txt

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
docker-compose exec app flask db upgrade
```

### Variables de Entorno

```bash
# .env.example
FLASK_ENV=development
DATABASE_URL=postgresql://user:password@localhost:5432/songs_db
GCS_BUCKET_NAME=melodia-songs-dev
GCS_CREDENTIALS_PATH=/path/to/credentials.json
USERS_SERVICE_URL=http://localhost:8001
JWT_SECRET_KEY=your-secret-key
```

<!-- TODO: Agregar todas las variables de entorno necesarias -->

---

## Testing

```bash
# Ejecutar todos los tests
pytest

# Ejecutar con coverage
pytest --cov=app --cov-report=html

# Ejecutar tests específicos
pytest tests/test_songs.py -v
```

<!-- TODO: Actualizar comandos según configuración real -->

!!! tip "Base de datos de test"
    Los tests usan una base de datos SQLite en memoria por defecto. Para tests de integración, se usa un contenedor PostgreSQL.
