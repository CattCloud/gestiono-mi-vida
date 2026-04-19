---
tags:
  - enter-tech-school
  - app-enterbase
  - en-espera
tipo: tarea
peso: 2
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden:
bloqueada_por:
desbloquea:
---

# Limpiar logs viejos de staging

## Detalle

Los logs del servidor staging se están acumulando y ocupando espacio. Hacer limpieza de los archivos más viejos que 30 días.

## Contexto para la IA

Los logs viven en `/var/log/enterbase-staging/`. Hay un script `clean-old-logs.sh` que ya hicimos hace meses pero no está automatizado en cron. Se puede correr manualmente: `bash /opt/scripts/clean-old-logs.sh --older-than 30d`.

**Por qué peso 1:** una sola acción, aislada, se resuelve en minutos. No requiere pensar.

**Por qué ⏳:** está en espera porque quiero coordinar con el equipo si algún log reciente les hace falta para debugging antes de borrarlos.

## Notas

## Tarea (CardBoard)

- [x] 🟡 Limpiar logs viejos del servidor staging ⏳ ✅ 2026-04-19
