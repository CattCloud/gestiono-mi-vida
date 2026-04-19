---
tags:
  - enter-tech-school
  - app-enterbase
  - pendiente
tipo: tarea
peso: 1
fecha_tipo: exacta
fecha_inicio: 2026-04-20
fecha_fin:
fecha_completado:
orden:
bloqueada_por:
desbloquea:
---

# Revisar backup semanal

## Detalle

Verificar que el script de backup semanal de la base de datos de Enterbase haya corrido correctamente y que el archivo resultante esté en su lugar.

## Contexto para la IA

El backup corre todos los lunes a las 2 AM vía cron. Los archivos quedan en `/backups/enterbase/` con formato `backup-YYYY-MM-DD.sql.gz`. Si falta el archivo del lunes, revisar logs en `/var/log/cron.log`.

**Por qué peso 1:** acción aislada, sin dependencias, rápida (5 minutos máximo).

## Notas

## Tarea (CardBoard)

- [ ] 🟡 Revisar que el script de backup semanal siga corriendo 📅 2026-04-20
