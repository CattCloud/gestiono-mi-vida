---
tags:
  - enter-tech-school
  - app-enterbase
---
# App Enterbase

## Aclarador

App Enterbase es el sistema interno de Enter Tech School. Es la aplicación principal donde se gestionan estudiantes, instructores, secciones y todo lo operativo de la escuela.

El proyecto más inmediato es el **formulario de registro de matriculados V2**, que digitaliza el Excel que se usaba para registrar matrículas. En la reunión del 13-abr-2026 el equipo aprobó el formulario con un ajuste: reordenar las secciones para que datos personales vayan primero e inscripción + pagos al final. Queda pendiente el testeo antes de subirlo a producción.

También se definieron funcionalidades para la siguiente versión (V2):
- **Matricular estudiantes antiguos:** Para alumnos que ya están en el sistema, solo pedir curso + inscripción + pago, sin repetir datos personales. Esto se necesita para mayo porque empezarán a llegar estudiantes recurrentes.
- **Editar datos de estudiantes:** Abrir el formulario completo del estudiante en una nueva página con opción de editar.
- **Ver detalle completo del estudiante:** Ampliar la vista actual de "ver detalle" para mostrar toda la información en una página dedicada, no en el modal lateral que se cierra fácil.

La funcionalidad de **exportación/descargables** también está en desarrollo. Se envió un documento de Drive con consultas por área. La mayoría del equipo ya respondió — solo queda pendiente la respuesta de Pagos. La presentación de avance (Sección/Alumnos y Personas) será mañana 15-abr-2026 a las 3 PM por Meet.

El orden de prioridad para avanzar las exportaciones es: 1) Sección > Alumnos, 2) Personas, 3) Leads (mejora), 4) Pagos, 5) Encuestas, 6) Canvas.

**Sección > Alumnos:** Ya avanzada. Se analizó, se generó documento de propuesta y Excel de propuesta para Gabriela. La reunión de mañana definirá qué datos se pueden ver en la exportación, y luego se procede con la implementación.

**Personas:** Recién arranca. Ya se tienen las respuestas — toca analizarlas con IA, generar documento de propuesta y Excel propuesta para presentar en la misma reunión del 15-abr.

Los demás (Leads, Pagos, Encuestas, Canvas) se avanzan cuando estén resueltas sus consultas. Pagos en particular espera respuesta del equipo.

## Tareas

### Formulario de matriculados (V1 → producción)
- [x] Cambiar orden de secciones del formulario: datos personales primero, inscripción y pagos al final (14-abr-2026) 📅 2026-04-14 @completed(2026-04-14T12:40:51-05:00)
- [x] Testear formulario de matriculados — pruebas completas incluyendo cambios en base de datos (14-abr-2026) 📅 2026-04-14
- [ ] Subir formulario de matriculados a producción (15-abr-2026) 📅 2026-04-15 @completed(2026-04-14T15:54:09-05:00)

### Exportación / Descargables
- [x] Esperar respuestas del equipo sobre consultas de exportación (doc de Drive) ✅
- [ ] Esperar respuesta de consultas de exportación de Pagos ⏳
- [ ] Análisis de exportación: Personas — analizar respuestas con IA, generar documento de propuesta y Excel propuesta (15-abr-2026) 📅 2026-04-15
- [ ] Presentación avance de descargables/exportación: Sección/Alumnos y Personas — reunión mañana 3 PM por Meet (15-abr-2026) 📅 2026-04-15
- [ ] Implementación de exportación: Sección > Alumnos — después de la reunión ⏳
- [ ] Análisis de exportación: Leads (mejora) — filtros y formato Excel ⏳
- [ ] Análisis de exportación: Pagos — depende de respuesta pendiente ⏳
- [ ] Análisis de exportación: Encuestas ⏳
- [ ] Análisis de exportación: Canvas ⏳

### V2 — Siguiente versión
- [ ] Matricular estudiantes antiguos: formulario solo con curso + inscripción + pago (sin datos personales). Necesario para mayo ⏳
- [ ] Editar datos de estudiantes existentes: formulario completo con opción de editar en nueva página ⏳
- [ ] Ver detalle completo del estudiante: toda la info en página dedicada en lugar del modal lateral ⏳

## Notas

- El formulario actual toca la base de datos (nuevos campos/tabla), por eso el testeo es delicado y no se puede subir directamente. 
- Para departamentos/distritos: por ahora solo Lima tiene desplegable de distritos. Se evaluó usar una API pero por seguridad (app privada) se descartó de momento. Los demás departamentos usan campo de texto. 
- Estudiantes duplicados: se acordó que los datos personales se registran UNA vez. Lo que cambia entre inscripciones es el curso, tipo de matrícula y pago.
