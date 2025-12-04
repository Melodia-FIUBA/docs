# 💡 Decisiones de Arquitectura

Esta sección documenta las decisiones de arquitectura de alto nivel tomadas durante el desarrollo de Melodia. Las decisiones específicas de cada servicio se encuentran en sus respectivas páginas de documentación, y los aprendizajes por checkpoint se encuentran en la sección de [Roadmap](checkpoints/checkpoint-1.md).

---

## ¿Por qué Microservicios?

<!-- TODO: Completar con la justificación real del equipo -->

**Contexto**: Al inicio del proyecto se evaluaron dos alternativas: una arquitectura monolítica vs. microservicios.

**Decisión**: Se optó por una arquitectura de microservicios.

**Justificación**:

- _Pendiente de completar_

**Consecuencias**:

- ✅ _Beneficio 1_
- ✅ _Beneficio 2_
- ⚠️ _Trade-off 1_

---

## Elección del Stack Tecnológico

<!-- TODO: Completar con la justificación de cada tecnología -->

**Contexto**: Se necesitaba elegir las tecnologías para cada componente del sistema.

| Componente       | Tecnología Elegida | Alternativas Consideradas | Razón de Elección |
| ---------------- | ------------------ | ------------------------- | ----------------- |
| Mobile App       | React Native       | Flutter, Native           | _Pendiente_       |
| Admin Backoffice | Next.js            | Create React App, Vue.js  | _Pendiente_       |
| Songs Service    | Python/Flask       | FastAPI, Django           | _Pendiente_       |
| Users Service    | Go                 | Node.js, Python           | _Pendiente_       |
| Admin Service    | Go                 | Node.js, Python           | _Pendiente_       |

**Criterios de decisión**:

1. Experiencia previa del equipo
2. Performance requerida
3. Ecosistema y comunidad
4. Facilidad de deployment en GCP

---

## Estrategia de Autenticación (JWT)

<!-- TODO: Completar con detalles de implementación -->

**Contexto**: Se necesitaba implementar autenticación para todos los servicios.

**Decisión**: Usar JSON Web Tokens (JWT) para autenticación stateless.

**Implementación**:

- Users Service genera tokens JWT al login
- Otros servicios validan tokens consultando a Users Service
- Refresh tokens para renovación de sesión

**Consideraciones de seguridad**:

- Tiempo de expiración del token: _pendiente_
- Refresh token strategy: _pendiente_
- Almacenamiento en cliente: _pendiente_

---

## Manejo de Archivos Multimedia

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

---

## Base de Datos por Servicio

<!-- TODO: Completar con justificación -->

**Contexto**: Evaluar si cada microservicio debería tener su propia base de datos o compartir una única instancia.

**Decisión**: Cada servicio tiene su propia base de datos PostgreSQL.

**Justificación**:

- _Pendiente de completar_

**Consecuencias**:

- Necesidad de mantener consistencia eventual entre servicios
- Mayor complejidad operacional
- Mejor aislamiento y escalabilidad independiente
