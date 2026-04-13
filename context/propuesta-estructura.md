# Propuesta: Estructura del Vault — "Mi Universo"

> **Estado: IMPLEMENTADA** — Esta propuesta fue aprobada y construida el 2026-04-13.
> Los archivos del sistema ya existen en el vault. Este documento se conserva como referencia del diseño original.

---

## La metáfora (sutil)

| Concepto real | Nombre astronómico | Para qué sirve |
|---|---|---|
| Vista global de todo | **Universo** | Dashboard principal: "¿qué tengo hoy en todas las áreas?" |
| Área de vida | **Planeta** | Cada gran zona: enter-tech-school, mis-proyectos-dev, mis-sistemas-identidad, nebulosa-mental |
| Vista por área | **Mapa estelar** | Dashboard de un planeta específico: "¿qué pasa solo en Trabajo?" |
| Proyecto específico | **Misión** | Cada proyecto dentro de un planeta (ej: Bootcamp, mi app personal) |
| Registro diario | **Aclarador diario** | Tu reflexión del día: qué hiciste, qué falta, cómo estás |
| Área de tareas sueltas | **Nebulosa** | Lo que anda disperso, tareas sin planeta definido |
| Captura rápida | **destellos.md** | El archivo donde aterrizan esas tareas sueltas |

La metáfora vive en los **nombres de las vistas y carpetas**, no en cada línea que escribes. El contenido de tus notas sigue siendo tuyo, en tu lenguaje natural.

---

## Estructura de carpetas

```
gestiono-mi-vida/
│
├── README.md                    ← Describe el proyecto: qué es, cómo funciona, glosario
├── universo.md                  ← Dashboard global ("¿qué tengo hoy?")
│
├── enter-tech-school/           ← 🪐 Planeta Trabajo
│   ├── README.md                ← Describe de qué trata este planeta
│   ├── _mapa-estelar.md         ← Vista general de este planeta
│   ├── bootcamp.md              ← Misión: cada proyecto es un archivo
│   ├── otro-proyecto.md         ← (los creas cuando surjan)
│   └── ...
│
├── mis-proyectos-dev/           ← 🪐 Planeta Proyectos Personales
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── mi-app.md
│
├── mis-sistemas-identidad/      ← 🪐 Planeta Sistemas / Hábitos
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── habito-lectura.md        ← Cada sistema/hábito es un archivo
│
├── nebulosa-mental/             ← 🌫️ Lo que anda disperso en tu mente
│   ├── README.md
│   ├── _mapa-estelar.md
│   └── destellos.md             ← Captura rápida: tareas sueltas van aquí
│
├── aclarador-diario/            ← 📓 Aclaradores diarios (opcional)
│   ├── README.md
│   └── 2026-04-12.md
│
├── context/                     ← 📜 Documentos fundacionales del sistema
│   ├── yo.md                    ← Tu documento de autoconocimiento
│   └── contexto-inicial-gestion.md ← La especificación original del proyecto
│
├── _plantillas/                 ← Plantillas reutilizables
│   ├── plantilla-mision.md      ← Template para crear un proyecto nuevo
│   └── plantilla-aclarador.md   ← Template para aclarador diario
```

### Principios de esta estructura

1. **Un proyecto = un archivo.** El archivo del proyecto contiene TODO: el aclarador, las tareas, el contexto. No se fragmenta.
2. **Las carpetas son tus planetas.** Cuando dices "ahora solo Enter Tech School", abres esa carpeta y el resto no existe.
3. **`README.md`** en cada carpeta describe de qué trata ese planeta: su propósito, qué tipo de misiones viven ahí, cualquier contexto útil.
4. **`_mapa-estelar.md`** empieza con `_` para que aparezca arriba. Es tu dashboard de esa área con queries de tareas.
5. **`nebulosa-mental/destellos.md`** es tu red de seguridad. ¿Se te ocurrió algo? Va ahí. Después en la revisión semanal decides si se queda, se mueve a un planeta o se descarta.
6. **`aclarador-diario/`** es opcional. Si te funciona escribir tu reflexión del día, genial. Si no, no pasa nada — tus tareas ya viven en los proyectos.

---

## Formato de un archivo de proyecto (Misión)

Así se vería `enter-tech-school/bootcamp.md`:

