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
  - 05c-testear-personas-y-secciones
desbloquea:
  - 06-probar-con-gaby
---

# 📄 05d — Hacer PR y merge a main — exportaciones Personas y Sección > Alumnos

## Detalle

Una vez pasado el testing técnico (05c), llevar a producción ambas exportaciones en un único PR.

**Pasos:**
1. Crear PR desde la rama de exportaciones hacia `main`.
2. Auto-aprobar el PR.
3. **Antes del merge**, verificar si hay migraciones de Prisma pendientes. Si las hay, correr `npx prisma migrate deploy` en producción ANTES de mergear (ver lección del 15-abr).
4. Merge del PR → deploy automático.
5. Validar que la app sigue corriendo en producción sin errores.
6. Verificar que las exportaciones están accesibles en el entorno de producción.
7. Avisar a Gaby que está listo para que pruebe (esto arranca la tarea 06).

## Contexto para la IA

**Lección del 15-abr:** el deploy anterior (formulario de matriculados) tumbó la app porque se mergeó sin correr la migración de Prisma primero. Aunque estas exportaciones probablemente no toquen schema, la verificación es obligatoria.

**Por qué peso 2:** no es un PR mecánico. Tiene un punto crítico (verificación de migraciones) y requiere validar post-deploy que todo sigue operativo. No es peso 3 porque el trabajo pesado (desarrollo + testing) ya se hizo antes.

## Notas

- Tener el rollback listo por si algo falla.
- Idealmente hacer el merge en horario donde estés disponible para revertir si es necesario.
- Al completarse, la tarea 06 (`probar-con-gaby`) pasa de `#en-espera` a `#pendiente` para coordinar con ella.

## Tarea (CardBoard)

- [x] 🟣 Hacer PR y merge a main — exportaciones Personas y Sección > Alumnos 📅 2026-04-23 ✅ 2026-04-23
