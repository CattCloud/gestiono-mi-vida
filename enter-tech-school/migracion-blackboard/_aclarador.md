---
tags:
  - enter-tech-school
  - mision
  - migracion-blackboard
tipo: mision
---

# 🎯 Migración a Blackboard

## Aclarador

Enter Tech School está migrando de Canvas a Blackboard como plataforma para alumnos. Mi rol es cubrir los detalles técnicos de desarrollo.

El 14-abr-2026 se realizó una reunión con un técnico de Blackboard donde se identificó que Blackboard cuenta con una API (https://developer.blackboard.com/portal/displayApi/Learn) que puede servir para la interacción entre Blackboard y el sistema de Enter Tech School.

**Reuniones clave:**
- Jueves 17-abr-2026 a las 12 PM: reunión con Luigi para aprender a crear un curso en Blackboard, brandearlo y subir info necesaria.
- Viernes 18-abr (aprox): reunión breve con Nicolás (técnico de Blackboard) para cerrar los detalles técnicos de la integración.

**Primer curso a migrar:** "IA Estratégica para Profesionales" (inicio 28-abr-2026). Según cómo resulte, se migran los demás.

**Integraciones identificadas con la API:**
- **Asistencia:** Marcar asistencia en Blackboard y que Enterbase la jale automáticamente vía API (elimina la doble carga actual).
- **Matriculados:** Al registrar un estudiante en Enterbase, crear automáticamente su cuenta en Blackboard vía API.
- Blackboard expone operaciones completas (crear, editar, eliminar, actualizar) sobre cuentas, tareas, asistencia, calendarios y matriculados.

## Sub-misiones activas

(Ninguna — el flujo actual es lineal. Cuando arranque la integración técnica, puede crearse una sub-misión `integracion-api/`.)

## Tareas sueltas

- [[tareas-sueltas/revisar-api-blackboard|📄 Revisar y entender la API de Blackboard]] — peso 3 🟠 ✅
- [[tareas-sueltas/generar-doc-api-lenguaje-sencillo|📄 Generar documentación de la API en lenguaje sencillo]] — peso 3 🟠 ✅
- [[tareas-sueltas/reunion-luigi|📄 Reunión con Luigi — crear curso + API]] — peso 2 🟣 ✅
- [[tareas-sueltas/preparar-reunion-lunes|📄 Preparar lo necesario para reunión del lunes]] — peso 2 🟣 📅 18-abr
- [[tareas-sueltas/reunion-nicolas|📄 Reunión de coordinación con Nicolás]] — peso 2 🟣 📅 20-abr
- [[tareas-sueltas/leer-manual-api|📄 Leer manual oficial de la API cuando Nicolás lo comparta]] — peso 2 🟣 ✅

## Notas

- Blackboard usuario ya compartido por Mhitzy vía WhatsApp.
- Autorización/claves se piden en la reunión con Luigi (y se cierran con Nicolás).
