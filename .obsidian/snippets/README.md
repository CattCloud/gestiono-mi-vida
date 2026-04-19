# CSS Snippets — Vault Gestiono mi vida

Esta carpeta contiene snippets CSS personalizados que modifican la apariencia de Obsidian y sus plugins. Obsidian los detecta automáticamente, pero hay que activarlos manualmente en:

> **Settings → Appearance → CSS snippets**

Cada snippet aparece con un toggle. Activado = se aplica. Desactivado = no afecta nada.

---

## Snippets instalados

### `cardboard-hide-tags.css`

Oculta la fila de tags que aparece encima de cada tarjeta del plugin CardBoard.

**Problema que resuelve:** CardBoard muestra por defecto todos los tags del archivo (frontmatter + línea de la tarea) encima de cada tarjeta. Los toggles del plugin (`Show filter tags on cards`, `Show column tags on cards`) solo ocultan los que cumplen esos roles específicos; los tags organizacionales como `#enter-tech-school`, `#app-enterbase`, `#formulario-matriculados` siempre quedan visibles y generan ruido visual.

**Qué hace:** oculta la fila completa de tags en las tarjetas de CardBoard. Los tags siguen en los archivos y siguen alimentando los Tag boards y las queries de Dataview; solo se ocultan visualmente.

**Cuándo desactivarlo:** si alguna vez necesitas ver los tags directamente en la tarjeta (por ejemplo para debuggear por qué una tarea cae o no en cierta columna), desactiva el toggle temporalmente.

---

## Cuándo agregar un snippet nuevo

Cuando el ajuste deseado no se puede hacer desde los settings de Obsidian ni de un plugin. Ejemplos razonables: ocultar un elemento visual, cambiar tipografías específicas, ajustar márgenes de tarjetas Kanban, etc.

Cada snippet nuevo debería:

1. Vivir en su propio archivo `.css` con un nombre descriptivo (ej. `calendar-compact-weekends.css`).
2. Tener un docstring al inicio explicando qué hace, por qué, y cuándo desactivarlo.
3. Quedar listado en este README con una sección propia.
