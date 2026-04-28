---
tags:
  - enter-tech-school
  - migracion-blackboard
  - bloqueada
tipo: tarea
peso: 2
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden:
bloqueada_por:
  - esperar-cursos-gabriela
desbloquea:
---

# 📄 Probar integración API con data real

## Detalle

Una vez Gabriela haya creado los cursos en `cetemin.blackboard.com`, probar los flujos reales de la integración API REST entre Blackboard y Enterbase. Validar que las llamadas que funcionaron por Postman con payloads de prueba también funcionen contra data real de Enter Tech School.

## Contexto para la IA

Esta tarea es el cierre técnico de la etapa actual de integración. Al 19-abr la integración ya funciona a nivel API (cuenta dev, credenciales, pruebas Postman exitosas). Falta la validación contra data real, que depende de Gabriela.

**Por qué peso 2:** requiere tiempo y criterio para probar los flujos completos, detectar fallas reales, y decidir qué ajustar. Aislada pero con profundidad técnica.

## Notas

- Bloqueada por `esperar-cursos-gabriela`. Cuando esa se complete, pasar esta a `#pendiente` y quitar el 🔒.

## Tarea (CardBoard)

- [ ] 🟣 Probar integración API con data real 🔒
