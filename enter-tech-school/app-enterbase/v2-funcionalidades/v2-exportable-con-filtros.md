---
tags:
  - enter-tech-school
  - app-enterbase
  - v2-funcionalidades
tipo: tarea
peso: 3
estado: en-espera
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden:
bloqueada_por:
desbloquea:
---

# 📄 V2 del exportable: filtros previos

## Detalle

Al darle a "exportar" en cualquier área, mostrar un desplegable con filtros previos (rango de fechas, alumnos específicos, etc.). El usuario aplica filtros y luego descarga el Excel con los datos filtrados.

## Contexto para la IA

La V1 del exportable (ver sub-misión `exportaciones/`) descarga todos los datos sin filtros. Esta mejora aplica una vez que la V1 esté estable y en uso en producción.

**Stack:** Next.js + Prisma + PostgreSQL. El filtrado se hace en backend antes de generar el Excel.

**Por qué peso 3:** feature transversal (aplica a todas las exportaciones), requiere UI de filtros, lógica de backend para cada tipo de filtro, y testeo por área. Complejidad alta.

## Notas

- Esta tarea asume que la V1 de exportaciones ya está en producción.

## Tarea (CardBoard)

- [ ] 🟠 V2 del exportable: desplegable con filtros previos (rango de fechas, alumnos, etc.) ⏳
