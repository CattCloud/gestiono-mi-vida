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

Esta sub-misión incluye 3 tareas secuenciales (ver orden en los archivos 01, 02, 03).

## Tareas

- [[01-generar-doc-bd|📄 01 — Generar doc de cambios de BD]] — peso 3 🟠 ✅ completada
- [[02-esperar-aprobacion-bruno|📄 02 — Esperar aprobación de Bruno]] — peso 2 🟣 ⏳ en espera
- [[03-deploy-produccion|📄 03 — Deploy a producción]] — peso 3 🟠 🔒 bloqueada

## Notas

- Incidente del 15-abr-2026: Al integrar el PR, la app cayó porque no se corrió la migración. Se revirtió y quedó estable.
