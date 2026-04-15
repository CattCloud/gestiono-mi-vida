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
| **Evolución** | Registro de mejoras, problemas e ideas que surgen durante el uso |

---

## Estructura

```
gestiono-mi-vida/
├── README.md                    ← Este archivo
├── universo.md                  ← Dashboard global
├── evolucion.md                 ← Registro de mejoras, problemas e ideas para el sistema
│
├── skill/                       ← 🎯 Instrucciones para el agente IA
│   └── control-de-mision.md
│
├── enter-tech-school/           ← 🪐 Trabajo en Enter Tech School
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── [misiones].md
│
├── mis-proyectos-dev/           ← 🪐 Proyectos de software personales
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── [misiones].md
│
├── mis-sistemas-identidad/      ← 🪐 Sistemas y hábitos de identidad
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── [misiones].md
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

1. Cada proyecto vive en un solo archivo (misión) dentro de su planeta.
2. Cada misión tiene un **aclarador** (contexto en prosa) + **tareas** (`- [ ]`).
3. El **universo.md** muestra todas las tareas pendientes de todos los planetas.
4. Cada planeta tiene un **_mapa-estelar.md** que muestra solo las tareas de esa área.
5. Las tareas que surgen sin contexto van a **nebulosa-mental/destellos.md**.
6. Un agente IA lee **control-de-mision.md** al inicio de cada chat para entender el sistema y operar sobre los archivos.

## Flujo de interacción

- **Obsidian** es la interfaz de lectura: dashboards, filtros, navegación visual.
- **Cowork / agente IA** es la interfaz de escritura: le hablas en lenguaje natural y el agente crea, edita, completa y mueve tareas en los archivos.
- El agente siempre confirma antes de modificar archivos.

---

## Filosofía

- Las herramientas se adaptan a cómo pienso, no al revés.
- Contexto y tareas conviven juntos, nunca separados.
- Empezar simple, escalar cuando haga falta.
- Sin categorías complejas, sin nomenclatura rígida.
- Los archivos .md son míos — funcionan con o sin Obsidian.
- El sistema existe para quitarme peso mental, no para agregarlo.

## Plugins de Obsidian

- **Dataview** (esencial) — Renderiza las queries en universo.md y los mapas estelares como vistas vivas de tareas. Reemplaza al plugin Tasks con queries más potentes.
- **CardBoard** (esencial) — Vista Kanban/Date de tareas. Lee los `- [ ]` de los archivos y los muestra como tarjetas en columnas por fecha o estado.
- **Shimmering Focus** (tema) — Tema visual limpio con enfoque en la escritura sin distracciones.
- **Templater** (opcional) — Para crear misiones desde plantilla con un click.
