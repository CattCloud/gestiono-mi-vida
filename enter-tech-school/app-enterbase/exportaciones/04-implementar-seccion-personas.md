---
tags:
  - enter-tech-school
  - app-enterbase
  - exportaciones
  - pendiente
tipo: tarea
peso: 3
fecha_tipo: exacta
fecha_inicio: 2026-04-18
fecha_fin:
fecha_completado:
orden: 4
bloqueada_por:
  - 03-presentacion-avance
desbloquea:
  - 05-probar-con-gaby
---

# 📄 04 — Implementar exportación: Sección > Alumnos y Personas

## Detalle

Implementar las dos exportaciones aprobadas por el equipo el 15-abr:
1. Sección > Alumnos
2. Personas

Deben generar Excel con el formato validado (ver Excel propuestos guardados en Drive). Esta es la primera pareja que va a producción.

## Contexto para la IA

**Stack:** Next.js + Prisma + PostgreSQL. La exportación debe generar Excel (.xlsx) con las columnas definidas en los docs de propuesta aprobados el 15-abr.

**Plan original:** implementar el 16-abr, subir el 17-abr. Por el incidente del deploy del formulario, la fecha se corrió un poco. Fecha actualizada: 18-abr.

**Por qué peso 3:** implementación completa de dos features (aunque paralelas), genera archivos que requieren formato validado, es el primer par que va a producción así que hay que tener cuidado con todo el pipeline de exportación.

## Notas

- Gaby va a probar una vez esté subido. Por eso la tarea siguiente es "probar con Gaby".
- Cuando esto esté listo, arranca la siguiente pareja (Leads + Encuestas).

## Tarea (CardBoard)

- [ ] 🟠 Implementar exportación: Sección > Alumnos y Personas 📅 2026-04-18
