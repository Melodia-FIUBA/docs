# 💡 Decisiones y Aprendizajes

Esta sección documenta las decisiones de arquitectura tomadas durante el desarrollo de Melodia, así como las lecciones aprendidas por el equipo. Este registro sirve como referencia para entender el *porqué* detrás del diseño del sistema.

!!! note "Decisiones por servicio"
    Cada servicio tiene sus propias decisiones de implementación y aprendizajes específicos documentados en su página dedicada en la sección [Servicios](services/mobile-app.md).

---

## Decisiones de Arquitectura

### ¿Por qué Microservicios?

<!-- TODO: Completar con la justificación real del equipo -->

**Contexto**: Al inicio del proyecto se evaluaron dos alternativas: una arquitectura monolítica vs. microservicios.

**Decisión**: Se optó por una arquitectura de microservicios.

**Justificación**:

- *Pendiente de completar*
- *Pendiente de completar*
- *Pendiente de completar*

**Consecuencias**:

- ✅ *Beneficio 1*
- ✅ *Beneficio 2*
- ⚠️ *Trade-off 1*
- ⚠️ *Trade-off 2*

---

### Elección del Stack Tecnológico

<!-- TODO: Completar con la justificación de cada tecnología -->

**Contexto**: Se necesitaba elegir las tecnologías para cada componente del sistema.

| Componente | Tecnología Elegida | Alternativas Consideradas | Razón de Elección |
|------------|-------------------|---------------------------|-------------------|
| Mobile App | React Native | Flutter, Native | *Pendiente* |
| Admin Backoffice | Next.js | Create React App, Vue.js | *Pendiente* |
| Songs Service | Python/Flask | FastAPI, Django | *Pendiente* |
| Users Service | Go | Node.js, Python | *Pendiente* |
| Admin Service | Go | Node.js, Python | *Pendiente* |

**Criterios de decisión**:

1. Experiencia previa del equipo
2. Performance requerida
3. Ecosistema y comunidad
4. Facilidad de deployment en GCP

---

### Estrategia de Autenticación (JWT)

<!-- TODO: Completar con detalles de implementación -->

**Contexto**: Se necesitaba implementar autenticación para todos los servicios.

**Decisión**: Usar JSON Web Tokens (JWT) para autenticación stateless.

**Implementación**:

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Client    │────▶│ Users Service│────▶│   JWT Token │
└─────────────┘     └──────────────┘     └─────────────┘
       │                                        │
       │                                        ▼
       │            ┌──────────────┐     ┌─────────────┐
       └───────────▶│ Songs Service│◀────│  Validate   │
                    └──────────────┘     └─────────────┘
```

**Consideraciones de seguridad**:

- Tiempo de expiración del token: *pendiente*
- Refresh token strategy: *pendiente*
- Almacenamiento en cliente: *pendiente*

---

### Manejo de Archivos Multimedia

<!-- TODO: Completar con estrategia de almacenamiento -->

**Contexto**: Las canciones y portadas necesitan almacenamiento escalable y eficiente para streaming.

**Decisión**: Usar Google Cloud Storage con URLs firmadas.

**Flujo de subida**:

1. Cliente solicita URL de subida al Songs Service
2. Songs Service genera URL firmada con permisos de escritura
3. Cliente sube archivo directamente a GCS
4. Songs Service registra metadata en la base de datos

**Flujo de streaming**:

1. Cliente solicita canción
2. Songs Service genera URL firmada con tiempo de expiración
3. Cliente reproduce desde URL firmada

!!! warning "Pendiente"
    Definir estrategia de transcoding y formatos soportados.

---

### Base de Datos por Servicio vs Compartida

<!-- TODO: Completar con justificación -->

**Contexto**: Evaluar si cada microservicio debería tener su propia base de datos o compartir una única instancia.

**Decisión**: Cada servicio tiene su propia base de datos PostgreSQL.

**Justificación**:

- *Pendiente de completar*

**Consecuencias**:

- Necesidad de mantener consistencia eventual entre servicios
- Mayor complejidad operacional
- Mejor aislamiento y escalabilidad independiente

---

## Lecciones Aprendidas

### Técnico

| # | Problema Encontrado | Solución Aplicada | Aprendizaje |
|---|---------------------|-------------------|-------------|
| 1 | <!-- TODO --> *Problema técnico 1* | *Solución aplicada* | *Qué aprendimos* |
| 2 | <!-- TODO --> *Problema técnico 2* | *Solución aplicada* | *Qué aprendimos* |
| 3 | <!-- TODO --> *Problema técnico 3* | *Solución aplicada* | *Qué aprendimos* |

### Proceso

| # | Problema Encontrado | Solución Aplicada | Aprendizaje |
|---|---------------------|-------------------|-------------|
| 1 | <!-- TODO --> *Problema de proceso 1* | *Solución aplicada* | *Qué aprendimos* |
| 2 | <!-- TODO --> *Problema de proceso 2* | *Solución aplicada* | *Qué aprendimos* |

### Comunicación

| # | Problema Encontrado | Solución Aplicada | Aprendizaje |
|---|---------------------|-------------------|-------------|
| 1 | <!-- TODO --> *Problema de comunicación 1* | *Solución aplicada* | *Qué aprendimos* |
| 2 | <!-- TODO --> *Problema de comunicación 2* | *Solución aplicada* | *Qué aprendimos* |

---

## Registro de Decisiones (ADR Log)

Para decisiones más detalladas, seguimos el formato de Architecture Decision Records (ADR).

| ID | Fecha | Título | Estado |
|----|-------|--------|--------|
| ADR-001 | *Pendiente* | Elección de arquitectura de microservicios | Aceptada |
| ADR-002 | *Pendiente* | Estrategia de autenticación con JWT | Aceptada |
| ADR-003 | *Pendiente* | Uso de Cloud Storage para multimedia | Aceptada |

<!-- TODO: Crear ADRs detallados en carpeta docs/adrs/ si se decide usar este formato -->

!!! tip "Formato ADR"
    Si el equipo decide documentar decisiones en formato ADR completo, se creará una carpeta `docs/adrs/` con documentos individuales por decisión.
