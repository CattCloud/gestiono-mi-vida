---
tags:
  - enter-tech-school
  - app-enterbase
  - exportaciones
  - completada
tipo: tarea
peso: 2
fecha_tipo: exacta
fecha_inicio: 2026-04-23
fecha_fin:
fecha_completado: 2026-04-23
orden: 5
bloqueada_por:
  - 05b-implementar-seccion-alumnos
desbloquea:
  - 05d-pr-merge-exportaciones
---

# 📄 05c — Testing técnico de exportaciones: Personas y Sección > Alumnos

## Detalle

Testing técnico previo al PR. Verificar que las dos exportaciones (Personas + Sección > Alumnos) funcionan correctamente de punta a punta, antes de llevar el código a producción.

**Checklist sugerido:**
- Descargar el Excel de Personas → verificar columnas, formato, datos.
- Descargar el Excel de Sección > Alumnos → verificar columnas, formato, datos.
- **Casos de borde:**
  - Sección vacía (sin alumnos).
  - Alumnos sin pagos registrados.
  - Alumnos con múltiples pagos (validar que solo se muestra el primer pago + URL voucher).
  - Caracteres especiales en nombres (tildes, ñ).
  - Exportación con muchos registros (sin timeouts).
- Verificar que no hay errores en consola ni en logs del servidor.
- Validar que el nombre del archivo descargado sea legible y consistente.

## Contexto para la IA

**Diferencia con la tarea 06 (`06-probar-con-gaby`):** esta tarea es testing *técnico* propio (bugs, errores, casos de borde). La 06 es validación *de usuaria final* con Gaby, tras el deploy a producción.

**Por qué se incluye Personas:** aunque la tarea `04-implementar-personas` ya está completada, no se hizo un testing explícito de punta a punta. Como ambas exportaciones van en el mismo PR, tiene sentido consolidar los tests acá.

**Stack:** Next.js + Prisma + PostgreSQL. Testing se puede hacer en local o en staging.

**Lección del 15-abr:** el deploy anterior (formulario de matriculados) cayó porque no se corrió `npx prisma migrate deploy`. Aunque estas exportaciones no tocan schema, vale verificar que no hay migraciones pendientes que afecten al PR.

**Por qué peso 2:** no es solo abrir el Excel y ver que se ve bien — requiere cubrir casos de borde, pensar qué puede romperse, y documentar hallazgos. Tarea aislada pero con profundidad.

## Notas

- Si durante el testing surge un bug que requiere arreglo, crear sub-tarea o resolver y re-testear.
- Al completarse, se desbloquea `05d-pr-merge-exportaciones`.

## Tarea (CardBoard)

- [x] 🟣 Testear exportaciones: Personas y Sección > Alumnos 📅 2026-04-23 ✅ 2026-04-23
