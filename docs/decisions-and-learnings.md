# 💡 Decisiones de Arquitectura

Esta sección documenta las decisiones de arquitectura de alto nivel tomadas durante el desarrollo de Melodia. Las decisiones específicas de cada servicio se encuentran en sus respectivas páginas de documentación, y los aprendizajes por checkpoint se encuentran en la sección de [Roadmap](checkpoints/checkpoint-1.md).

---

## ¿Por qué Microservicios?

**Contexto**: Al inicio del proyecto se evaluaron dos alternativas: una arquitectura monolítica vs. microservicios.

**Decisión**: Se optó por una arquitectura de microservicios.

**Justificación**:

Decidimos utilizar una arquitectura basada en microservicios debido a que esta nos permite realizar más escalable en comparación a la monolítica debido a la flexibilidad que tiene al agregar nuevas funcionalidades. Así mismo, es ideal para el desarrollo el paralelo entre integrantes de un grupo y permite incorporar lenguajes o tecnologías distintas y acoplarlos perfectamente.
En nuestro caso, contamos con tres microservicios distintos:
- El primero es para usuarios, utilizando el lenguaje GO.
- El segundo es de Colecciones, implementado con Python.
- El tercero es exclusivo para el BackOffiece, el cual también fue desarrollado en Go

**Consecuencias**:

- ✅ Permitió desarrollar funcionalidades distintas más rápidamente.
- ✅ Estas funcionalidades no necesariamente estaban relacionadas, por lo que había una mejor división de tareas por parte del equipo del Frontend.
- ✅ El proyecto es más escalable y entendible debido a que esta separados por módulos distintos.
- ⚠️ En determinados momentos podía ocurrir de que se implementan menos funcionalidades de un determinado microservicio, por lo que uno de los integrantes estaba más ocupado el otro.
- ⚠️ Como principal desventaja, si alguno de los integrantes del BackEnd no podía realizar una determinada funcionalidad perteneciente a un microservicio especifico, era complicado que reciba ayuda de algún integrante.

---

## Elección del Stack Tecnológico

- Mobile App: Por parte de la catedra, como Tecnología del FrontEnd se debía utilizar obligatoriamente React Native debido a la curva de aprendizaje y versatilidad con respecto a la conexión con el backend.
- Admin BackOffice: Es una tecnología análoga a React Native, pero para el desarrollo de web
- Songs Service: Se decidio utilizar debido a la facilidad y múltiples libreas con soporte que esta posee.
- User Service y Admin Service: Como caso particular, se utilizó Go debido a que uno de los integrantes del BackEnd está más familiarizado con el uso de la misma en Go.


**Contexto**: Se necesitaba elegir las tecnologías para cada componente del sistema.

| Componente       | Tecnología Elegida | Alternativas Consideradas | Razón de Elección |
| ---------------- | ------------------ | ------------------------- | ----------------- |
| Mobile App       | React Native       | Flutter, Native           | Obligatorio       |
| Admin Backoffice | Next.js            | Create React App, Vue.js  | Conveniencia      |
| Songs Service    | Python/Flask       | FastAPI, Django           | Versatilidad      |
| Users Service    | Go                 | Node.js, Python           | Familiaridad      |
| Admin Service    | Go                 | Node.js, Python           | Familiaridad      |

**Criterios de decisión**:

1. Experiencia previa del equipo
2. Performance requerida
3. Ecosistema y comunidad
4. Facilidad de deployment en GCP
5. Practicidad en desarrollo
6. Tiempo de entrega dado
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

Decidimos utilizar las siguinetes base de datos por servicio:

- Usuarios: Se utilizo MySQL para el modelado.
- Colecciones: Se uso PostreSQL para modelerlas.
- Canciones: Utilizamos el storage de GCP con un enfoque no relacional.

**Contexto**: Evaluar si cada microservicio debería tener su propia base de datos o compartir una única instancia.

**Decisión**: Cada servicio tiene su propia base de datos PostgreSQL.

**Justificación**:



**Consecuencias**:

- Necesidad de mantener consistencia eventual entre servicios
- Mayor complejidad operacional
- Mejor aislamiento y escalabilidad independiente
