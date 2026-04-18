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

# 📄 Marcar asistencia múltiple desde calendario

## Detalle

Nueva vista de acción múltiple desde el calendario/clase para marcar asistencia de varios alumnos a la vez. Hoy Gaby entra alumno por alumno, módulo por módulo — flujo tedioso y propenso a errores.

## Contexto para la IA

Esta es una de las tres prioridades post-descargables acordadas con Mhitzy (ver misión `app-enterbase/_aclarador.md`):
1. Registro de asistencias/entregables múltiple (ESTA tarea)
2. Integración con Kommo
3. Integración con Blackboard vía API

**Nota importante:** Esta tarea aplica solo para cursos que SIGAN en Enterbase/Canvas. Para los cursos migrados a Blackboard, la asistencia se maneja vía la API de Blackboard (ver misión `migracion-blackboard`).

**Stack:** Next.js + Prisma + PostgreSQL. Requiere UI nueva (selección múltiple en calendario) y endpoint batch para guardar asistencias.

**Por qué peso 3:** feature con UI compleja (multi-selección en calendario), endpoint batch que debe ser eficiente, y validaciones múltiples (no marcar asistencia en clases futuras, respetar horarios).

## Notas

- Hablar con Gaby sobre casos de borde: ¿qué pasa si se marca mal y hay que deshacer? ¿Se puede marcar inasistencia en bloque?

## Tarea (CardBoard)

- [ ] 🟠 Marcar asistencia múltiple desde calendario/clase (acción múltiple) ⏳
