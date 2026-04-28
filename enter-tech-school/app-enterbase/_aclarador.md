---
tags:
  - enter-tech-school
  - mision
  - app-enterbase
tipo: mision
---

# 🎯 App Enterbase

## Aclarador

App Enterbase es el sistema interno de Enter Tech School. Es la aplicación principal donde se gestionan estudiantes, instructores, secciones y todo lo operativo de la escuela.

El proyecto más inmediato es el **formulario de registro de matriculados V2**, que digitaliza el Excel que se usaba para registrar matrículas. En la reunión del 13-abr-2026 el equipo aprobó el formulario con un ajuste: reordenar las secciones para que datos personales vayan primero e inscripción + pagos al final. Queda pendiente el deploy final a producción.

**Incidente del deploy (15-abr-2026):** El intento de subir el formulario a producción falló. Al integrar el PR, la app cayó porque no se corrió `npx prisma migrate deploy` en producción — el schema nuevo llegó sin la migración de BD (tabla nueva + campos adicionales). Ya se revirtió y la app está estable. Para el próximo intento se generó un documento con los cambios de BD para facilitar la aprobación de Bruno.

La funcionalidad de **exportación/descargables** también está en desarrollo. El 15-abr el equipo validó el formato de los Excel (Personas y Sección > Alumnos). Plan: avanzar implementación jueves 16-abr y subir viernes 17-abr para que Gaby lo pruebe y lo use oficialmente desde la próxima semana.

**Orden de prioridad exportaciones:** 1) Sección > Alumnos, 2) Personas, 3) Leads, 4) Pagos, 5) Encuestas, 6) Canvas.

También se definieron funcionalidades para la siguiente versión (V2): matricular estudiantes antiguos (solo curso + inscripción + pago, necesario para mayo), editar datos de estudiantes, ver detalle completo en página dedicada, V2 del exportable con filtros previos, y marcar asistencia múltiple desde el calendario.

**Prioridad post-descargables (acordada con Mhitzy):**
1. Registro de asistencias y entregables en Enterbase (acción múltiple desde calendario/clase).
2. Integración con Kommo — ver misión `integracion-kommo`.
3. Integración con Blackboard vía API — ver misión `migracion-blackboard`.

## Sub-misiones activas

- [[formulario-matriculados/_aclarador|📂 Formulario de matriculados]] — ✅ 5/5 completada (en producción desde 21-abr)
- [[exportaciones/_aclarador|📂 Exportaciones / Descargables]] — 10 tareas (4 completadas, 6 pendientes)
- [[acciones-multiples/_aclarador|📂 Acciones múltiples (Asistencia / Entregables)]] — 4 tareas (planificación hoy 21-abr)
- [[v2-funcionalidades/_aclarador|📂 V2 — Siguientes funcionalidades]] — 4 tareas futuras

## Tareas sueltas

(Ninguna por ahora — todas las tareas viven en sub-misiones.)

## Notas generales

- El formulario actual toca la base de datos (nuevos campos/tabla), por eso el testeo es delicado y no se puede subir directamente.
- Para departamentos/distritos: solo Lima tiene desplegable de distritos. Se evaluó usar una API pero por seguridad (app privada) se descartó de momento. Los demás departamentos usan campo de texto.
- Estudiantes duplicados: los datos personales se registran UNA vez. Lo que cambia entre inscripciones es el curso, tipo de matrícula y pago.
