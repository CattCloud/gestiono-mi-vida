---
tags:
  - enter-tech-school
  - app-enterbase
  - formulario-matriculados
  - tarea-pesada
tipo: tarea
estado: completada
fecha_tipo: exacta
fecha_inicio: 2026-04-16
fecha_fin:
fecha_completado: 2026-04-16
orden: 1
bloqueada_por:
desbloquea:
  - 02-esperar-aprobacion-bruno
---

# 📄 01 — Generar documento de cambios de BD

## Detalle

Preparar un documento breve que explique los cambios de base de datos que trae el PR del formulario de matriculados V2: qué tabla nueva se crea, qué campos adicionales se agregan a qué tablas, y por qué son necesarios.

El documento debe ser entendible sin tener contexto técnico profundo — Bruno lo va a leer para decidir si aprueba el acceso al servidor de producción.

## Contexto para la IA

Esto surge del incidente del 15-abr-2026, cuando el deploy falló porque no se corrió `npx prisma migrate deploy`. Bruno (responsable de infraestructura) preguntó si era una tabla nueva — se le confirmó que sí (tabla nueva + campos adicionales). Para facilitarle la decisión, acordamos generar este documento antes de hacer el PR con request a su usuario.

**Stack relevante:** Next.js + Prisma + PostgreSQL. Las migraciones viven en `prisma/migrations/`. El PR que se revirtió estaba en la rama `feature/formulario-matriculados-v2`.

## Notas

- El documento lo terminé el 16-abr a las 9:34 AM.
- Quedó guardado en Drive, pendiente solo enviárselo a Bruno (eso pasa a la tarea 02).

## Tarea (CardBoard)

- [x] Generar documento breve con los cambios de BD para facilitar la decisión de Bruno 📅 2026-04-16 ✅ 2026-04-16
