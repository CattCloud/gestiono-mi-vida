---
tags:
  - enter-tech-school
  - app-enterbase
  - formulario-matriculados
  - en-espera
tipo: tarea
peso: 2
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden: 4
bloqueada_por:
  - 03-generar-y-enviar-doc-bd
desbloquea:
  - 05-hacer-pr-y-merge
---

# 📄 04 — Esperar aprobación de Bruno

## Detalle

Esperar que Bruno apruebe el deploy a producción del formulario de matriculados V2, tras haber recibido el documento de cambios de BD enviado el 17-abr.

**Nota sobre fecha:** No tiene fecha exacta porque depende de cuándo responda Bruno. Si pasa demasiado tiempo sin respuesta, se podría convertir en deadline (ej. "antes del 25-abr sí o sí").

## Contexto para la IA

Continuación directa de la tarea 03. El documento ya fue enviado por Slack el 17-abr. Bruno suele responder en 1-2 días hábiles pero esta vez viene saliendo de vacaciones, entonces puede demorar.

**Importante sobre el rol de Bruno:** Bruno NO da acceso al servidor de producción. Su aprobación es de negocio/infra — es él quien decide cuándo el feature puede ir a producción. El PR y su merge los hace y aprueba el propio usuario; el deploy es automático al mergear a main.

Si Bruno dice que no basta el doc y pide más info, esta tarea se queda pendiente y se podría crear una tarea 04.5 de "preparar info adicional".

**Por qué peso 2:** no es aislada-rápida (peso 1) porque la IA puede ayudar a anticipar posibles preguntas/objeciones de Bruno, preparar respuestas, o redactar seguimientos. Tiene contexto que vale la pena preservar.

## Notas

- Canal de comunicación con Bruno: Slack directo.
- Si no responde en 3 días, escalar con Mhitzy.

## Tarea (CardBoard)

- [ ] 🟣 Esperar aprobación de Bruno para deploy a producción ⏳
