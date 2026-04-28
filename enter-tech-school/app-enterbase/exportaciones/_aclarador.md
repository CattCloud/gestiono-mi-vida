---
tags:
  - enter-tech-school
  - app-enterbase
  - sub-mision
  - exportaciones
tipo: sub-mision
mision_padre: app-enterbase
---

# 📂 Exportaciones / Descargables

## Aclarador

Sub-misión dentro de app-enterbase. El objetivo es que Gaby y el equipo puedan descargar datos operativos de Enterbase en Excel, en lugar de consultar/calcular manualmente desde Cloud.

**Estado actual (19-abr-2026):** El 15-abr el equipo validó el formato de los Excel (Personas y Sección > Alumnos). Se aprobó avanzar. Hoy se ejecuta la implementación de forma **secuencial**: primero Personas, luego Sección > Alumnos. La tarea original que juntaba ambas (peso 3) se partió en dos tareas de peso 2 para tener tracking por feature. Gaby probará cuando ambas estén subidas. Mientras, sigue calculando como venía haciéndolo.

**Orden de prioridad acordado:**
1. Sección > Alumnos (ya avanzado)
2. Personas (recién arranca análisis)
3. Leads (mejora)
4. Pagos (depende de respuesta del equipo)
5. Encuestas
6. Canvas

**Futuro V2:** Al darle a exportar aparecería un desplegable con filtros previos (rango de fechas, alumnos, etc.); se aplican filtros y luego se descarga.

## Tareas

### Secuencia principal (Sección > Alumnos + Personas)

- [[01-esperar-respuestas-equipo|📄 01 — Esperar respuestas del equipo sobre consultas]] — peso 1 🟡 ✅ completada
- [[02-analisis-personas|📄 02 — Análisis exportación: Personas]] — peso 3 🟠 ✅ completada
- [[03-presentacion-avance|📄 03 — Presentación avance Sección/Personas]] — peso 2 🟣 ✅ completada
- [[04-implementar-personas|📄 04 — Implementar exportación: Personas]] — peso 2 🟣 ✅ completada
- [[05a-planear-seccion-alumnos|📄 05a — Planear exportación: Sección > Alumnos]] — peso 1 🟡 ✅ completada
- [[05b-implementar-seccion-alumnos|📄 05b — Implementar exportación: Sección > Alumnos]] — peso 2 🟣 ✅ completada (23-abr)
- [[05c-testear-personas-y-secciones|📄 05c — Testing técnico: Personas y Sección > Alumnos]] — peso 2 🟣 ✅ completada (23-abr)
- [[05d-pr-merge-exportaciones|📄 05d — PR y merge a main — exportaciones]] — peso 2 🟣 ✅ completada (23-abr) — en producción

_(La antigua tarea `06-probar-con-gaby` se eliminó el 24-abr: Gaby prueba las exportaciones por su cuenta, sin tarea espejo acá.)_

### Análisis pendientes (otras exportaciones)

- [[esperar-respuesta-pagos|📄 Esperar respuesta de Pagos]] — peso 1 🟡 ⏳ en espera
- [[analisis-leads|📄 Análisis exportación: Leads]] — peso 2 🟣 ⏳
- [[analisis-pagos|📄 Análisis exportación: Pagos]] — peso 2 🟣 🔒 bloqueada por respuesta
- [[analisis-encuestas|📄 Análisis exportación: Encuestas]] — peso 2 🟣 ⏳
- [[analisis-canvas|📄 Análisis exportación: Canvas]] — peso 2 🟣 ⏳

## Notas

- Documento con consultas por área enviado por Drive. Todo el equipo respondió excepto Pagos.
- Para Leads, Encuestas y Canvas: se avanzan cuando Sección/Personas esté en producción.
