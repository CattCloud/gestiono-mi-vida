# Mi Universo — Sistema de Gestión Personal

Sistema de gestión de tareas y vida personal construido en Obsidian, sincronizado con Git. Diseñado para que un agente IA (Cowork, Claude Code, u otro) lea y edite los archivos directamente en lenguaje natural, mientras Obsidian sirve como capa visual.

---

## Glosario astronómico

| Término | Significado |
|---|---|
| **Universo** | Vista global de todo: todas las áreas, todas las tareas (archivo `universo.md`) |
| **Planeta** | Un área de vida (trabajo, proyectos personales, hábitos, etc.) |
| **Mapa estelar** | Dashboard de un planeta: lista sus misiones activas y sus tareas |
| **Misión** | Un proyecto concreto dentro de un planeta (carpeta con `_aclarador.md`) |
| **Sub-misión** | Agrupación opcional de tareas dentro de una misión (carpeta con `_aclarador.md`) |
| **Aclarador** | Texto en lenguaje natural que describe la situación de una misión o sub-misión |
| **Aclarador diario** | Reflexión del día: qué hiciste, qué falta, cómo estás |
| **Nebulosa mental** | Tareas sueltas que aún no tienen planeta definido |
| **Destellos** | Ideas o tareas que aparecen de repente y hay que capturar |
| **Control de Misión** | Skill/instrucciones para que un agente IA opere este sistema |
| **Notas** | Cuaderno de captura rápida: modificaciones a tareas, ideas de mejora y nebulosa sin categoría. Se procesa por lotes. |

---

## Jerarquía de 4 niveles

**Planeta → Misión → Sub-misión (opcional) → Tarea**

- **Planeta** es una carpeta en la raíz (`enter-tech-school/`, `mis-proyectos-dev/`, etc.).
- **Misión** es una carpeta dentro del planeta, con un `_aclarador.md` que contiene su contexto.
- **Sub-misión** es una carpeta dentro de una misión (opcional), también con su `_aclarador.md`. Si una misión no tiene agrupaciones naturales, todas sus tareas van en `[mision]/tareas-sueltas/`.
- **Tarea** es un `.md` propio con frontmatter rico (peso, tag de estado, fechas, dependencias) + 4 secciones: Detalle, Contexto para la IA, Notas, Tarea (CardBoard).

---

## Estructura del vault

```
gestiono-mi-vida/
├── README.md                        ← Este archivo
├── universo.md                      ← Dashboard global con Dataview
├── notas.md                         ← Captura rápida (modificaciones, ideas, nebulosa)
│
├── skill/                           ← 🎯 Instrucciones para el agente IA
│   └── control-de-mision.md         ← Skill principal: léelo al iniciar cada chat
│
├── context/                         ← 📜 Documentos fundacionales
│   ├── yo.md                        ← Perfil personal (los "3 Bosses", fortalezas, debilidades)
│   ├── contexto-inicial-gestion.md
│   ├── guia-instalacion-plugins.md
│   └── [propuestas históricas y decisiones de diseño]
│
├── _plantillas/                     ← Plantillas reutilizables
│   ├── plantilla-mision.md          ← Para `_aclarador.md` de misión
│   ├── plantilla-sub-mision.md      ← Para `_aclarador.md` de sub-misión
│   ├── plantilla-tarea.md           ← Para cada tarea nueva
│   └── plantilla-aclarador.md       ← Para aclaradores diarios
│
├── enter-tech-school/               ← 🪐 Planeta (trabajo)
│   ├── README.md
│   ├── _mapa-estelar.md             ← Índice de misiones activas + dashboards Dataview
│   ├── app-enterbase/               ← 🎯 Misión (carpeta)
│   │   ├── _aclarador.md
│   │   ├── formulario-matriculados/ ← 📂 Sub-misión
│   │   │   ├── _aclarador.md
│   │   │   └── 01-cambiar-orden-secciones.md    ← 📄 Tarea (prefijo NN- si es secuencia)
│   │   ├── exportaciones/
│   │   ├── v2-funcionalidades/
│   │   └── tareas-sueltas/          ← Tareas de la misión sin sub-misión
│   ├── desarrollo-cursos/
│   ├── instructor-code101n20/
│   ├── integracion-kommo/
│   └── migracion-blackboard/
│
├── mis-proyectos-dev/               ← 🪐 Planeta (proyectos personales)
├── mis-sistemas-identidad/          ← 🪐 Planeta (hábitos e identidad)
│
├── nebulosa-mental/                 ← 🌫️ Tareas dispersas sin área definida
│   ├── _mapa-estelar.md
│   └── destellos.md
│
├── aclarador-diario/                ← 📓 Reflexiones diarias
│   └── [YYYY-MM-DD].md
│
├── _prueba-estructura/              ← 🧪 Zona de pruebas para iterar diseño del sistema
│   ├── README.md
│   └── v2-unificado/                ← Última iteración de prueba antes de integrar al vault
│
└── .obsidian/
    ├── snippets/                    ← CSS personalizado (ver README interno)
    │   ├── README.md
    │   └── cardboard-hide-tags.css
    └── [configuración de plugins, workspace, etc.]
```

---

## Planetas actuales

