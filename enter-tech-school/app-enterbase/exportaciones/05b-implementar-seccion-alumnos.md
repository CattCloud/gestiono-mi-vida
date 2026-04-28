---
tags:
  - enter-tech-school
  - app-enterbase
  - exportaciones
  - completada
tipo: tarea
peso: 2
fecha_tipo: exacta
fecha_inicio: 2026-04-23
fecha_fin:
fecha_completado: 2026-04-23
orden: 5
bloqueada_por:
  - 05a-planear-seccion-alumnos
desbloquea:
  - 05c-testear-personas-y-secciones
---

# 📄 05b — Implementar exportación: Sección > Alumnos

## Detalle

Implementar la exportación de **Sección > Alumnos** aprobada por el equipo el 15-abr, siguiendo el plan definido en `05a-planear-seccion-alumnos`. Debe generar Excel (.xlsx) con el formato validado (ver Excel propuesto guardado en Drive).

Segunda de las dos exportaciones del par inicial que va a producción. Arranca al completar `05a`.

## Contexto para la IA

**Stack:** Next.js + Prisma + PostgreSQL. La exportación debe generar Excel (.xlsx) con las columnas definidas en el doc de propuesta aprobado el 15-abr, siguiendo el diseño cerrado en `05a`.

**Historial:** esta tarea se partió de la original `04-implementar-seccion-personas` (peso 3) para bajar peso. Luego, el 22-abr, se volvió a partir en planeación (`05a`, peso 1) + implementación (este archivo, `05b`, peso 2) porque la planeación no se ejecutó el 21-abr y se trasladó a hoy.

**Por qué peso 2:** una sola exportación aislada. Ya el pipeline de Personas (04) validó la tecnología; acá solo hay que aplicar el diseño cerrado en `05a`.

## Notas

- **Modificación acordada en la exposición del 19-abr:** en la sección de Pagos del Excel, mostrar solamente el **primer pago** y la **URL del voucher**. Los demás campos (monto total, etc.) se sacan de este Excel — irán en el Excel de Pagos cuando se trabaje esa exportación.
- Al completarse, se desbloquea `05c-testear-personas-y-secciones` (testing técnico previo al PR).

## Tarea (CardBoard)

- [x] 🟣 Implementar exportación: Sección > Alumnos 📅 2026-04-23 ✅ 2026-04-23
