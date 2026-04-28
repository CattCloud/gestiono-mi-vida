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

**Estado actual (19-abr-2026) — integración API funcionando:**

Hoy se realizó la reunión con Nicolás (se adelantó del 20-abr al 19-abr) y se avanzó hasta dejar la integración técnica operativa:

1. Se creó cuenta en https://developer.blackboard.com/.
2. Se obtuvieron las credenciales necesarias (ID de aplicación, secreto, etc.).
3. Con esas credenciales se conectó la API REST contra https://cetemin.blackboard.com/ (cuenta de administrador que Mhitzy ya había compartido por WhatsApp).
4. Se probaron las llamadas vía Postman y funcionaron con éxito.

**Bloqueo actual:** no hay data de Enter Tech School cargada en Blackboard para probar contra data real. Gabriela debe crear los cursos en `cetemin.blackboard.com` antes de que se pueda seguir validando los flujos.

**Integraciones identificadas con la API (post-validación):**
- **Asistencia:** Marcar asistencia en Blackboard y que Enterbase la jale automáticamente vía API (elimina la doble carga actual).
- **Matriculados:** Al registrar un estudiante en Enterbase, crear automáticamente su cuenta en Blackboard vía API.
- Blackboard expone operaciones completas (crear, editar, eliminar, actualizar) sobre cuentas, tareas, asistencia, calendarios y matriculados.

Estas integraciones no se han convertido en tareas todavía — se definirán cuando avance la validación con data real.

## Sub-misiones activas

(Ninguna — el flujo actual es lineal. Cuando arranque la integración técnica, puede crearse una sub-misión `integracion-api/`.)

## Tareas sueltas

- [[tareas-sueltas/revisar-api-blackboard|📄 Revisar y entender la API de Blackboard]] — peso 3 🟠 ✅
- [[tareas-sueltas/generar-doc-api-lenguaje-sencillo|📄 Generar documentación de la API en lenguaje sencillo]] — peso 3 🟠 ✅
- [[tareas-sueltas/reunion-luigi|📄 Reunión con Luigi — crear curso + API]] — peso 2 🟣 ✅
- [[tareas-sueltas/leer-manual-api|📄 Leer manual oficial de la API cuando Nicolás lo comparta]] — peso 2 🟣 ✅
- [[tareas-sueltas/preparar-reunion-lunes|📄 Preparar lo necesario para reunión del lunes]] — peso 2 🟣 ✅ descartada
- [[tareas-sueltas/reunion-nicolas|📄 Reunión de coordinación con Nicolás]] — peso 2 🟣 ✅ completada
- [[tareas-sueltas/esperar-cursos-gabriela|📄 Esperar que Gabriela cree los cursos en Blackboard]] — peso 1 🟡 ⏳ en espera
- [[tareas-sueltas/probar-integracion-api-con-data-real|📄 Probar integración API con data real]] — peso 2 🟣 🔒 bloqueada

## Notas

- Blackboard usuario ya compartido por Mhitzy vía WhatsApp.
- Autorización/claves se piden en la reunión con Luigi (y se cierran con Nicolás).
