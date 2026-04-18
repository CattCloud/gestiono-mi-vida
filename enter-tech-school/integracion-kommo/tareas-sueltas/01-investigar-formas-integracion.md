---
tags:
  - enter-tech-school
  - integracion-kommo
tipo: tarea
peso: 3
estado: completada
fecha_tipo: exacta
fecha_inicio: 2026-04-17
fecha_fin:
fecha_completado: 2026-04-17
orden: 1
bloqueada_por:
desbloquea:
  - 02-redactar-doc-propuesta
---

# 📄 01 — Investigar formas de integrar Kommo con Enterbase

## Detalle

Investigar todas las formas posibles de comunicar Kommo con Enterbase:
- API privada
- Webhooks
- Import/export
- Intermediarios
- Otros mecanismos

Evaluar pros y contras de cada enfoque considerando el contexto del equipo (no siempre hay recursos para integraciones complejas) y la naturaleza de los datos.

## Contexto para la IA

La primera propuesta fue la API privada (https://developers.kommo.com/docs/private-integration). Esta tarea no es para implementarla, sino para decidir cuál es el camino correcto antes de implementar.

**Stack:** Next.js + Prisma + PostgreSQL en Enterbase. Kommo expone API REST con autenticación privada.

**Por qué peso 3:** investigación abierta con múltiples caminos, requiere comparar opciones, evaluar trade-offs técnicos y organizacionales, y llegar a una propuesta fundamentada. Complejidad alta.

## Notas

- Completada el 17-abr, mismo día de la reunión. Ver doc siguiente (tarea 02).

## Tarea (CardBoard)

- [x] 🟠 Investigar formas posibles de comunicar Kommo con Enterbase (API, webhooks, import/export, intermediarios) 📅 2026-04-17 ✅ 2026-04-17
