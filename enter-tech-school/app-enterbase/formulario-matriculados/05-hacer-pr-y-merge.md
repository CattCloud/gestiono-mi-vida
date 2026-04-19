---
tags:
  - enter-tech-school
  - app-enterbase
  - formulario-matriculados
  - bloqueada
tipo: tarea
peso: 2
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden: 5
bloqueada_por:
  - 04-esperar-aprobacion-bruno
desbloquea:
---

# 📄 05 — Hacer PR, auto-aprobar y merge a main

## Detalle

Una vez Bruno apruebe el deploy, hacer el PR del formulario de matriculados V2, auto-aprobarlo y mergear a main. El deploy a producción es automático al mergear.

**Pasos:**
1. Crear PR desde `feature/formulario-matriculados-v2` hacia `main`.
2. Auto-aprobar el PR.
3. **Antes del merge**, correr `npx prisma migrate deploy` en producción.
4. Merge del PR → deploy automático.
5. Validar que la app no cayó (esta vez sí, no como el 15-abr).
6. Avisar a Gaby para que pruebe el formulario en producción.

## Contexto para la IA

El deploy anterior (15-abr-2026) falló porque se hizo el merge sin correr la migración de Prisma primero. Resultado: la app cayó porque el schema nuevo necesitaba tabla nueva + campos adicionales que no existían en BD. Se revirtió.

**La lección clave es el orden:** la migración va ANTES del merge, no después.

**Por qué peso 2:** aunque tiene varios sub-pasos, el trabajo pesado (desarrollo + test + doc) ya está hecho. Lo que queda es ejecución con un punto crítico (el orden migración→merge). No es peso 3 porque ya no hay investigación ni desarrollo, solo aplicar el plan.

## Notas

- Tener listo el rollback por si acaso.
- Coordinar con Gaby el día exacto para que ella esté disponible para probar.
- Idealmente hacer el deploy en la mañana por si hay que revertir.

## Tarea (CardBoard)

- [ ] 🟣 Hacer PR, correr `npx prisma migrate deploy` y mergear a main (deploy automático) 🔒
