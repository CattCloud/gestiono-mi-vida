---
tags:
  - enter-tech-school
  - app-enterbase
  - formulario-matriculados
tipo: tarea
peso: 3
estado: bloqueada
fecha_tipo: rango
fecha_inicio: 2026-04-22
fecha_fin: 2026-04-25
fecha_completado:
orden: 3
bloqueada_por:
  - 02-esperar-aprobacion-bruno
desbloquea:
---

# 📄 03 — Deploy a producción

## Detalle

Una vez aprobado el acceso por Bruno, hacer el deploy del formulario de matriculados V2 a producción. Pasos:

1. Hacer PR con request hacia el usuario de Bruno
2. Esperar aprobación del PR
3. **Antes del merge**, correr `npx prisma migrate deploy` en producción
4. Merge del PR
5. Validar que la app no cayó (esta vez sí, no como el 15-abr)
6. Avisar a Gaby para que pruebe el formulario en producción

## Contexto para la IA

El deploy anterior (15-abr-2026) falló porque se hizo el merge sin correr la migración de Prisma primero. Resultado: la app cayó porque el schema nuevo necesitaba tabla nueva + campos adicionales que no existían en BD. Se revirtió.

**La lección clave es el orden:** la migración va ANTES del merge, no después.

**Ventana de deploy:** entre el 22 y 25 de abril. Se puede hacer cualquier día en ese rango, pero idealmente en la mañana por si hay que revertir.

**Por qué peso 3:** tiene subtareas secuenciales, dependencia de Bruno, y es del tipo "cosas que suelen complicarse" (ya pasó una vez). Naturaleza impredecible.

## Notas

- Tener a mano el rollback listo por si acaso.
- Coordinar con Gaby el día exacto para que ella esté disponible para probar.

## Tarea (CardBoard)

- [ ] 🟠 Deploy de formulario de matriculados a producción (correr `npx prisma migrate deploy` antes del merge) 📅 2026-04-22
