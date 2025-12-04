# ⚠️ Problemas Conocidos y Features Incompletas

Esta sección documenta las funcionalidades incompletas, errores conocidos y deuda técnica identificada en el sistema al momento de la entrega final.

---

## Funcionalidades Incompletas

Las siguientes funcionalidades están parcialmente implementadas o pendientes de completar:

| Feature                  | Estado         | Descripción                    | Razón                                    |
| ------------------------ | -------------- | ------------------------------ | ---------------------------------------- |
| 🔔 Notificaciones Push   | 🟡 Parcial     | Solo funciona en Android       | Configuración de APNs pendiente para iOS |
| 📊 Dashboard de Artistas | 🔴 No iniciado | Estadísticas de reproducciones | Priorizado para Checkpoint 4             |
| 🔍 Búsqueda Avanzada     | 🟡 Parcial     | Solo búsqueda por nombre       | Falta implementar filtros                |
| 📱 Modo Offline          | 🔴 No iniciado | Descarga de canciones          | Fuera del alcance del MVP                |

<!-- TODO: Actualizar tabla con funcionalidades reales incompletas -->

### Leyenda de Estados

- 🟢 **Completo**: Funcionalidad completamente implementada y testeada
- 🟡 **Parcial**: Funcionalidad parcialmente implementada
- 🔴 **No iniciado**: Funcionalidad planificada pero no iniciada

---

## Errores Conocidos

Bugs identificados que aún no han sido corregidos:

| Bug                   | Severidad | Impacto                   | Workaround             |
| --------------------- | --------- | ------------------------- | ---------------------- |
| <!-- TODO --> _Bug 1_ | 🔴 Alta   | _Descripción del impacto_ | _Workaround si existe_ |
| <!-- TODO --> _Bug 2_ | 🟡 Media  | _Descripción del impacto_ | _Workaround si existe_ |
| <!-- TODO --> _Bug 3_ | 🟢 Baja   | _Descripción del impacto_ | _Workaround si existe_ |

<!-- TODO: Actualizar tabla con bugs reales identificados -->

### Severidad

- 🔴 **Alta**: Afecta funcionalidad crítica, bloquea uso normal
- 🟡 **Media**: Afecta experiencia de usuario pero hay workaround
- 🟢 **Baja**: Inconveniente menor, no afecta funcionalidad principal

---

## Deuda Técnica

Items identificados que requieren refactorización o mejora:

### Backend

- [ ] **Songs Service**: Refactorizar manejo de errores
- [ ] **Users Service**: Implementar rate limiting
- [ ] **Admin Service**: Agregar paginación a endpoints de listado
- [ ] **General**: Estandarizar formato de logs entre servicios

<!-- TODO: Actualizar con deuda técnica real -->

### Frontend

- [ ] **Mobile App**: Optimizar re-renders en listas largas
- [ ] **Admin Backoffice**: Agregar manejo de errores global

<!-- TODO: Actualizar con deuda técnica real -->

### Infraestructura

- [ ] **CI/CD**: Agregar ambiente de staging
- [ ] **Monitoreo**: Configurar alertas en Cloud Monitoring
- [ ] **Base de datos**: Configurar backups automáticos

<!-- TODO: Actualizar con deuda técnica real -->
