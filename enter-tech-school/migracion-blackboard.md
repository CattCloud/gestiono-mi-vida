---
tags: [enter-tech-school, migracion-blackboard]
---

# Migración a Blackboard

## Aclarador
Enter Tech School está migrando de Canvas a Blackboard como plataforma para alumnos. Mi rol es cubrir los detalles técnicos de desarrollo. El 14-abr-2026 se realizó una reunión con un técnico de Blackboard donde se identificó que Blackboard cuenta con una API (https://developer.blackboard.com/portal/displayApi/Learn) que puede servir para la interacción entre Blackboard y el sistema de Enter Tech School.

Mhitzy confirmó que el jueves 17-abr-2026 a las 12 PM habrá reunión con Luigi para aprender a crear un curso en Blackboard, brandearlo y subir la info necesaria. El primer curso que se lanzará será "IA Estratégica para Profesionales" (inicio 28-abr-2026). Según cómo resulte, se migrarán los demás cursos.

Mhitzy compartió por WhatsApp mi usuario oficial para entrar a Blackboard y explorarlo antes de la reunión. En la reunión del jueves con Luigi se le comentará la intención de integrar la API, se pedirá el manual oficial y se preguntará por la autorización/claves necesarias (es una API privada). Luego se plantea una reunión breve el viernes 18-abr con Nicolás (técnico de Blackboard) para cerrar los detalles técnicos de la integración.

**Integraciones identificadas con la API:**
- **Asistencia:** Marcar asistencia en Blackboard y que Enterbase la jale automáticamente vía API (elimina la doble carga actual).
- **Matriculados:** Al registrar un estudiante en Enterbase, crear automáticamente su cuenta en Blackboard vía API.
- Blackboard expone operaciones completas (crear, editar, eliminar, actualizar) sobre cuentas, tareas, asistencia, calendarios y matriculados.

## Tareas

- [x] Revisar y entender la API de Blackboard 📅 2026-04-15 ✅ 2026-04-15
- [x] Generar documentación de la API en lenguaje sencillo para las demás áreas (no técnicas) — qué datos se pueden jalar, subir, etc.
- [x] Reunión con Luigi — crear curso en Blackboard, branding y subir info + comentar integración API, pedir manual y preguntar por autorización/claves 📅 2026-04-17
- [ ] Preparar lo necesario para la reunion del lunes con  📅 2026-04-18
- [ ] Reunión de coordinación con Nicolás (técnico Blackboard)  — revisar manual, autorización y claves de conexión. 📅 2026-04-20
- [x] Leer manual oficial de la API de Blackboard cuando Nicolás lo comparta

## Notas

