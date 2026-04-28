---
tags:
  - enter-tech-school
  - app-enterbase
  - sub-mision
  - acciones-multiples
tipo: sub-mision
mision_padre: app-enterbase
---

# 📂 Acciones múltiples (Asistencia / Entregables)

## Aclarador

Sub-misión dentro de app-enterbase para implementar **acciones múltiples** desde el calendario de clases. Hoy Gaby entra alumno por alumno, módulo por módulo — flujo tedioso. La feature permite marcar asistencia o entregables a varios estudiantes a la vez con UI tipo Gmail (checkboxes + botón de acción batch).

Esta sub-misión nace de la reunión del **27-mar-2026 con Mhitzy**. Originalmente vivía como una sola tarea en `v2-funcionalidades`, pero como abarca dos features (Asistencia + Entregables) que comparten UI y contexto, y cada una requiere planificación + implementación, se separa como sub-misión propia.

## Contexto de la reunión (27-mar-2026)

**Acceso:** desde el calendario de clases. Al hacer clic en una sesión (ej: Code 301), aparecen dos botones/íconos al costado:
- **A** → Asistencia
- **E** → Entregables

**Comportamiento:** al pulsar el botón se abre la lista de estudiantes (vista flotante o página nueva — a definir). El usuario marca checkboxes (uno, varios, o "seleccionar todos") y arriba un botón de acción batch: "Marcar asistencia" / "Marcar fallas" / "Marcar entregados". Se registra y el dashboard se actualiza automáticamente.

**Referencia visual:** plataforma de gestión de correos tipo Gmail — checkboxes + acción masiva con etiquetas.

**Casos de uso:**
- Asistencia: se marca el mismo día de la clase. Hoy lo hace Gaby; en el futuro debería hacerlo el docente (solo verá su propio calendario).
- Entregables: Gaby los marca al día siguiente (no el mismo día) porque los plazos de entrega dan margen.

**Consideraciones de diseño:**
- Botones notables, no perderse en la interfaz.
- Mobile: dos botones pequeños son difíciles de presionar — pedir sugerencias específicas para iOS/Android.
- Decisión pendiente: vista flotante vs página nueva.

**Stack:** Next.js + Prisma + PostgreSQL. UI nueva + endpoint batch eficiente.

## Estrategia

Secuencial: primero Asistencia (planificar → implementar), luego Entregables (planificar → implementar). La planificación de cada uno es con IA (propuestas, preguntas, decisiones de diseño). Como la UI es la misma, lo aprendido en asistencia acelera entregables.

## Tareas

- [[01-planificar-asistencia|📄 01 — Planificar asistencia múltiple]] — peso 2 🟣 ✅ completada (21-abr)
- [[02-implementar-asistencia|📄 02 — Implementar asistencia múltiple]] — peso 2 🟣 ✅ completada (23-abr)
- [[03-planificar-entregables|📄 03 — Planificar entregables múltiples]] — peso 2 🟣 📅 pendiente (hoy 24-abr)
- [[04-implementar-entregables|📄 04 — Implementar entregables múltiples]] — peso 2 🟣 🔒 bloqueada por 03

## Notas

- Esta feature aplica solo a cursos que sigan en Enterbase/Canvas. Para los cursos migrados a Blackboard, asistencia/entregables se manejan vía la API de Blackboard (ver misión `migracion-blackboard`).
- Hablar con Gaby sobre casos de borde: ¿qué pasa si se marca mal y hay que deshacer? ¿Se puede marcar inasistencia en bloque?