- **enter-tech-school/** — Todo lo relacionado con mi trabajo en Enter Tech School. Cada proyecto es una misión (carpeta).
- **mis-proyectos-dev/** — Proyectos de software que desarrollo por cuenta propia.
- **mis-sistemas-identidad/** — Hábitos y sistemas que estoy construyendo para mi crecimiento personal.
- **nebulosa-mental/** — El cajón para lo que surge de repente: compras, ideas, tareas sueltas que aún no tienen planeta.

---

## Sistema de estados (tags)

Cada tarea tiene exactamente un tag de estado en su frontmatter. Es la **única fuente de verdad**: alimenta los Tag boards de CardBoard y las queries de Dataview.

| Tag | Cuándo | Marcador en línea CardBoard |
|---|---|---|
| `#pendiente` | Lista para trabajar. Sin bloqueos ni esperas externas. | (sin emoji de estado) |
| `#en-espera` | Esperando respuesta de alguien o condición externa. | `⏳` al final del texto |
| `#bloqueada` | Esperando que se complete otra tarea (llenar `bloqueada_por`). | `🔒` al final del texto |
| `#completada` | Cerrada. Debe tener `fecha_completado`. | `- [x]` + `✅ YYYY-MM-DD` |

El tag del frontmatter y el marcador de la línea CardBoard **siempre van alineados**. El agente IA hace un barrido silencioso al inicio de cada conversación para detectar desincronizaciones.

---

## Pesos de tareas

Cada tarea tiene un peso 1/2/3 que refleja su complejidad. El emoji de peso va **al inicio** del texto CardBoard porque CardBoard trunca textos largos.

| Peso | Emoji | Naturaleza |
|---|---|---|
| **1** | 🟡 | Aislada y rápida. Una acción sin dependencias. |
| **2** | 🟣 | Aislada pero requiere tiempo o pensamiento. |
| **3** | 🟠 | Compleja. Subtareas, dependencias, o naturaleza impredecible. |

---

## Cómo funciona

1. Cada proyecto vive en una **carpeta** (misión) dentro de su planeta, con un `_aclarador.md` que contiene su contexto.
2. Dentro de una misión pueden existir **sub-misiones** (carpetas con su propio `_aclarador.md`) que agrupan tareas relacionadas.
3. Cada **tarea** es un `.md` propio con frontmatter rico y 4 secciones (Detalle, Contexto para la IA, Notas, Tarea CardBoard).
4. Las tareas que no caen en una sub-misión viven en `[mision]/tareas-sueltas/`.
5. Las tareas secuenciales dentro de una sub-misión se prefijan con `NN-` (`01-`, `02-`, `03-`) para reflejar el orden.
6. **`universo.md`** muestra todas las tareas pendientes de todos los planetas vía queries Dataview.
7. Cada planeta tiene un **`_mapa-estelar.md`** que lista sus misiones activas y dashboards Dataview.
8. **CardBoard** ofrece Tag boards (vista Kanban por estado) que usan los tags `#pendiente`/`#en-espera`/`#bloqueada`/`#completada` como columnas.
9. Las tareas que surgen sin contexto van a **`nebulosa-mental/destellos.md`**.
10. Un agente IA lee **`skill/control-de-mision.md`** al inicio de cada chat para entender el sistema y operar sobre los archivos.

---

## Flujo de interacción

- **Obsidian** es la interfaz de lectura: dashboards Dataview, Tag boards de CardBoard, navegación visual.
- **Cowork / agente IA** es la interfaz de escritura: le hablas en lenguaje natural y el agente crea, edita, completa y mueve tareas en los archivos.
- El agente siempre confirma antes de modificar archivos (regla `CONFIRMA ANTES DE ACTUAR` en la skill).
- `notas.md` es la captura rápida al vuelo cuando no hay tiempo de abrir chat; se procesa por lotes después.

---

## Plugins de Obsidian

| Plugin | Rol |
|---|---|
| **Dataview** (esencial, con Dataview JS habilitado) | Queries vivas en `universo.md` y mapas estelares. Dataview JS habilita scripts que pueden modificar archivos — base técnica para la futura sincronización automática de dependencias. |
| **CardBoard** (esencial) | Tag boards (Kanban por estado) y Date boards (vista por fecha). Lee los `- [ ]` de los archivos y el frontmatter para agrupar tarjetas. |
| **Full Calendar** (esencial) | Vista calendario de las tareas del vault por fecha. Complementaria a Google Calendar. |
| **Google Calendar** | Muestra Google Calendar dentro de Obsidian (tareas externas de ClickUp, reuniones). Plugin en modo stale pero funcional. |
| **Minimal (tema) + Style Settings** | Tema visual limpio y profesional, personalizable sin código. |

### CSS Snippets

En `.obsidian/snippets/` hay CSS personalizado activo. Ver `.obsidian/snippets/README.md` para el listado y descripción de cada snippet. Actualmente:

- **`cardboard-hide-tags.css`** — Oculta la fila de tags que CardBoard muestra encima de cada tarjeta, para evitar ruido visual de los tags organizacionales (`#enter-tech-school`, `#app-enterbase`, etc.). Los tags siguen alimentando Tag boards y queries Dataview normalmente.

---

## Filosofía

- Las herramientas se adaptan a cómo pienso, no al revés.
- Contexto y tareas conviven juntos, nunca separados.
- Empezar simple, escalar cuando haga falta.
- Sin categorías complejas, sin nomenclatura rígida.
- Los archivos `.md` son míos — funcionan con o sin Obsidian.
- El sistema existe para quitarme peso mental, no para agregarlo.
