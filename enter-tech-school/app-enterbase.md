---
tags:
  - enter-tech-school
  - app-enterbase
---
# App Enterbase

## Aclarador

App Enterbase es el sistema interno de Enter Tech School. Es la aplicación principal donde se gestionan estudiantes, instructores, secciones y todo lo operativo de la escuela.

El proyecto más inmediato es el **formulario de registro de matriculados V2**, que digitaliza el Excel que se usaba para registrar matrículas. En la reunión del 13-abr-2026 el equipo aprobó el formulario con un ajuste: reordenar las secciones para que datos personales vayan primero e inscripción + pagos al final. Queda pendiente el testeo antes de subirlo a producción.

**Incidente del deploy (15-abr-2026):** El intento de subir el formulario a producción falló. Al integrar el PR, la app cayó porque no se corrió `npx prisma migrate deploy` en producción — el schema nuevo llegó sin la migración de BD (tabla nueva + campos adicionales). Ya se revirtió el cambio y la app está estable. Para el próximo intento se necesita acceso al servidor de producción; se solicitó a Bruno, quien preguntó si era una tabla nueva. Se le confirmó que sí (tabla nueva + campos adicionales) y para facilitar su decisión se generará un documento breve con los cambios de BD antes de hacer el PR con request hacia su usuario.

También se definieron funcionalidades para la siguiente versión (V2):
- **Matricular estudiantes antiguos:** Para alumnos que ya están en el sistema, solo pedir curso + inscripción + pago, sin repetir datos personales. Esto se necesita para mayo porque empezarán a llegar estudiantes recurrentes.
- **Editar datos de estudiantes:** Abrir el formulario completo del estudiante en una nueva página con opción de editar.
- **Ver detalle completo del estudiante:** Ampliar la vista actual de "ver detalle" para mostrar toda la información en una página dedicada, no en el modal lateral que se cierra fácil.

La funcionalidad de **exportación/descargables** también está en desarrollo. Se envió un documento de Drive con consultas por área. La mayoría del equipo ya respondió — solo queda pendiente la respuesta de Pagos. La presentación de avance (Sección/Alumnos y Personas) será mañana 15-abr-2026 a las 3 PM por Meet.

El orden de prioridad para avanzar las exportaciones es: 1) Sección > Alumnos, 2) Personas, 3) Leads (mejora), 4) Pagos, 5) Encuestas, 6) Canvas.

**Sección > Alumnos:** Ya avanzada. Se analizó, se generó documento de propuesta y Excel de propuesta para Gabriela. La reunión de mañana definirá qué datos se pueden ver en la exportación, y luego se procede con la implementación.

**Personas:** Recién arranca. Ya se tienen las respuestas — toca analizarlas con IA, generar documento de propuesta y Excel propuesta para presentar en la misma reunión del 15-abr.

Los demás (Leads, Pagos, Encuestas, Canvas) se avanzan cuando estén resueltas sus consultas. Pagos en particular espera respuesta del equipo.

**Resultado de la reunión del 15-abr:** El equipo validó el formato de los Excel (Personas y Sección > Alumnos). Quedó aprobado avanzar. Plan: avanzar implementación el jueves 16-abr y subir viernes 17-abr en la mañana/tarde para que Gaby lo pruebe. Gaby lo usaría oficialmente desde la próxima semana; mientras tanto sigue calculando como lo venía haciendo con Cloud. Para los leads y encuestas se avanzarán como siguiente pareja (de dos en dos para no sobrecargar).

**Futuro V2 del exportable:** Al darle a exportar aparecería un desplegable con filtros previos (rango de fechas, alumnos, etc.); se aplican filtros y luego se descarga.

**Futuro — marcar asistencia múltiple:** Hoy Gaby entra alumno por alumno, módulo por módulo. Se planea una vista de acción múltiple desde el calendario/clase para marcar asistencia de varios a la vez. Con la migración a Blackboard este tema se resuelve aún mejor vía la API de Blackboard (ver misión `migracion-blackboard`), pero solo para los cursos migrados — los que sigan en Enterbase/Canvas necesitan mantener el registro manual facilitado.

**Prioridad post-descargables (acordada con Mhitzy):**
1. Registro de asistencias y entregables en Enterbase — acción múltiple desde calendario/clase (cursos no migrados a Blackboard).
2. Integración con Kommo — ver misión `integracion-kommo`.
3. Integración con Blackboard vía API — ver misión `migracion-blackboard`.

## Tareas

### Formulario de matriculados (V1 → producción)
- [x] Cambiar orden de secciones del formulario: datos personales primero, inscripción y pagos al final 📅 2026-04-14 ✅ 2026-04-14
- [x] Testear formulario de matriculados — pruebas completas incluyendo cambios en base de datos 📅 2026-04-14
- [x] Generar documento breve con los cambios de BD (tabla nueva + campos adicionales) para facilitar la decisión de Bruno 📅 2026-04-16 ✅ 2026-04-16
- [ ] Enviar documento a Bruno y esperar aprobación de acceso al servidor de producción ⏳
- [ ] Hacer PR con request hacia el usuario de Bruno — solo después de tener acceso/aprobación ⏳
- [ ] Subir formulario de matriculados a producción (correr `npx prisma migrate deploy` antes del merge) ⏳

### Exportación / Descargables
- [x] Esperar respuestas del equipo sobre consultas de exportación (doc de Drive) ✅
- [ ] Esperar respuesta de consultas de exportación de Pagos ⏳
- [x] Análisis de exportación: Personas — analizar respuestas con IA, generar documento de propuesta y Excel propuesta 📅 2026-04-15 ✅ 2026-04-15
- [x] Presentación avance de descargables/exportación: Sección/Alumnos y Personas — reunión mañana 3 PM por Meet 📅 2026-04-15 ✅ 2026-04-15
- [ ] Implementar exportación: Sección > Alumnos y Personas  📅 2026-04-18 
- [ ] Probar junto con Gaby la exportación implementada  ⏳
- [ ] Análisis de exportación: Leads (mejora) — filtros y formato Excel ⏳
- [ ] Análisis de exportación: Pagos — depende de respuesta pendiente ⏳
- [ ] Análisis de exportación: Encuestas ⏳
- [ ] Análisis de exportación: Canvas ⏳

### V2 — Siguiente versión
- [ ] Matricular estudiantes antiguos: formulario solo con curso + inscripción + pago (sin datos personales). Necesario para mayo ⏳
- [ ] Editar datos de estudiantes existentes: formulario completo con opción de editar en nueva página ⏳
- [ ] Ver detalle completo del estudiante: toda la info en página dedicada en lugar del modal lateral ⏳
- [ ] V2 del exportable: desplegable con filtros previos (rango de fechas, alumnos, etc.) antes de descargar ⏳
- [ ] Marcar asistencia múltiple desde el calendario/clase (acción múltiple) — elimina entrar alumno por alumno ⏳

## Notas

- El formulario actual toca la base de datos (nuevos campos/tabla), por eso el testeo es delicado y no se puede subir directamente. 
- Para departamentos/distritos: por ahora solo Lima tiene desplegable de distritos. Se evaluó usar una API pero por seguridad (app privada) se descartó de momento. Los demás departamentos usan campo de texto. 
- Estudiantes duplicados: se acordó que los datos personales se registran UNA vez. Lo que cambia entre inscripciones es el curso, tipo de matrícula y pago.