```markdown
---
tags: [trabajo, bootcamp]
---

# Bootcamp

## Aclarador
Estoy esperando la reunión del viernes para mostrar avances.
El tema del testing es clave porque sin eso no podemos validar nada
del formulario. Gabriela aún no responde sobre la exportación.

## Tareas

- [ ] Formulario de Matriculados: mostrar en la reunión, falta test 📅 2026-04-18
  - REQUIERE: Crear la skill de Test para proyectos
- [x] Adiciones de Filtro de fechas: Implementado y en main ✅
- [ ] Exportación de datos (Gabriela): en curso, esperando respuesta ⏳
- [ ] Exportación de datos (las demás): pospuesto hasta resultado de Gabriela

## Notas
(espacio libre para lo que surja sobre este proyecto)
```

### Lo que hace este formato

- **Tags** en el frontmatter → permiten filtrar desde el dashboard global
- **Aclarador** → tu prosa libre, cómo piensas, qué está pasando
- **Tareas** → formato `- [ ]` compatible con Obsidian Tasks
- **📅** → fecha de vencimiento (la lee el plugin Tasks)
- **⏳** → indicador visual de "esperando algo" (opcional)
- **Notas** → espacio libre para lo que surja

---

## Los dashboards: cómo ver todo sin perderte

### `universo.md` — Vista global

Usa queries del plugin Tasks de Obsidian para jalar tareas de TODOS los archivos:

```markdown
# 🌌 Universo

## Hoy
(query: tareas con fecha de hoy, de cualquier carpeta)

## Pendientes por planeta
### Enter Tech School
(query: tareas pendientes en carpeta enter-tech-school/)

### Mis proyectos dev
(query: tareas pendientes en carpeta mis-proyectos-dev/)

### Mis sistemas identidad
(query: tareas pendientes en carpeta mis-sistemas-identidad/)

### Nebulosa mental
(query: tareas pendientes en carpeta nebulosa-mental/)
```

### `_mapa-estelar.md` — Vista por área

Cada planeta tiene su mapa estelar. Ejemplo para `enter-tech-school/_mapa-estelar.md`:

```markdown
# 🪐 Mapa estelar — Enter Tech School

## Misiones activas
(links a los proyectos activos)

## Tareas pendientes
(query: todas las tareas pendientes en carpeta enter-tech-school/)

## Esperando respuesta
(query: tareas con ⏳ en carpeta enter-tech-school/)
```

---

## Flujo diario propuesto

### Al empezar el día
1. Abre `universo.md` → mira qué tienes para hoy en todas las áreas
2. Decide en qué planeta enfocarte → abre esa carpeta

### Durante el día
3. Trabajas en el archivo del proyecto directamente
4. ¿Surgió algo random? → `nebulosa-mental/destellos.md`, escríbelo y sigue
5. Completas tareas → marcas `[x]`

### Al cerrar el día (opcional)
6. Si usas aclarador diario: escribe en `aclarador-diario/2026-04-12.md` tu reflexión del día
7. Si no: simplemente actualiza los aclaradores de los proyectos que tocaste

### Revisión semanal (10-15 min)
8. Revisa `nebulosa/destellos.md` → mueve a un planeta, descarta o crea misiones nuevas
9. Revisa cada `_mapa-estelar.md` → ¿hay misiones estancadas? ¿prioridades que cambiaron?
10. Actualiza aclaradores de proyectos activos

---

## Sobre el historial de tareas completadas

Las tareas que marcas con `[x]` **no desaparecen** — se quedan en el archivo del proyecto. El plugin Tasks puede hacer queries de tareas completadas. Más adelante, cuando tengas historial suficiente, podemos crear una vista de "patrones" que analice qué tipo de tareas sueles tener en la Nebulosa para detectar si merece crear un planeta nuevo.

---

## Plugins necesarios (por orden de prioridad)

1. **Tasks** — fundamental. Lee los `- [ ]` y permite queries/filtros
2. **Dataview** (recomendado) — queries más potentes para los dashboards
3. **Kanban** o **Task Board** — vista de tablero (no urgente, puede esperar)
4. **Google Calendar Sync** — para tareas con fecha (puede esperar)
5. **Templater** — para usar las plantillas al crear archivos nuevos (útil pero no urgente)

---

## Lo que NO tiene este sistema (a propósito)

- ❌ No hay categorías complejas ni taxonomías
- ❌ No hay nomenclatura rígida de archivos
- ❌ No separa tareas de contexto
- ❌ No requiere plugins para funcionar (los plugins mejoran la experiencia pero sin ellos los .md siguen siendo legibles)
- ❌ No hay más estructura de la necesaria para empezar

---

> **Siguiente paso:** Revisa esta propuesta. Dime qué te gusta, qué cambiarías, qué sobra, qué falta. Después la construimos juntos.
