---
tags:
  - enter-tech-school
  - app-enterbase
  - formulario-matriculados
tipo: tarea
peso: 2
estado: en-espera
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden: 2
bloqueada_por:
  - 01-generar-doc-bd
desbloquea:
  - 03-deploy-produccion
---

# 📄 02 — Esperar aprobación de Bruno

## Detalle

Enviar a Bruno el documento generado en la tarea 01 (cambios de BD) y esperar que apruebe el acceso al servidor de producción. Cuando apruebe, hacer PR con request hacia su usuario.

**Nota sobre fecha:** Esta tarea no tiene fecha exacta porque depende de cuándo responda Bruno. Si pasa demasiado tiempo sin respuesta, se podría convertir en deadline (ejemplo: "antes del 25-abr necesitamos esto sí o sí").

## Contexto para la IA

Continuación directa de la tarea 01. El documento ya está listo en Drive. Solo falta enviárselo y esperar. Bruno suele responder en 1-2 días hábiles pero esta vez viene saliendo de vacaciones, entonces puede demorar.

Si Bruno dice que no basta el doc y pide más info, esta tarea se queda pendiente y se podría crear una tarea 2.5 de "preparar info adicional".

**Por qué peso 2:** no es aislada-rápida (peso 1) porque la IA puede ayudarme a redactar el mensaje, anticipar preguntas de Bruno, o preparar respuestas a posibles objeciones. Tiene contexto que vale la pena preservar aunque sea una acción relativamente simple.

## Notas

- Canal de comunicación con Bruno: Slack directo.
- Si no responde en 3 días, escalar con Mhitzy.

## Tarea (CardBoard)

- [ ] 🟣 Enviar documento a Bruno y esperar aprobación de acceso al servidor de producción ⏳
