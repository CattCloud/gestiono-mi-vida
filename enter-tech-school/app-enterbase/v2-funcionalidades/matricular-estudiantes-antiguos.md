---
tags:
  - enter-tech-school
  - app-enterbase
  - v2-funcionalidades
tipo: tarea
peso: 3
estado: en-espera
fecha_tipo: deadline
fecha_inicio:
fecha_fin: 2026-05-31
fecha_completado:
orden:
bloqueada_por:
desbloquea:
---

# 📄 Matricular estudiantes antiguos

## Detalle

Nuevo flujo de matrícula para estudiantes que ya están en el sistema. En lugar de pedir todos los datos personales otra vez, solo pedir:
1. Curso
2. Tipo de inscripción
3. Pago

Reutilizando la información personal que ya existe del estudiante.

## Contexto para la IA

Esta funcionalidad es **necesaria para mayo 2026** porque empezarán a llegar estudiantes recurrentes (alumnos que ya matricularon un curso anterior y se vuelven a matricular en uno nuevo).

Es uno de los pilares de la decisión "los datos personales se registran UNA vez" acordada en equipo. Lo que cambia entre inscripciones es: curso, tipo de matrícula y pago.

**Stack:** Next.js + Prisma + PostgreSQL. El formulario nuevo es una variante más corta del formulario V2 ya existente.

**Por qué peso 3:** es una feature completa con UX propia (flujo distinto al de matrícula nueva), toca BD, requiere identificar al alumno (búsqueda por DNI/nombre), y tiene deadline de negocio.

## Notas

- Coordinar con Gaby para entender el flujo operativo actual de re-matrículas.
- Se puede arrancar en cuanto el formulario V2 esté en producción y estable.

## Tarea (CardBoard)

- [ ] 🟠 Matricular estudiantes antiguos: formulario corto (curso + inscripción + pago) 📅 2026-05-31
