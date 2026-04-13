# Contexto inicial: Sistema de gestión personal y profesional

## Sobre mí

Soy programador y trabajo en **Enter Tech School** (entertechschool), una plataforma de educación tecnológica. Mi rol abarca diseño, marketing y operaciones técnicas, incluyendo UX/UI, diseño gráfico y configuración de herramientas de desarrollo.

Manejo Git, GitHub, SSH, y tengo experiencia con desarrollo web, automatización de procesos y flujos de trabajo técnicos. Uso Windows como sistema operativo principal y Android como dispositivo móvil.

---

## Mi filosofía de organización

Soy **minimalista**. Rechazo herramientas sobrecargadas. Mi experiencia con ClickUp fue frustrante: demasiadas funcionalidades, demasiado ruido visual, demasiadas opciones que no necesito. Lo mismo aplica para Notion en cierta medida — lo uso para apuntes porque el formato visual de markdown es excelente, pero lo considero pesado: se demora en cargar, no es ligero al abrir la app.

**Quiero herramientas que se adapten a cómo pienso, no adaptar mi pensamiento a una herramienta.**

---

## Cómo organizo mis tareas actualmente

Mi sistema natural es dividir todo en **secciones temáticas**. Cada sección agrupa tareas y notas relacionadas. Ejemplos de secciones:

- **Trabajo** — Tareas del día a día en Enter Tech School
- **Personal** — Metas, compras, trámites
- **Mañana** — Lo que debo hacer al día siguiente
- Otras secciones según necesidad

### Dentro de cada sección

Combino **texto libre** (para aclarar mi mente, dar contexto, pensar en voz alta) con **listas de tareas** concretas. No separo las notas de las tareas — conviven juntas porque el contexto es parte de la tarea.

### Ejemplo real de cómo escribo

```markdown
## Sobre el bootcamp
Estoy esperando la reunión del viernes para mostrar avances.
El tema del testing es clave porque sin eso no podemos 
validar nada del formulario. Gabriela aún no responde 
sobre la exportación, hay que esperar.

- Formulario de Matriculados: Está en su rama feature respectiva, 
      eso se mostrará en la reunión, aún falta realizar el test respectivo.
      REQUIERE: Crear la skill de Test para proyectos
- Adiciones de Filtro de fechas: Implementado y en main, 
      las chicas ya tienen los avances ✅
- Exportación de datos: La de Gabriela está en curso, 
      se implementará una vez se tenga respuesta de Gabriela. 
      Las demás se posponen hasta resultado ...
```

**Puntos clave de este formato:**
- Uso markdown de forma natural, no forzada
- La prosa libre y las tareas (`- [ ]`) conviven en el mismo archivo
- Las tareas tienen contexto y dependencias escritas en lenguaje natural
- Uso checkboxes de markdown como indicador de completado
- A veces uso emojis como ✅ para marcar cosas terminadas inline

---

## Herramienta elegida: Obsidian

Después de evaluar múltiples alternativas (Anytype, Notion, TickTick, GitHub Projects), elegí **Obsidian** por estas razones:

1. **Markdown puro** — Los archivos `.md` son míos, viven en mi disco, los puedo editar con cualquier editor
2. **Git como sincronización** — Mi vault de Obsidian ES un repositorio de GitHub. Sincronizo entre Windows y Android usando Git (gratis)
3. **Control total** — Yo diseño la estructura, las convenciones, todo
4. **Plugins para tareas** — El plugin Tasks detecta checkboxes (`- [ ]`) en todos mis archivos y permite hacer queries, filtros, y dashboards
5. **Kanban** — El plugin Kanban o Task Board me da vista de tablero sin duplicar información
6. **Google Calendar** — Existe plugin de sync (Obsidian → Google Calendar) para tareas con fecha
7. **Sin vendor lock-in** — Si Obsidian desaparece mañana, mis `.md` siguen funcionando

### Lo que NO busco en Obsidian
- No necesito que sea bonito — necesito que sea funcional
- No necesito templates elaborados — prefiero crear mi propia estructura
- No necesito colaboración en tiempo real — esto es para gestión personal y de mis tareas de trabajo

---

## Qué necesito que hagas

Necesito que me ayudes a **diseñar la estructura de carpetas y archivos** de mi vault de Obsidian, considerando:

### Estructura de carpetas
- Debe reflejar mis secciones naturales (Trabajo, Personal, etc.)
- Debe ser escalable pero empezar simple
- Las carpetas deben tener sentido para mí, no para un sistema genérico

### Convenciones de archivos
- Cómo nombrar archivos (formato de nombres)
- Qué headers/estructura interna usar en cada tipo de nota
- Dónde van las tareas vs las notas libres vs los dashboards
- Cómo uso tags si los necesito

### Sistema de tareas
- Las tareas deben vivir dentro de mis notas con contexto (no en archivos separados de solo tareas)
- Necesito poder ver todas las tareas pendientes desde un dashboard central
- Necesito secciones tipo "Hoy", "Esta semana", "Por proyecto"
- El formato debe ser compatible con el plugin Tasks de Obsidian (`- [ ]` con metadatos como 📅 para fechas)

### Integración con Google Calendar
- Las tareas con fecha deben poder sincronizarse con Google Calendar
- Definir convención de cómo agregar fechas a las tareas

### Flujo diario
- Cómo debería verse mi rutina diaria de gestión en este sistema
- Dónde capturo ideas rápidas vs tareas formales
- Cómo hago revisión semanal

---

## Contexto técnico adicional

- **SO:** Windows (principal), Android (móvil)
- **Sync:** Git + GitHub (repo privado)
- **Editor:** Obsidian (desktop + mobile)
- **Plugins previstos:** Tasks, Kanban o Task Board, Google Calendar Sync, posiblemente Dataview
- **Lenguaje de notas:** Español
- **Proyectos actuales en el trabajo:** Bootcamp (formularios, filtros, exportación), Proyecto B2B, Homepage de Enter Tech School

---

## Lo que NO quiero

- ❌ Sistemas complejos con demasiadas categorías
- ❌ Nomenclatura rígida tipo `YYYY-MM-DD_proyecto_v2_final_FINAL`
- ❌ Separar tareas de su contexto en archivos diferentes
- ❌ Depender de plugins frágiles para funcionalidad básica
- ❌ Que la estructura me genere más trabajo del que me ahorra
