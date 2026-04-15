# Propuesta: Skill de Automatización — "Control de Misión"

> **Estado: IMPLEMENTADA** — La skill fue construida el 2026-04-13 como `control-de-mision.md` en la raíz del vault.
> Este documento se conserva como referencia del diseño original.

---

## Qué es esta skill

Una skill de Cowork es un archivo de instrucciones que el modelo IA lee al inicio de cada conversación. Cuando abres un chat con tu vault conectada, el modelo ya sabe: quién eres, cómo funciona tu sistema, qué estructura tiene tu vault, y qué acciones puede realizar sobre tus archivos.

No necesitas un MCP especial para Obsidian. El agente (Cowork, Claude Code, u otro) simplemente abre la carpeta del vault y edita los archivos .md directamente.

---

## Flujo general

```
Tú abres el chat con la carpeta del vault conectada
        ↓
El modelo lee la skill "Control de Misión"
        ↓
La skill le indica leer el estado actual del vault:
  - README.md (entiende la estructura y glosario)
  - context/yo.md (entiende quién eres)
  - universo.md + mapas estelares (entiende qué hay pendiente)
        ↓
El modelo te saluda con un resumen breve del estado actual
  Ejemplo: "Tienes 3 tareas pendientes en Enter Tech School,
            2 destellos sin procesar y 1 tarea para hoy."
        ↓
Tú hablas en lenguaje natural, el modelo actúa
```

---

## Acciones que la skill debe manejar

### 1. Crear tareas desde lenguaje natural

**Tú dices:**
> "Tengo que hacer el testing del formulario de matriculados para el viernes, y también necesito revisar el diseño del landing con el equipo de marketing"

**El modelo hace:**
- Detecta 2 tareas
- Identifica que ambas son de Enter Tech School
- Te pregunta a qué misión pertenece cada una (o propone si es obvio)
- Si la misión no existe, ofrece crearla
- Agrega las tareas con formato `- [ ]` y fecha con doble formato `(18-abr-2026) 📅 2026-04-18` si aplica
- Actualiza el aclarador de cada misión afectada

---

### 2. Completar tareas

**Tú dices:**
> "Ya terminé el testing del formulario"

**El modelo hace:**
- Busca la tarea en los archivos del vault
- Cambia `- [ ]` a `- [x]`
- Actualiza el aclarador de esa misión reflejando el avance
- Te confirma: "Marcada como completada en bootcamp.md. Actualicé el aclarador."

---

### 3. Editar tareas

**Tú dices:**
> "La exportación de datos ya no depende de Gabriela, ahora la hace Carlos y es para el miércoles"

**El modelo hace:**
- Encuentra la tarea en el archivo correspondiente
- Actualiza la descripción y la fecha
- Actualiza el aclarador si el contexto cambió
- Te confirma los cambios

---

### 4. Mover tareas entre planetas

**Tú dices:**
> "Eso de estudiar el curso de React no es un destello, ponlo como misión en mis-proyectos-dev"

**El modelo hace:**
- Elimina la tarea de `nebulosa-mental/destellos.md`
- Crea un nuevo archivo `mis-proyectos-dev/curso-react.md` usando la plantilla de misión
- Agrega la tarea ahí
- Te confirma

---

### 5. Capturar destellos rápidos

**Tú dices:**
> "Acuérdate que tengo que comprar comida para el perro y renovar el antivirus"

**El modelo hace:**
- Agrega ambas como tareas en `nebulosa-mental/destellos.md`
- No pregunta a qué planeta van — es captura rápida
- Te confirma: "2 destellos capturados."

---

### 6. Crear nuevas misiones

**Tú dices:**
> "Voy a empezar un proyecto nuevo en el trabajo, se llama Plataforma B2B, es para hacer un sistema de facturación para clientes empresariales"

**El modelo hace:**
- Crea `enter-tech-school/plataforma-b2b.md` usando la plantilla de misión
- Escribe un aclarador inicial basado en lo que le dijiste
- Agrega el link en `enter-tech-school/_mapa-estelar.md` bajo "Misiones activas"
- Te confirma y pregunta si quieres agregar tareas iniciales

---

### 7. Consultar estado

**Tú dices:**
> "¿Qué tengo pendiente para hoy?"
> "¿Cómo va el bootcamp?"
> "¿Qué hay en mi nebulosa?"

**El modelo hace:**
- Lee los archivos relevantes
- Te da un resumen en lenguaje natural (no te pega el markdown crudo)
- Si hay tareas con fecha vencida, te avisa

---

### 8. Crear aclarador diario

