---
tags:
  - enter-tech-school
  - app-enterbase
  - sub-mision
  - v2-funcionalidades
tipo: sub-mision
mision_padre: app-enterbase
---

# 📂 V2 — Siguientes funcionalidades

## Aclarador

Sub-misión dentro de app-enterbase. Agrupa las funcionalidades aprobadas para la siguiente versión del sistema, que se empezarán una vez el formulario de matriculados V2 esté en producción y las exportaciones principales también.

Todas son funcionalidades "futuras" sin fecha exacta todavía, excepto "matricular estudiantes antiguos" que tiene deadline blando en mayo.

**Prioridad interna sugerida:**
1. Matricular estudiantes antiguos (deadline mayo)
2. Ver detalle completo del estudiante
3. Editar datos de estudiantes existentes
4. V2 del exportable con filtros previos

## Tareas

- [[matricular-estudiantes-antiguos|📄 Matricular estudiantes antiguos]] — peso 3 🟠 ⏳ (mayo 2026)
- [[editar-datos-estudiantes|📄 Editar datos de estudiantes existentes]] — peso 3 🟠 ⏳
- [[ver-detalle-completo-estudiante|📄 Ver detalle completo del estudiante]] — peso 2 🟣 ⏳
- [[v2-exportable-con-filtros|📄 V2 del exportable: filtros previos]] — peso 3 🟠 ⏳

## Notas

- **(21-abr-2026)** La feature de asistencia/entregables múltiples se movió a su propia sub-misión `app-enterbase/acciones-multiples/` porque abarca dos features (asistencia + entregables) que comparten UI y requieren planificación + implementación cada una.
- La asistencia múltiple se resuelve vía Blackboard API para los cursos migrados (ver misión `migracion-blackboard`). La sub-misión `acciones-multiples` aplica solo para cursos que sigan en Enterbase/Canvas.
