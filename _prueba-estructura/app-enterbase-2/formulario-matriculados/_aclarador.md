---
tags:
  - enter-tech-school
  - app-enterbase
  - sub-mision
  - formulario-matriculados
tipo: sub-mision
mision_padre: app-enterbase
---

# 📂 Formulario de Matriculados

## Aclarador

Sub-misión dentro de app-enterbase. El objetivo es digitalizar el Excel que se usaba para registrar matrículas, reemplazándolo por un formulario en Enterbase.

**Estado actual (18-abr-2026):** El formulario está listo y testeado. El último intento de deploy falló porque faltó correr `npx prisma migrate deploy` en producción. Se generó un documento explicando los cambios de BD para facilitar la aprobación de acceso por parte de Bruno.

Esta sub-misión incluye 3 tareas pesadas secuenciales (ver orden en los archivos 01, 02, 03).

## Tareas pesadas (con .md propio)

Las tareas con `01-`, `02-`, `03-` en el nombre siguen orden secuencial. Una depende de la anterior.

- [[01-generar-doc-bd|📄 01 — Generar doc de cambios de BD]] ✅ completada
- [[02-esperar-aprobacion-bruno|📄 02 — Esperar aprobación de Bruno]] ⏳ en espera
- [[03-deploy-produccion|📄 03 — Deploy a producción]] 🔒 bloqueada

## Notas

- Incidente del 15-abr-2026: Al integrar el PR, la app cayó porque no se corrió la migración. Se revirtió y quedó estable.
