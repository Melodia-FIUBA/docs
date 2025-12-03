# ⚠️ Problemas Conocidos

Esta sección documenta las funcionalidades incompletas, errores conocidos y deuda técnica identificada en el sistema. El objetivo es mantener transparencia sobre el estado actual del proyecto.

!!! warning "Actualización"
    Esta página debe actualizarse regularmente conforme se identifican y resuelven problemas.

---

## Funcionalidades Incompletas

Las siguientes funcionalidades están parcialmente implementadas o pendientes de completar:

| Feature | Estado | Descripción | Razón |
|---------|--------|-------------|-------|
| 🔔 Notificaciones Push | 🟡 Parcial | Solo funciona en Android | Configuración de APNs pendiente para iOS |
| 📊 Dashboard de Artistas | 🔴 No iniciado | Estadísticas de reproducciones | Priorizado para Checkpoint 4 |
| 🔍 Búsqueda Avanzada | 🟡 Parcial | Solo búsqueda por nombre | Falta implementar filtros y búsqueda por letra |
| 📱 Modo Offline | 🔴 No iniciado | Descarga de canciones | Fuera del alcance del MVP |
| 🎨 Temas de la App | 🟡 Parcial | Solo modo claro disponible | Modo oscuro en desarrollo |
| 📤 Compartir en Redes | 🔴 No iniciado | Compartir canciones/playlists | Depende de deep linking |

<!-- TODO: Actualizar tabla con funcionalidades reales incompletas -->

### Leyenda de Estados

- 🟢 **Completo**: Funcionalidad completamente implementada y testeada
- 🟡 **Parcial**: Funcionalidad parcialmente implementada
- 🔴 **No iniciado**: Funcionalidad planificada pero no iniciada

---

## Errores Conocidos

Bugs identificados que aún no han sido corregidos:

| Bug | Severidad | Impacto | Workaround |
|-----|-----------|---------|------------|
| <!-- TODO --> Login falla intermitentemente | 🔴 Alta | Usuarios no pueden acceder | Reintentar login después de 30s |
| <!-- TODO --> Imagen de perfil no se actualiza | 🟡 Media | UX afectada | Cerrar y abrir la app |
| <!-- TODO --> Playlist duplicada al crear rápido | 🟡 Media | Datos inconsistentes | Esperar a que se complete antes de crear otra |
| <!-- TODO --> Timeout en búsqueda | 🟢 Baja | Búsqueda lenta | Usar términos más específicos |
| <!-- TODO --> Scroll lag en lista larga | 🟢 Baja | Performance afectada | Ninguno disponible |

<!-- TODO: Actualizar tabla con bugs reales identificados -->

### Severidad

- 🔴 **Alta**: Afecta funcionalidad crítica, bloquea uso normal
- 🟡 **Media**: Afecta experiencia de usuario pero hay workaround
- 🟢 **Baja**: Inconveniente menor, no afecta funcionalidad principal

---

## Deuda Técnica

Items identificados que requieren refactorización o mejora:

### Backend

- [ ] **Songs Service**: Refactorizar manejo de errores para usar patrón consistente
- [ ] **Songs Service**: Agregar índices a queries lentas en búsqueda
- [ ] **Songs Service**: Implementar caché de Redis para queries frecuentes
- [ ] **Users Service**: Mejorar validación de inputs en endpoints
- [ ] **Users Service**: Implementar rate limiting
- [ ] **Admin Service**: Agregar paginación a endpoints de listado
- [ ] **General**: Estandarizar formato de logs entre servicios
- [ ] **General**: Implementar tracing distribuido

<!-- TODO: Actualizar con deuda técnica real -->

### Frontend

- [ ] **Mobile App**: Migrar componentes de clase a funcionales con hooks
- [ ] **Mobile App**: Implementar lazy loading de imágenes
- [ ] **Mobile App**: Optimizar re-renders en listas
- [ ] **Admin Backoffice**: Agregar manejo de errores global
- [ ] **Admin Backoffice**: Implementar tests de componentes
- [ ] **General**: Unificar sistema de diseño entre apps

<!-- TODO: Actualizar con deuda técnica real -->

### Infraestructura

- [ ] **CI/CD**: Agregar ambiente de staging
- [ ] **CI/CD**: Implementar tests de integración en pipeline
- [ ] **Monitoreo**: Configurar alertas en Cloud Monitoring
- [ ] **Seguridad**: Implementar rotación automática de secrets
- [ ] **Base de datos**: Configurar backups automáticos
- [ ] **Base de datos**: Implementar migrations automáticas en deploy

<!-- TODO: Actualizar con deuda técnica real de infraestructura -->

---

## Limitaciones Conocidas

Restricciones del sistema que no son bugs pero afectan la funcionalidad:

### Límites de Archivo

| Recurso | Límite | Razón |
|---------|--------|-------|
| Tamaño máximo de canción | 50 MB | Límite de Cloud Storage upload |
| Duración máxima de canción | 15 minutos | Definido en requerimientos |
| Tamaño de imagen de perfil | 5 MB | Optimización de storage |
| Canciones por playlist | 500 | Performance de queries |

### Límites de Rate

| Endpoint | Límite | Ventana |
|----------|--------|---------|
| Login | 5 intentos | 15 minutos |
| Registro | 3 cuentas | Por IP/hora |
| Upload de canción | 10 canciones | Por día |
| Búsqueda | 100 requests | Por minuto |

<!-- TODO: Actualizar con límites reales del sistema -->

---

## Proceso de Reporte

Para reportar nuevos problemas:

1. **Verificar** que el problema no esté ya documentado
2. **Crear issue** en el repositorio correspondiente
3. **Incluir**:
    - Pasos para reproducir
    - Comportamiento esperado vs actual
    - Screenshots si aplica
    - Ambiente (dispositivo, OS, versión de app)
4. **Etiquetar** con severidad apropiada
5. **Actualizar** esta documentación si es un problema conocido

!!! tip "Priorización"
    Los bugs de severidad alta se priorizan sobre nuevas funcionalidades. La deuda técnica se aborda en sprints dedicados según disponibilidad.
