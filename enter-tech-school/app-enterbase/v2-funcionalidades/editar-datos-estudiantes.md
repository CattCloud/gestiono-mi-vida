---
tags:
  - enter-tech-school
  - app-enterbase
  - v2-funcionalidades
  - en-espera
tipo: tarea
peso: 3
fecha_tipo: sin-fecha
fecha_inicio:
fecha_fin:
fecha_completado:
orden:
bloqueada_por:
desbloquea:
---

# 📄 Editar datos de estudiantes existentes

## Detalle

Permitir editar la información personal de un estudiante ya registrado. Abrir el formulario completo del estudiante en una nueva página (no en modal lateral) con opción de editar los campos.

## Contexto para la IA

**Stack:** Next.js + Prisma + PostgreSQL. Reutiliza el formulario V2 pero en modo edición.

Se diferencia de "matricular estudiantes antiguos" (otra tarea de V2) en que esta es solo para editar datos personales, no para agregar matrículas nuevas.

**Por qué peso 3:** feature completa, nueva página, validación de cambios, posibles efectos en datos históricos (ej. si se cambia el nombre después de facturar).

## Notas

- Ver también `ver-detalle-completo-estudiante` — hermanas.

## Tarea (CardBoard)

- [ ] 🟠 Editar datos de estudiantes existentes: formulario completo con opción de editar en nueva página ⏳
