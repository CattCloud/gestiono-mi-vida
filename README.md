# Mi Universo — Sistema de Gestión Personal

Sistema de gestión de tareas y vida personal construido en Obsidian, sincronizado con Git. Diseñado para interactuar con un agente IA (Cowork, Claude Code u otro) que lee y edita los archivos directamente.

---

## Glosario astronómico

| Término | Significado |
|---|---|
| **Universo** | Vista global de todo: todas las áreas, todas las tareas |
| **Planeta** | Un área de vida (trabajo, proyectos personales, hábitos, etc.) |
| **Mapa estelar** | Dashboard de un planeta: qué misiones hay, qué está pendiente |
| **Misión** | Un proyecto concreto dentro de un planeta |
| **Aclarador** | Texto en lenguaje natural que describe la situación de una misión |
| **Aclarador diario** | Reflexión del día: qué hiciste, qué falta, cómo estás |
| **Nebulosa mental** | Tareas sueltas que aún no tienen planeta definido |
| **Destellos** | Ideas o tareas que aparecen de repente y hay que capturar |
| **Control de Misión** | Skill/instrucciones para que un agente IA opere este sistema |
| **Notas** | Cuaderno de captura rápida: modificaciones a tareas, ideas de mejora y nebulosa sin categoría. Se procesa por lotes. |

---

## Estructura

Jerarquía de 4 niveles: **Planeta → Misión → Sub-misión (opcional) → Tarea**. Cada misión y cada sub-misión es una carpeta con un `_aclarador.md` adentro. Cada tarea es un `.md` propio con frontmatter rico.

```
gestiono-mi-vida/
├── README.md                    ← Este archivo
├── universo.md                  ← Dashboard global
├── notas.md                     ← Captura rápida (modificaciones, ideas, nebulosa)
│
├── skill/                       ← 🎯 Instrucciones para el agente IA
│   └── control-de-mision.md
│
├── enter-tech-school/           ← 🪐 Planeta (trabajo)
│   ├── README.md
│   ├── _mapa-estelar.md
│   ├── app-enterbase/           ← 🎯 Misión (carpeta)
│   │   ├── _aclarador.md        ← Aclarador de la misión
│   │   ├── formulario-matriculados/   ← 📂 Sub-misión
│   │   │   ├── _aclarador.md
│   │   │   └── NN-tarea.md      ← 📄 Tarea secuencial
│   │   └── tareas-sueltas/      ← Tareas de la misión sin sub-misión
│   │       └── tarea.md
│   └── [otras-misiones]/
│
├── mis-proyectos-dev/           ← 🪐 Planeta (proyectos personales)
├── mis-sistemas-identidad/      ← 🪐 Planeta (hábitos e identidad)
│
├── nebulosa-mental/             ← 🌫️ Tareas dispersas sin área definida
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── destellos.md
│
├── aclarador-diario/            ← 📓 Reflexiones diarias
│   ├── README.md
│   └── [YYYY-MM-DD].md
│
├── context/                     ← 📜 Documentos fundacionales
│   ├── yo.md
│   └── contexto-inicial-gestion.md
│
└── _plantillas/                 ← Plantillas reutilizables
    ├── plantilla-mision.md
    ├── plantilla-sub-mision.md
    ├── plantilla-tarea.md
    └── plantilla-aclarador.md
```

---

## Planetas actuales

- **enter-tech-school/** — Todo lo relacionado con mi trabajo en Enter Tech School. Cada proyecto es una misión (un archivo).
- **mis-proyectos-dev/** — Proyectos de software que desarrollo por cuenta propia.
- **mis-sistemas-identidad/** — Los hábitos y sistemas que estoy construyendo para mi crecimiento personal.
- **nebulosa-mental/** — El cajón para lo que surge de repente: compras, ideas, tareas sueltas que aún no tienen planeta.

---

## Cómo funciona

1. Cada proyecto vive en una **carpeta** (misión) dentro de su planeta, con un `_aclarador.md` que contiene su contexto.
2. Dentro de una misión pueden existir **sub-misiones** (carpetas con su propio `_aclarador.md`) que agrupan tareas relacionadas.
3. Cada **tarea** es un `.md` propio con frontmatter (peso, estado, fechas, dependencias) + 4 secciones: Detalle, Contexto para la IA, Notas, Tarea (CardBoard).
4. Las tareas que no caen en una sub-misión viven en `[mision]/tareas-sueltas/`.
5. El **universo.md** muestra todas las tareas pendientes de todos los planetas.
6. Cada planeta tiene un **_mapa-estelar.md** que lista sus misiones activas.
7. Las tareas que surgen sin contexto van a **nebulosa-mental/destellos.md**.
8. Un agente IA lee **skill/control-de-mision.md** al inicio de cada chat para entender el sistema y operar sobre los archivos.

## Flujo de interacción

- **Obsidian** es la interfaz de lectura: dashboards, filtros, navegación visual.
- **Cowork / agente IA** es la interfaz de escritura: le hablas en lenguaje natural y el agente crea, edita, completa y mueve tareas en los archivos.
- El agente siempre confirma ante