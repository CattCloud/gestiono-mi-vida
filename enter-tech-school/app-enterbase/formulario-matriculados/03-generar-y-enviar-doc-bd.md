---
tags:
  - enter-tech-school
  - app-enterbase
  - formulario-matriculados
  - completada
tipo: tarea
peso: 3
fecha_tipo: exacta
fecha_inicio: 2026-04-16
fecha_fin:
fecha_completado: 2026-04-17
orden: 3
bloqueada_por:
desbloquea:
  - 04-esperar-aprobacion-bruno
---

# 📄 03 — Generar doc de cambios de BD y enviar a Bruno

## Detalle

Preparar un documento breve que explique los cambios de base de datos que trae el PR del formulario de matriculados V2 (qué tabla nueva se crea, qué campos adicionales se agregan, por qué son necesarios) y enviárselo a Bruno por Slack.

El documento debe ser entendible sin contexto técnico profundo — Bruno lo va a leer para decidir si aprueba el deploy a producción.

## Contexto para la IA

Esto surge del incidente del 15-abr-2026, cuando el deploy falló porque no se corrió `npx prisma migrate deploy`. Bruno (responsable de infraestructura) preguntó si era una tabla nueva — se le confirmó que sí (tabla nueva + campos adicionales). Para facilitarle la decisión, se acordó generar este documento antes del PR.

**Stack relevante:** Next.js + Prisma + PostgreSQL. Las migraciones viven en `prisma/migrations/`.

**Sobre Bruno:** NO da acceso al servidor de producción. Su aprobación es de negocio/infra. El PR lo hace y aprueba el propio usuario; el deploy es automático al mergear a main.

**Por qué peso 3:** aunque parece "solo redactar un doc", implica repasar las migraciones, identificar cada cambio, explicarlo de forma no-técnica, preparar ejemplos y coordinar el envío. Tiene complejidad oculta y dependencias.

**Por qué se fusionó generar + enviar:** originalmente eran dos tareas, pero el envío es inmediato después de generar el doc y no aporta granularidad práctica separarlos.

## Notas

- Documento generado el 16-abr a las 9:34 AM.
- Enviado a Bruno por Slack el 17-abr-2026.
- Guardado en Drive.

## Tarea (CardBoard)

- [x] 🟠 Generar doc con los cambios de BD y enviarlo a Bruno 📅 2026-04-16 ✅ 2026-04-17
