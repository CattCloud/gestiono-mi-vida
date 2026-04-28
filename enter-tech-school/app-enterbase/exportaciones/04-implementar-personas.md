---
tags:
  - enter-tech-school
  - app-enterbase
  - exportaciones
  - completada
tipo: tarea
peso: 2
fecha_tipo: exacta
fecha_inicio: 2026-04-19
fecha_fin:
fecha_completado: 2026-04-19
orden: 4
bloqueada_por:
  - 03-presentacion-avance
desbloquea:
  - 05-implementar-seccion-alumnos
---

# 📄 04 — Implementar exportación: Personas

## Detalle

Implementar la exportación de **Personas** aprobada por el equipo el 15-abr. Debe generar Excel (.xlsx) con el formato validado (ver Excel propuesto guardado en Drive).

Primera de las dos exportaciones del par inicial que va a producción. Al terminar esta, arranca la de Sección > Alumnos.

## Contexto para la IA

**Stack:** Next.js + Prisma + PostgreSQL. La exportación debe generar Excel (.xlsx) con las columnas definidas en el doc de propuesta aprobado el 15-abr.

**Plan:** ejecutar secuencialmente hoy (19-abr). Primero Personas, luego Sección > Alumnos. Esta tarea se partió de la original `04-implementar-seccion-personas` (peso 3) para bajar peso y tener tracking de avance por feature.

**Por qué peso 2:** una sola exportación aislada. Requiere tiempo y cuidado (primera que sale a producción), pero acotada en alcance.

## Notas

- Al completarse, se desbloquea `05-implementar-seccion-alumnos`.
- Gaby va a probar cuando ambas estén subidas (tarea `06-probar-con-gaby`).

## Tarea (CardBoard)

- [x] 🟣 Implementar exportación: Personas 📅 2026-04-19 ✅ 2026-04-19
