---
tags:
  - enter-tech-school
  - app-enterbase
  - exportaciones
  - completada
tipo: tarea
peso: 1
fecha_tipo: exacta
fecha_inicio: 2026-04-22
fecha_fin:
fecha_completado: 2026-04-22
orden: 5
bloqueada_por:
desbloquea:
  - 05b-implementar-seccion-alumnos
---

# 📄 05a — Planear exportación: Sección > Alumnos

## Detalle

Planear la implementación de la exportación **Sección > Alumnos**. Bajar a papel:
- Qué columnas exactas va a tener el Excel (.xlsx) según lo aprobado el 15-abr y la modificación del 19-abr sobre Pagos.
- Estructura de la query: qué tablas se cruzan, filtros, orden.
- Dónde va el botón/endpoint en Next.js.
- Qué validaciones y casos de borde (sección vacía, alumnos sin pagos, etc.).

Originalmente esta planeación iba fusionada con la implementación en la tarea `05-implementar-seccion-alumnos` con fecha 21-abr, pero se partió en dos: planeación hoy (22-abr), implementación después.

## Contexto para la IA

**Stack:** Next.js + Prisma + PostgreSQL. La implementación previa de Personas (tarea 04) ya validó el pipeline — acá no hay tecnología nueva, solo un diseño concreto para esta exportación específica.

**Modificación acordada en la exposición del 19-abr:** en la sección de Pagos del Excel de Sección > Alumnos, mostrar solamente el **primer pago** y la **URL del voucher**. Los demás campos (monto total, etc.) NO van acá — irán en el Excel de Pagos cuando se trabaje esa exportación.

**Por qué peso 1:** planeación aislada, una sola sesión de pensamiento. No requiere investigación nueva porque el pipeline de Personas ya está validado y las columnas están definidas en el doc del 15-abr. El trabajo es consolidar el diseño antes de codificar.

## Notas

- Formato validado en el doc de Drive del 15-abr (Excel propuesto).
- Al completarse, se desbloquea `05b-implementar-seccion-alumnos`.

## Tarea (CardBoard)

- [x] 🟡 Planear exportación: Sección > Alumnos 📅 2026-04-22 ✅ 2026-04-22
