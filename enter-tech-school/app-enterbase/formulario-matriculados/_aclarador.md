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

**Estado actual (22-abr-2026):** ✅ Sub-misión completada. Bruno aprobó el deploy y el PR se mergeó exitosamente el 21-abr. El formulario de matriculados V2 está en producción.

Esta sub-misión incluye 5 tareas secuenciales (ver orden en los archivos 01, 02, 03, 04, 05).

## Tareas

- [[01-cambiar-orden-secciones|📄 01 — Cambiar orden de secciones]] — peso 1 🟡 ✅ completada
- [[02-testear-formulario|📄 02 — Testear formulario con cambios BD]] — peso 2 🟣 ✅ completada
- [[03-generar-y-enviar-doc-bd|📄 03 — Generar doc de cambios BD y enviar a Bruno]] — peso 3 🟠 ✅ completada
- [[04-esperar-aprobacion-bruno|📄 04 — Esperar aprobación de Bruno]] — peso 2 🟣 ✅ completada
- [[05-hacer-pr-y-merge|📄 05 — Hacer PR, auto-aprobar y merge a main]] — peso 2 🟣 ✅ completada

## Notas

- Incidente del 15-abr-2026: El PR se mergeó sin correr `npx prisma migrate deploy` en producción. La app cayó y se revirtió.
- **Lección clave:** la migración de Prisma va ANTES del merge, no después.
- Bruno NO da acceso al servidor — su aprobación es de negocio/infra. El PR lo hace y aprueba el propio usuario.
- Deploy es automático al mergear a `main`.