**Tú dices:**
> "Hoy fue un día complicado. Avancé con el formulario pero me quedé trabado en el testing. Mañana tengo que hablar con Carlos sobre la exportación. También se me ocurrió que debería automatizar el deploy."

**El modelo hace:**
- Crea `aclarador-diario/2026-04-13.md` usando la plantilla
- Llena las secciones basándose en lo que le dijiste
- Detecta la idea del deploy y pregunta: "¿La idea del deploy la agrego como destello o como tarea en alguna misión?"

---

### 9. Revisión semanal asistida

**Tú dices:**
> "Hagamos la revisión semanal"

**El modelo hace:**
- Lee todos los mapas estelares y destellos
- Te presenta un resumen:
  - Tareas completadas esta semana (tu progreso)
  - Tareas pendientes por planeta
  - Destellos sin procesar
  - Misiones sin actividad reciente
- Te guía destello por destello: "Tienes 'comprar comida para el perro'. ¿Lo muevo a algún planeta, lo dejo aquí, o lo descarto?"
- Actualiza los aclaradores de misiones activas si hay cambios

---

### 10. Archivar/cerrar misiones

**Tú dices:**
> "El proyecto del bootcamp ya terminó"

**El modelo hace:**
- Te pregunta si quieres archivarlo o eliminarlo
- Si archiva: mueve el archivo a una carpeta `_archivo/` (o lo marca con un tag)
- Actualiza el mapa estelar removiendo el link
- Te confirma

---

## Lo que la skill NO hace sin preguntar

- **No crea planetas nuevos** sin tu aprobación
- **No elimina tareas** — solo las marca como completadas o las mueve
- **No asume a qué misión pertenece algo** si hay ambigüedad — pregunta
- **No modifica `yo.md`** ni `contexto-inicial-gestion.md` — los documentos fundacionales son tuyos

---

## Contexto inicial que la skill lee al arrancar

La skill debe instruir al modelo a leer estos archivos al inicio de cada chat:

1. `README.md` — Entiende la estructura, el glosario, la filosofía
2. `context/yo.md` — Entiende quién eres y cómo tratarte (especialmente: no alimentar al perfeccionista)
3. Cada `_mapa-estelar.md` — Entiende el estado actual de cada planeta
4. `nebulosa-mental/destellos.md` — Sabe qué anda suelto

Esto le da al modelo un snapshot completo de tu universo en cada conversación nueva.

---

## Plugins de Obsidian recomendados para este flujo

Dado que **Obsidian es tu interfaz de lectura** y **Cowork/IA es tu interfaz de escritura**, los plugins que necesitas son:

### Esenciales

| Plugin | Para qué | Por qué lo necesitas |
|---|---|---|
| **Tasks** | Renderiza los bloques ` ```tasks``` ` en los dashboards | Sin esto, universo.md y los mapas estelares son texto plano. Con esto, son vistas vivas de tus tareas |
| **Dataview** | Queries más avanzadas (listar misiones activas, contar tareas por estado, etc.) | Complementa a Tasks para vistas que Tasks no puede hacer solo |

### Útiles pero no urgentes

| Plugin | Para qué | Cuándo instalarlo |
|---|---|---|
| **Templater** | Crear misiones nuevas desde plantilla con un click dentro de Obsidian | Cuando quieras crear misiones rápidas sin pasar por el chat |
| **Calendar** | Vista de calendario en la sidebar para navegar tus aclaradores diarios | Cuando tengas varios aclaradores diarios y quieras navegar por fecha |
| **Kanban** | Vista de tablero para misiones | Cuando quieras visualizar estados de misiones (activa, pausada, completada) |

### NO necesarios en este flujo

| Plugin | Por qué no |
|---|---|
| **Google Calendar Sync** | Si Cowork es quien gestiona tus fechas, la sync con Google Calendar se podría manejar de otra forma más adelante. No es prioritario. |

---

## Preguntas abiertas

Antes de construir la skill, necesito que decidas:

### 1. Tono del modelo al inicio
¿Quieres que al abrir el chat el modelo te dé un resumen automático del estado del vault, o prefieres que espere a que tú hables primero?

### 2. Confirmación de acciones
¿Quieres que el modelo te confirme ANTES de hacer cambios ("Voy a marcar X como completada y actualizar el aclarador, ¿procedo?") o que actúe y después te diga qué hizo?

### 3. Lenguaje del modelo
¿El modelo te habla formal, casual, o como un copiloto amigo? ¿Usa la metáfora astronómica ("Misión completada, aclarador actualizado") o habla directo?

### 4. Nombre de la skill
¿"Control de Misión" te gusta o prefieres otro nombre?

---

> **Siguiente paso:** Responde las preguntas abiertas, y construyo la skill real (el archivo SKILL.md + instrucciones).
