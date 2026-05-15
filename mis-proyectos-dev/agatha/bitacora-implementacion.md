---
título: Bitácora de implementación — Agatha
proyecto: Agatha
audiencia: Claude Code (escritor) + Erick (revisor)
estado: activa
creada: 2026-05-01
---

# Bitácora de implementación — Agatha

> Diario técnico de Claude Code durante la implementación del MVP.
> Registra decisiones técnicas no triviales, hallazgos de la
> implementación, y decisiones consultadas con el usuario.
>
> **No es un changelog** (eso vive en git).
> **No es un plan** (eso vive en `etapa-5-brief-implementacion.md`).
> Es **el porqué** de las decisiones que se toman durante el desarrollo.

---

## Para qué sirve este archivo

Cuando Erick revise el código en el futuro y se pregunte "¿por qué Claude Code eligió esta librería?" o "¿por qué este patrón y no otro?", la respuesta vive acá. La bitácora cubre el espacio entre git (qué cambió) y el brief (qué hay que hacer): **por qué se decidió así**.

También sirve para el caso inverso: cuando Erick necesite cuestionar o revertir una decisión, esta bitácora le da el contexto completo para hacerlo con criterio.

---

## Convenciones

**Una entrada por decisión, no una por commit.** Si una decisión se materializa en 5 commits, sigue siendo una entrada. Si un commit toma 3 decisiones independientes, son 3 entradas.

**Granularidad de qué registrar:**

- ✅ **Sí registrar:** elección de librería, patrón arquitectónico, decisión técnica que el brief delegó al implementador, hallazgo durante implementación que cambia el plan, decisión consultada con Erick.
- ❌ **No registrar:** detalles de naming de variables, decisiones de formato, refactors triviales, fixes de bugs propios. Eso vive en git.

**Formato de cada entrada:**

```markdown
### YYYY-MM-DD — [Título corto] #fase-X
**Decisión:** [qué se decidió, una línea]
**Por qué:** [una o dos líneas con la razón principal]
**Alternativas consideradas:** [si hubo, breve]
**Documentos afectados:** [si la decisión modifica algún doc del repo]
**Consultado con Erick:** sí (fecha) / no
```

**Tags de fase disponibles:** `#fase-0`, `#fase-1`, `#fase-2`, `#fase-3`, `#fase-4`, `#fase-5`. Si una decisión cruza fases, usar la fase donde se tomó.

**Cuando consultar con Erick:** usar el flujo de la sección 7 del brief de Etapa 5. Decisiones mayores (arquitectura, UX visible, costos) **siempre** se consultan antes de tomarse y se registran después con `Consultado con Erick: sí`.

---

## Entradas

> Las entradas se agregan en orden cronológico, las más recientes arriba.

### 2026-05-08 — Calibración de voz: sin voseo, con emojis/gestos, con sarcasmo ingenioso #fase-6

**Decisión:** Cuatro cambios al skill runtime de Agatha (`skill/control-de-mision.md`) basados en feedback de uso real.
1. **Voz neutral peruana sin voseo argentino.** §3 ya decía "usa tú (registro peruano cálido)" pero el modelo no la respetaba porque §4 (saludo) y §5 (acciones) estaban en voseo masivo — el patrón ganaba sobre la regla. Refuerzo en §3 con tabla explícita de qué usar / qué evitar ("tienes" no "tenés", "avisa" no "avisá", "dime" no "decime", "muévele" no "movele"). Limpieza pasada por pasada en §4 (ejemplos de saludo) y §5 (instrucciones operativas + ejemplos de comandos del usuario). Voseo restante deliberado: solo en la columna "NO usar" de la tabla anti-ejemplos.
2. **Apertura explícita a emojis** en respuestas de Agatha. Antes no había regla; el modelo los usaba ocasionalmente (ej. 💙 al cerrar un mensaje cálido). Ahora la skill lo enuncia: emojis bienvenidos cuando suman al momento, no en cada mensaje, sí en los que llevan emoción genuina.
3. **Gestos textuales entre asteriscos** explícitamente bienvenidos en momentos íntimos (`*te devuelve el abrazo*`, `*sonríe*`, `*asiente despacio*`). Para los momentos humanos, no para respuestas operativas. Da vida a la conversación.
4. **Sarcasmo ingenioso permitido bajo cinco reglas.** Subsección nueva en §3 ("Humor y sarcasmo ingenioso") que enuncia el permiso con guardrails: apunta a los 3 Bosses / situaciones / ideas — nunca a Erick como persona; co-conspira con Erick contra sus Bosses; solo en estado operativo o ligero (apagado en bajón profundo); acompañado de calidez o gesto textual; especia no plato principal. Incluye 3 ejemplos válidos y 4 anti-ejemplos para anclar la línea entre ingenioso y ácido.

**Por qué:** Feedback directo de Erick tras conversación real con Agatha 2026-05-07. Los argentinismos rompían la intimidad — Erick es peruano y el voseo se siente ajeno. Los emojis y gestos le dan vida al lazo conversacional y refuerzan el "no es asistente, es compañía". El sarcasmo ingenioso encaja con su personalidad analítica y, bien calibrado, sirve como herramienta para desactivar a los 3 Bosses (Agatha y Erick riéndose juntos del perfeccionista en lugar de combatirlo con argumentos solemnes).

**Alternativas consideradas:**
- Para el voseo: cambio quirúrgico (solo §3 + §4) — descartado porque el modelo absorbe patrones léxicos de todo el skill, no solo de los ejemplos. La regla no alcanza si los ejemplos la contradicen.
- Para el sarcasmo: mencionarlo en pasada dentro de "Voz" sin reglas formales — descartado porque el modelo IA tiende a sobrejugar cuando se le da permiso amplio. La línea ingenioso/ácido es delgada y necesita guardrails concretos.

**Documentos afectados:** `skill/control-de-mision.md` (§3 Voz + Registro lingüístico + Gestos + Humor y sarcasmo, §4 ejemplos saludo, §5.1 a §5.11 limpieza pasada).
**Consultado con Erick:** sí (2026-05-08, dos preguntas separadas: limpieza de voseo + apertura al sarcasmo).

### 2026-05-08 — Iteración 4: columna "Futuro" + badge VENCIDA (B36 + B37) #fase-6

**Decisión:** Dos cambios en el DateBoard para manejar tareas con fechas no-hoy.
1. Columna "Mañana" renombrada a "Futuro" y ampliada para incluir todas las tareas con fecha posterior a hoy (no solo mañana), ordenadas cronológicamente ascendente. Las tareas del día+2 en adelante ya no quedan atrapadas en "Sin fecha".
2. Tareas con fecha pasada (vencidas) se muestran en la columna HOY con badge "VENCIDA" en terracota (`#f2e8e1` / `#8b4020`) en lugar del badge "HOY". La prevalencia de badges queda: bloqueada/en-espera > VENCIDA > HOY.

**Por qué:** Sin este cambio, las tareas vencidas desaparecían de la vista (iban a "Sin fecha") y las futuras tardías también. El tono terracota respeta el anti-objetivo "sin culpa": no es rojo alarma, es un recordatorio cálido.
**Alternativas consideradas:** Para VENCIDA: gris reflexivo (tokens existentes) o mismo naranja que HOY. Erick eligió terracota (token nuevo) por ser cálido pero distinguible del badge HOY.
**Documentos afectados:** dos tokens nuevos en `variables.css` (`--color-vencida-bg/text`). Helpers `esVencida` y `esFutura` en `src/domain/fechas.ts`.
**Consultado con Erick:** sí (2026-05-08)

### 2026-05-07 — UX post-uso-real: color peso en chat, fechas DD-MM-YYYY, botón editar #fase-6

**Decisión:** Tres mejoras de UX detectadas durante el uso real de la V1.
1. Emojis de peso (🟡🟣🟠) en burbujas del chat reemplazados por dots CSS con los colores del design system. El 🟣 nativo es lila; el sistema usa `#E08D9C` (rosa) para peso 2 — el emoji y el token nunca coincidieron visualmente. Solución: `procesarTexto` + `components` de ReactMarkdown intercepta los nodos de texto y sustituye cada emoji con un `<span>` con `background: var(--color-weight-N)`.
2. Fechas ISO (`YYYY-MM-DD`) en respuestas de Agatha se reformatean a `DD-MM-YYYY` antes del render. Solo afecta nodos de texto del markdown (code blocks quedan intactos). Regex `\b(\d{4})-(\d{2})-(\d{2})\b` → `$3-$2-$1`.
3. Botón "Editar en Agatha" en el footer del `TaskDrawer`. Al hacer clic: cierra el drawer, abre el chat con mutual exclusión animada existente, y pre-llena el borrador con `Editá la tarea "[titulo]": ` listo para dictar el cambio.

**Por qué:** Feedback directo de Erick tras uso real. El color lila rompía la coherencia del design system. El formato ISO es interno del vault y no debería exponerse al usuario. El botón de editar cierra el gap entre "ver tarea" y "pedirle un cambio a Agatha".
**Alternativas consideradas:** Para los emojis, se evaluó cambiar el token `--color-weight-2` a morado (alinear con el emoji en vez de al revés) — descartado porque la guía visual ya tiene rosa definido y calibrado. Para las fechas, se evaluó pre-procesar el string completo antes de ReactMarkdown — descartado porque afectaría code blocks.
**Documentos afectados:** ninguno (cambios de presentación, sin impacto en skill ni guía visual).
**Consultado con Erick:** sí (2026-05-07)

### 2026-05-05 — Tool `editar_tarea` — edición de campos del frontmatter #fase-5

**Decisión:** Nueva tool `editar_tarea` con campos opcionales (`titulo`, `peso`, `fechaTipo`, `fechaInicio`, `fechaFin`). Una sola tool unificada en vez de tools separadas por campo.

**Por qué:**
- El caso que motivó la pieza: Agatha no podía mover fechas de tareas atrasadas y tenía que dictarle a Erick los cambios manuales.
- Una tool unificada permite que el modelo agrupe varios cambios en un único tool call (e.g., cambio de fecha + peso) → una sola pasada line-based, un solo rename atómico. Tools separadas implicarían N escrituras al mismo archivo.
- `Option<T>` en cada campo: `None` = no cambiar, `Some(valor)` = reemplazar. Idempotente: si el nuevo contenido == contenido original, no-op.

**Decisiones técnicas:**
- **Cambio de título no renombra el archivo.** El `id`/`rutaArchivo` es el contrato estable con `bloqueada_por`/`desbloquea` (que referencian por slug del nombre). Renombrar el archivo rompería esas referencias. El título se cambia solo en el H1 del body y la línea CardBoard.
- **Coherencia según `fechaTipo`:** al cambiar `fechaTipo` a `sin-fecha`, la tool fuerza `fechaInicio=""` y `fechaFin=""` internamente (override). `vence` → limpia `fechaInicio`. `exacta` → limpia `fechaFin`. `rango` → conserva ambas. Esto se aplica en Rust antes de iterar las líneas.
- **Patrón heredado de `marcar_completada`:** line-based puro con `split_inclusive('\n')`, detección de frontmatter por dos `---`, BOM-safe, `watcher::suprimir` antes del rename atómico, `escribir_atomico` (temp + fsync + rename).
- **CardBoard matcher:** `linea.trim_start().starts_with("- [ ]")` o `starts_with("- [x]")` — el mismo patrón endurecido en F-22, descarta menciones del pattern en inline code.

**Alternativas consideradas:**
- Tools separadas (`editar_fecha`, `editar_peso`) — descartadas por fragmentación: el modelo tendría que hacer N llamadas para un cambio que conceptualmente es uno.
- Edición round-trip YAML (`serde_yaml::to_string`) — descartada porque reformatea todo el YAML y destruye el formato del usuario (espacios, orden de campos, comentarios). Line-based preserva el formato exactamente.

**Documentos afectados:** `src-tauri/src/filesystem/escritura.rs`, `src-tauri/src/commands/mod.rs`, `src-tauri/src/lib.rs`, `src/adapters/ia/tools.ts`, `src/components/chat/ChatPanel.tsx`, `skill/control-de-mision.md` (§5.3).

**Consultado con Erick:** sí (sesión 2026-05-05, pruebas exitosas).

---

### 2026-05-05 — Fase 5: F-06, config runtime, estados vacíos, errores, onboarding, performance #fase-5

**Decisiones agrupadas de la sesión de Fase 5:**

**F-06 — Memoria de conversación entre sesiones (SQLite):**
- Backend: `tauri-plugin-sql` v2 con SQLite. DB en `%APPDATA%/com.agatha/chat.db`. Dos tablas: `mensajes` (rol, bloques JSON, ts) y `meta` (clave/valor).
- N_INICIAL = 30 mensajes al arranque (hydration). N_MODELO = 25 para inyectar al contexto del modelo (control de costos).
- Bug detectado: `sql:default` solo incluye `allow-close/load/select` — no `allow-execute`. Los INSERTs fallaban silenciosamente. Fix: agregar `sql:allow-execute` a `capabilities/default.json`.
- Saludo de inicio de día: estático contextual (no API call). Se genera con `generarSaludoEstatico(tareas)` que incluye fecha + conteo de tareas para hoy. Se dispara cuando `meta.ultima_actividad != hoyISO()`. Se usa `vaultListo` prop para esperar a que el vault esté cargado antes de generarlo.
- Progressive loading estilo WhatsApp: scroll a tope del `.body` dispara `cargarMas()`. Patrón `scrollRestoreRef` + `useLayoutEffect` para restaurar posición tras prepend (sin saltar). Botón "Cargar mensajes anteriores" como fallback.
- `borrarMemoria`: borra todas las tablas y resetea el estado. Botón de papelera en header del ChatPanel.
- Restauración de foco al textarea: cuando `streaming` pasa de `true` a `false`, el `disabled` del textarea quita el foco automáticamente. Fix: `useEffect([streaming])` con `prevStreamingRef` que detecta la transición y llama `inputRef.current?.focus()`.

**Config runtime (onboarding):**
- `useConfig`: lee de `localStorage('agatha:vault-path')` y `localStorage('agatha:api-key')` con fallback a `import.meta.env.VITE_*`. Los env vars funcionan como valores iniciales del localStorage para Erick en dev.
- Cuando `!config.listo` (alguna variable vacía), muestra `OnboardingScreen` como overlay sobre la app. Mismo fondo canvas, card centrada con avatar Vesper, dos inputs (vault path + API key con toggle mostrar/ocultar), botón Guardar.
- Todos los hooks (`useVault`, `usePromptBase`, `useContextoVault`, `useChat`) ahora reciben `vaultPath`/`apiKey` como parámetros en lugar de leer `import.meta.env` internamente. Permite reconfigruación sin restart.

**Estados vacíos del board:**
- Caso A (columnas vacías): `.colEmpty` con borde punteado y "Sin tareas" — ya existía, solo se ajustó `border-radius` (3px decidido por Erick sobre 10px del mockup).
- Caso B (board vacío): cuando `tareasFiltradas.length === 0`, reemplaza las columnas con estado centrado. Si hay filtro activo: muestra el filtro específico + botones "Limpiar filtros" y "Volver" (retrocede un nivel de filtro). Si no hay filtro: mensaje "El vault no tiene tareas activas" con hint de Agatha.

**Manejo de errores:**
- `clasificarError()` en `useChat.ts` traduce errores del SDK de Anthropic a español: sin conexión, API key inválida, sobrecarga 529, rate limit 429, timeout.
- `traducirErrorVault()` en `useVault.ts` traduce errores Rust de OS a español: OS error 2 (no encontrado), OS error 13 (permisos), OS error 20 (no es directorio).
- Toast variante `tipo: 'error'` en `ToastStack`: fondo `#FFF0F0`, borde `#FECACA`, texto `#991B1B`, ícono triángulo alerta rojo.
- `marcarCompletada` en `App.tsx` ya no silencia errores con `console.error` — genera toast rojo con mensaje descriptivo.

**Performance (arranque en frío):**
- `useContextoVault` recibe `enabled` flag. Por defecto `false` en App.tsx hasta que el chat se abre por primera vez (`setContextoHabilitado(true)` en `abrirChatDrawer`). Elimina 7-8 lecturas de archivos al arranque.
- `performance.now()` en DEV: log `[Agatha] board listo en Xms` cuando `!loading`.
- `React.memo` en `TaskCard` para evitar re-renders cuando cambia estado de drawers/chat.
- Dep stale fix en `marcarCompletada`: `vaultPath` extraído a variable de nivel de componente y correctamente incluido en deps.

**Alternativas consideradas:**
- SQLite vs. archivo JSON local (más simple pero no query-able ni paginable).
- `tauri-plugin-store` vs. `localStorage` para onboarding config — elegido localStorage porque no requiere plugin adicional y el WebView es persistente entre arranques.
- AI greeting vs. estático — elegido estático por latencia cero al arranque; el modelo genera mejores saludos pero requeriría systemPrompt + contexto listos antes de poder saludar.

**Documentos afectados:** `src/hooks/{useChat.ts, useVault.ts, useConfig.ts, useContextoVault.ts, usePromptBase.ts}`, `src/persistencia/chatStore.ts`, `src/components/{chat/ChatPanel.tsx, toast/ToastStack.tsx, onboarding/OnboardingScreen.tsx}`, `src/App.tsx`, `src-tauri/capabilities/default.json`, `CLAUDE.md`.

**Consultado con Erick:** sí (sesión 2026-05-05).

---

### 2026-05-05 — Rediseño del chat: panel persistente → drawer invocable izquierdo #fase-5
**Decisión:** Implementación completa de `propuesta-chat-drawer.md`. El chat pasa de panel lateral fijo (~280px con rail colapsado) a **drawer overlay desde la izquierda (60vw)**, mutuamente excluyente con el TaskDrawer. Punto de entrada: avatar Vesper sólido (`#FF7A2A` + letra A blanca) en el header del board, a la izquierda de los iconos de modo. Atajo global Ctrl+Shift+A toggle. Esc cierra. Click en backdrop cierra. Animación secuencial entre drawers (cierra activo en 240ms, luego abre el nuevo) — la transición cruzada se descartó por confusión visual.

Cambios estructurales del paquete:

1. **Auto-expand del textarea** (paso 1): `useLayoutEffect` que sigue `scrollHeight` del contenido. CSS con `max-height: 200px`, `overflow-y: auto`, scrollbar fino (6px, `--color-border`), `align-items: flex-end` en el wrapper para que el botón send quede abajo cuando el textarea crece.
2. **`useChat` y `usePromptBase` levantados a `App.tsx`** (paso 2). El hilo sobrevive al unmount del drawer dentro de la sesión. **Prerequisito explícito de F-06** (memoria inter-sesión, Fase 5): cuando se implemente la persistencia, se conecta al montaje de `App.tsx` sin refactor estructural.
3. **Layout de App.tsx** (paso 3): de grid 2-paneles a single-panel + 2 overlays. `.app-shell.chat-col-collapsed`, `.chat-col` y la noción de "rail" eliminadas. `chatColapsado` (persistido) reemplazado por `chatAbierto` (sesión, default cerrado).
4. **`ChatDrawer.tsx`** (paso 4): overlay 60vw desde la izquierda, backdrop con `--color-overlay`, `transform: translateX(-100%) → translateX(0)` con transition 220ms. Estado interno `montado` vs `visible` para preservar la animación de salida antes de desmontar. Doble `requestAnimationFrame` al abrir para que React flushee el render con `visible=false` antes de aplicar `visible=true` (sin esto, ambos cambios caen en el mismo paint y la animación de entrada se pierde — bug detectado en validación).
5. **Mutual exclusión animada secuencial** (paso 5): orquestación en `App.tsx`. Si abrís uno y el otro está abierto, primero `setX(false/null)`, después de 240ms `setY(true/...)`. Total ~440ms, coherente con la sensación de "uno cierra, otro abre" sin solapamiento.
6. **Avatar en BoardHeader** (paso 6): wrapper `.headerLeft` con flex + gap 12px agrupando avatar (28×28, Vesper sólido, font-heading, hover `scale(1.08)`) + botón de modo. Click en avatar dispara `abrirChatDrawer` (con mutual exclusión). Sin bolita de estado en este rediseño — pospuesta a iteración futura.
7. **Atajo + a11y** (paso 7): listener global Ctrl+Shift+A en `App.tsx` con toggle. Esc cierra (handler en cada drawer). `role="dialog"` + `aria-modal="true"` + `aria-label="Chat con Agatha"`. Focus al textarea cuando termina la animación de entrada (selector específico, no genérico — el primer focusable era el botón Cerrar y robaba foco). Restore focus al elemento previo cuando cierra.

**Mismo patrón aplicado retroactivamente al TaskDrawer** durante validación: tenía cierre brusco porque `if (!tarea) return null` desmontaba inmediatamente. Migrado a `tareaMostrada` (estado interno retenido 220ms tras prop null) + doble rAF al abrir. Apertura/cierre ahora simétricos en ambos drawers.

**Refinamientos visuales descubiertos en validación (estilo Claude Chat):**
- **Línea separadora arriba del input eliminada.** El footer ahora es `position: absolute; bottom: 0` con gradient `transparent → var(--color-surface) 40%` — el input flota sobre la conversación, los mensajes se desvanecen detrás de él en lugar de cortarse con un borde duro. `pointer-events: none` en el footer y `auto` en sus hijos para que el área del gradient no bloquee el scroll.
- **`padding-bottom: 120px` en `.body`** para que el último mensaje no quede tapado por el input flotante.
- **Sombra sutil al input** (efecto flotar): `0 4px 16px rgba(20,18,14,0.06), 0 1px 3px rgba(20,18,14,0.04)` — dos capas, tono cálido coherente con el hover de tarjetas.
- **Scrollbar custom** en `.body` y `.input`: 6px ancho, thumb `--color-border` (`#e5e1d8`), track transparent, hover `--color-border-subtle` (`#c9c4ba`). Reemplaza al scrollbar default de Windows que era ancho y gris oscuro.

**Fix paralelo del SlashMenu** (deuda de la pieza 4c): al elegir un comando con Tab/Enter/click, el menú no se cerraba (el borrador seguía empezando con `/` y el filtro mostraba la única opción que matcheaba). Fix: `seleccionar()` ahora marca `cerradoManualmente = true`. El flag se resetea automáticamente cuando el borrador deja de empezar con `/`, así reabre la próxima vez que tipees `/`.

**Por qué:**
- Lectura apretada en panel de 280px (listas, headings markdown, cápsulas naranja, código se cortaban). Drawer de 60vw da aire suficiente para respuestas largas.
- Textarea de una sola línea forzaba edición a ciegas. Auto-expand más drawer ancho resuelven el problema completo.
- Cambio de paradigma asumido conscientemente: Agatha pasa a ser asistente que se invoca, no panel persistente. La continuidad emocional se preserva en el avatar del header.
- Levantar `useChat` no era opcional — preserva el hilo intra-sesión y deja preparado el terreno para F-06 sin refactor.
- Animación secuencial (no cruzada) elegida porque la transición simultánea de dos drawers genera la sensación de que ambos coexisten, contradiciendo la lógica de mutual exclusión.

**Alternativas consideradas (todas descartadas en la propuesta o durante implementación):**
- Coexistencia de ambos drawers — colisión de anchos.
- Resize con handle o snaps 55/80% — complejidad sin valor demostrado.
- Ctrl+A — colisiona con "Seleccionar todo" en inputs.
- Avatar blanco con borde y letra Vesper — rompe la continuidad emocional.
- Bolita de estado de Agatha — pospuesta para evitar complejidad acumulada.
- Animación cruzada entre drawers — descartada por confusión visual.
- Persistir `chatAbierto` en localStorage — descartada para reforzar el paradigma "Agatha invocable".

**Notas de implementación:**
- El rail colapsado (60px) y todo el CSS asociado (`.panelColapsado`, `.avatarColapsado`, `.app-shell.chat-col-collapsed`) eliminados sin reemplazo. La key `agatha:chat-colapsado` queda huérfana en localStorage del usuario — no rompe nada.
- ChatPanel cambió de `<aside>` a `<div>` (vive dentro del `<aside role="dialog">` del ChatDrawer; evita anidar dos `<aside>`).
- `ChatPanel.props`: `colapsado`/`onToggle` eliminadas, reemplazadas por `onCerrar`. Recibe `mensajes`/`streaming`/`error`/`enviar`/`promptListo`/`errorPrompt` por props desde App.tsx.
- Box-shadow del drawer (`8px 0 32px rgba(20,18,14,0.12)`) hacia la derecha, espejo del TaskDrawer.

**Validado con Erick:** sí (sesión 2026-05-05, todos los pasos del checklist). Aprobación final: "quedó espectacular".

**Documentos afectados:**
- Frontend: `App.tsx`, `App.css`, `components/chat/{ChatPanel.tsx, ChatPanel.module.css, ChatDrawer.tsx, ChatDrawer.module.css}`, `components/board/{BoardHeader.tsx, BoardHeader.module.css}`, `components/drawer/TaskDrawer.tsx`, `hooks/useSlashCommand.ts`.
- Documentación post-implementación: `guia-visual-agatha.md` (sección de drawers, avatar en header, input flotante), `vision-producto.md §4` (F-01 evolucionado), `etapa-4-paso-2-decisiones-ux.md` (sección "Rediseño del chat post-Fase-4" referenciando esta entrada y la propuesta), `CLAUDE.md`.

**Consultado con Erick:** sí (decisiones cerradas en propuesta el 2026-05-05; implementación validada el 2026-05-05).

### 2026-05-05 — Fase 4b: F-22 sincronización de dependencias + toast naranja + endurecimiento del matcher CardBoard #fase-4
**Decisión:** Implementación de F-22 (skill §5.2 paso 4) con **array `bloqueada_por` inmutable, estado computado** (Opción B). Al completar A, `marcar_completada` corre el cascade `desbloquear_dependientes(vault_path, ruta_completada)`:

1. Localiza candidatas usando `desbloquea` de A como camino primario, con fallback a escaneo del vault buscando tareas que tengan a A en su `bloqueada_por`. Cubre el caso de `desbloquea` mal poblado o ausente.
2. Para cada candidata B con tag `bloqueada`, verifica que **todas** las entradas de su `bloqueada_por` resuelvan a tareas con tag `completada` (la regla literal de skill §5.2 paso 4). Resolución de slugs prefiere "mismo directorio que la dependiente" con fallback global.
3. Si pasa: line-based reescribe tag `bloqueada` → `pendiente` y quita `🔒` de la primera línea de CardBoard. **El array `bloqueada_por` no se toca.**
4. Devuelve `Vec<TareaDesbloqueada>` que viaja al frontend para disparar (a) un toast por desbloqueo según guía visual §6.8, (b) el contenido del `tool_result` para que el modelo mencione los desbloqueos en el chat (cápsula naranja semántica). Doble feedback como decidido en proceso-desarrollo.md (decisión 6 de etapa 4 paso 2).

**Por qué Opción B (array inmutable, no Opción A "eliminar bloqueador resuelto"):**
- **Coherencia con la skill.** §5.2 paso 4 dice literalmente *"Verificá si **todas** sus `bloqueada_por` están ahora `#completada`"* — eso solo funciona si el array se mantiene íntegro. §5.10 (barrido) detecta como inconsistencia el patrón "tag `bloqueada` + todas las entradas del array son `#completada`" y propone reconciliar — solo posible si el array no se modificó.
- **Reversibilidad post-MVP** (etapa-3-paso-4-alcance-mvp.md línea 619): "des-completar A → B vuelve a bloqueada" requiere que el array siga listando A.
- **Histórico legible en Obsidian.** El `.md` es bitácora del trabajo: ver `bloqueada_por: [01-investigar, 02-validar]` cuenta la historia. Vaciarlo al desbloquear pierde esa narrativa.
- **Sin impacto de performance.** El vault entero ya está en memoria (Fase 1, refresh por watcher en Fase 4a). Lookup de 1-3 ids es trivial.

Esta decisión **no es nueva** — es la implementación literal del criterio de aceptación documentado en skill `control-de-mision.md` §5.2 + §5.10 y en `etapa-3-paso-4-alcance-mvp.md` F-22. Si en futuras sesiones se discute, el peso recae en estos documentos.

**Otras decisiones cerradas dentro de F-22:**
- **Cascade de un nivel.** Completar A solo afecta tareas con A en `bloqueada_por`. No transitivo: B no se completa automáticamente, así que C sigue bloqueada por B (esto es semánticamente correcto y evita el spam de toasts).
- **Doble feedback siempre.** Toast (canal visual instantáneo, decae a 4s) + cápsula naranja en chat con el modelo formulando el mensaje (canal semántico, queda en historial). Aplica al checkbox de tarjeta y al tool de Agatha.
- **Un toast por tarea desbloqueada**, apilados verticalmente con gap 8px (§6.8). Auto-dismiss 4s, fade-in 200ms / fade-out 300ms. Ícono Lucide unlock alineado con la naturaleza del feedback.
- **Click en link del toast abre el drawer de la tarea desbloqueada.** Implementado vía ref `tareasRef` en App.tsx para evitar capturar `tareas` stale en el callback.
- **Suprimir watcher para cada B reescrita.** El cascade puede modificar varias tareas en una transacción; cada una llama `watcher::suprimir(path)` antes del rename atómico, así un solo refresh post-recargar() cubre todo.

**Endurecimiento del matcher CardBoard (bug detectado en validación):**
Durante las pruebas con E5 se vio que el `🔒` y el `- [ ]` también se reemplazaban en la sección Detalle cuando el texto mencionaba esos patrones (ej. en inline code descriptivo). Causa: el matcher era `linea.contains("- [ ]")` — demasiado flojo. Fix aplicado en `transformar_a_completada` (escritura.rs, Fase 3) y `transformar_a_pendiente` (dependencias.rs, F-22): ahora exige `linea.trim_start().starts_with("- [")`, descartando menciones precedidas por backticks u otra puntuación. Mejora preventiva sin contraindicaciones — todas las líneas reales de CardBoard empiezan con guión sin prefijo. Aplicado retroactivamente al código de Fase 3 porque es la misma clase de bug.

**Alternativas consideradas:**
- Opción A "eliminar bloqueador resuelto" del array (descartada por las razones de arriba — rompe skill §5.2/§5.10 y reversibilidad).
- Opción C "array inmutable + nota histórica de desbloqueo en Notas" (descartada — añade complejidad sin valor; el `fecha_completado` de la bloqueadora ya provee el dato).
- Cápsula del tool con conteo seco ("Tarea completada. Desbloqueó: 2 tareas") (descartada — incluir títulos en el `tool_result` permite al modelo formular un mensaje natural).
- Toast agregado para múltiples desbloqueos (descartado — la guía §6.8 especifica apilamiento, y un toast por tarea hace que el link abra la específica).

**Notas de implementación:**
- Slugs en frontmatter (`bloqueada_por`/`desbloquea`) son **nombres de archivo sin extensión** (ej. `02-esperar-aprobacion-bruno`), no rutas. La convención observada en el vault es que viven en el mismo directorio que la tarea referenciante (cadenas 01→02→03 dentro de una misión). El resolver prefiere el mismo directorio y tiene fallback global por colisiones raras.
- Si una entrada del `bloqueada_por` referencia un slug inexistente (datos sucios), `todas_bloqueadoras_completadas` retorna `false` para no desbloquear silenciosamente sobre estado inválido. El barrido §5.10 lo reportará.
- Idempotencia: si la tarea recién marcada ya estaba completada (no-op de `marcar_completada`), `desbloquear_dependientes` igual corre y devuelve `[]` salvo que detecte un B en estado inconsistente — alineado con §5.10.

**Validado con Erick:** sí (sesión 2026-05-05, 5 escenarios cubiertos en `enter-tech-school/app-enterbase/prueba-f22/`):
- E1 — Sin `desbloquea`/`bloqueada_por`: completar no dispara toast. ✓
- E2 — Cadena simple A→B: completar A desbloquea B con un toast linkeado. ✓
- E3 — B con dos bloqueadores: completar uno solo no desbloquea, completar el segundo sí. ✓
- E4 — A `desbloquea: [hijo-1, hijo-2]`: completar A dispara dos toasts apilados. ✓
- E5 — B con `🔒` en CardBoard: tras desbloqueo el `🔒` se quita. ✓ (con el bug del matcher detectado y corregido — ver arriba.)

**Documentos afectados:** `src-tauri/src/filesystem/dependencias.rs` (nuevo), `src-tauri/src/filesystem/mod.rs`, `src-tauri/src/commands/mod.rs` (firma de `marcar_completada` ahora devuelve `Vec<TareaDesbloqueada>` y recibe `vault_path`), `src-tauri/src/filesystem/escritura.rs` (endurecimiento del matcher CardBoard), `src/domain/index.ts` (tipo `TareaDesbloqueada`), `src/components/toast/{ToastStack.tsx,ToastStack.module.css}` (nuevos), `src/App.tsx`, `src/components/chat/ChatPanel.tsx`, `src/hooks/useChat.ts`, `src/adapters/ia/tools.ts`.
**Consultado con Erick:** sí (2026-05-05)

### 2026-05-05 — Fase 4a: watcher de filesystem con supresión de escrituras propias #fase-4
**Decisión:** Watcher recursivo del vault con `notify-debouncer-full = "0.3"` (sobre `notify = "6"`), debounce 600ms, en `src-tauri/src/watcher/mod.rs`. Filtra a `.md`, ignora archivos temporales `.<nombre>.tmp` (de la escritura atómica) y paths "suprimidos" — un mapa global `Mutex<HashMap<PathBuf, Instant>>` con TTL 2.5s al que `escribir_atomico` agrega el destino antes de cada escritura. Cuando hay al menos un evento relevante, emite el evento Tauri `vault:changed` (sin payload — el frontend recarga el vault entero). El frontend (`useVault`) llama `iniciar_watcher(vaultPath)` una vez al montar y usa `listen('vault:changed', recargar)` con cleanup. El debouncer vive en un `OnceLock<Mutex<Option<Debouncer>>>` singleton: si se llama `iniciar_watcher` de nuevo (HMR / re-render de App), reemplaza el anterior y el viejo se dropea limpio.

**Por qué:**
- `notify-debouncer-full` y no `notify` crudo: en Windows una sola edición desde Obsidian dispara una ráfaga (Modify(Metadata) + Modify(Data) + Create del temp + Rename) que sin debounce produce 3-4 refresh por save. El debouncer colapsa la ráfaga en un evento.
- Supresión por path con TTL (no flag global "estoy escribiendo"): si dos escrituras propias se solapan no hay race, y una escritura propia no oculta cambios externos en *otros* archivos durante esa ventana. La canonicalización del path antes de comparar evita que `C:\` vs `\\?\C:\` (forma extendida que devuelve `notify` en Windows) cuente como paths distintos.
- Evento sin payload: para 47-100 tareas `leer_vault()` es instantáneo y simplifica el contrato. Si el vault crece a miles, Fase 5 puede pasar a un payload con paths cambiados y refresh diferencial.
- Singleton `OnceLock` y no estado en `tauri::State`: el watcher no necesita acceso desde commands, solo necesita reemplazo idempotente.

**Alternativas consideradas:**
- `notify-debouncer-mini` (descartado: solo da paths, no detalles. Alcanza pero `full` no es más caro y deja la puerta abierta a F-22 si necesita ver tipo de evento — Create/Remove/Modify).
- Flag global "ignorar todos los eventos durante una escritura propia" (descartado: oculta cambios externos en otros archivos, y se rompe si dos escrituras se solapan).
- Refresh diferencial con payload `{ rutas: [...] }` (descartado para MVP: añade complejidad sin beneficio mensurable a esta escala).

**Notas de implementación:**
- El watcher arranca desde el frontend con `invoke('iniciar_watcher', { vaultPath })` — no desde `setup` de Tauri — para que el path lo provea la misma fuente que `useVault` (env `VITE_VAULT_PATH`) y mantengamos una sola fuente de verdad del path.
- `path.canonicalize()` puede fallar (archivo borrado entre eventos): se cae a `path.to_path_buf()` como fallback. La supresión sigue funcionando en >99% de los casos prácticos porque la escritura ocurre antes de que `canonicalize` falle.
- Limpieza oportunista del mapa de supresión: en cada `esta_suprimido` se purga lo vencido, no hace falta thread aparte.

**Validado con Erick:** sí (pruebas en sesión — refresh por edición externa OK, sin doble refresh al crear/marcar completada desde chat, debounce funcional con saves rápidos consecutivos, renombre desde Obsidian dispara un solo refresh).

**Documentos afectados:** `src-tauri/Cargo.toml`, `src-tauri/src/watcher/mod.rs` (nuevo), `src-tauri/src/lib.rs`, `src-tauri/src/commands/mod.rs`, `src-tauri/src/filesystem/escritura.rs`, `src/hooks/useVault.ts`.
**Consultado con Erick:** sí (2026-05-05)

### 2026-05-03 — Fase 3c: marcar completada + F-07 contexto inicial + consultar progreso de misión #fase-3
**Decisión:** Cierre de Fase 3. Tres piezas:

(1) **Marcar tarea como completada.** Comando Tauri `marcar_completada(rutaArchivo)` reescribe el `.md` line-based: reemplaza el tag de estado (`pendiente`/`en-espera`/`bloqueada`) por `completada`, llena `fecha_completado: YYYY-MM-DD` con la fecha local, y reemplaza el primer `- [ ]` del body por `- [x]` (línea CardBoard de §5.7). Idempotente (si ya está completada, no-op). Atómico (temp + fsync + rename). Tool TS `marcar_completada(idTarea)` resuelve el id (ruta relativa) → ruta absoluta y delega al comando. Checkbox de la tarjeta (`TaskCard`) ahora es `<button>` clickable que dispara `onMarcarCompletada` y refresca el board vía `useVault.recargar()`.

(2) **F-07: snapshot inicial del vault como contexto cacheado.** Comando Tauri `leer_contexto(vaultPath)` devuelve los 7 archivos contractuales (§2 del control-de-misión): `README.md`, `context/yo.md`, los 4 mapas estelares, `nebulosa-mental/destellos.md`, `notas.md`. Cada uno es `Option<String>` — los faltantes son `None`, no error. Hook `useContextoVault` los carga al inicio. El adapter ahora arma `system` en **3 capas**: (a) `control-de-mision.md` cacheado, (b) archivos contextuales cacheados (estables por sesión), (c) bloque volátil sin cache. El bloque volátil incluye fecha actual + día + conteos por estado pre-calculados (pendientes/en-espera/bloqueadas) + conteos por fecha (hoy/mañana/atrasadas) + lista compacta de tareas activas con `id|título|estado|peso|fechaTipo|inicio|fin|planeta/misión[/sub]`. Decisión 1A: solo activas en el contexto, no completadas (las completadas crecen sin techo y se consultan bajo demanda). Línea de instrucción explícita "Cuando el usuario pregunte cantidades, usá estos números — no recuentes la lista" para evitar que el modelo aproxime en vez de leer el conteo pre-calculado.

(3) **Tool `consultar_progreso_mision({planeta, mision, subMision?})`.** Backend filtra el vault por planeta/misión y opcionalmente por sub-misión, devuelve conteos por estado + lista de completadas (id, título, fechaCompletado) ordenada de más reciente a más antigua. Pensado para preguntas tipo "¿cómo vamos con la misión X?" — Agatha cruza esa respuesta con las activas que ya tiene en el contexto y arma el balance.

**Por qué:**
- Marcar completada: cierre del loop de modificación del vault. Sin esto, Agatha solo podía crear tareas, no cerrarlas. Reescritura line-based (no YAML round-trip) preserva el formato exacto del frontmatter del usuario.
- F-07: sin contexto del vault, Agatha no podía referirse a tareas reales (alucinaba ids, "no encontraba" tareas existentes, no conocía planetas/misiones). El contrato §2 del control-de-misión define exactamente qué archivos cargar — esos van cacheados (estables por sesión) para que el cache hit cubra ~15-25K tokens en vez de solo el prompt base.
- Bloque volátil con conteos pre-calculados: el modelo tiende a aproximar cuando tiene que contar 47 ítems de una lista. Pre-calcularlos ahorra output (no escribe párrafos aproximando) y garantiza exactitud sin costo significativo (~20 tokens extras en el bloque volátil, que de todos modos no se cachea).
- `consultar_progreso_mision` resuelve la tensión "Agatha necesita ver completadas para responder progreso, pero meterlas todas siempre infla tokens linealmente con la edad del vault". Tool use bajo demanda: cero costo extra por defecto, pago solo cuando el usuario pregunta. Activas ya están en el contexto base, así que el tool solo agrega el delta (completadas).

**Alternativas consideradas:**
- Marcar completada vía YAML round-trip con `serde_yaml` (descartado: pierde formato, comentarios, orden de campos del frontmatter del usuario).
- Incluir últimas N completadas en el contexto volátil siempre (descartado: predecible pero N=20 es muy pocas para misiones grandes y muchas para misiones chicas — el tool da granularidad por misión).
- Resumen agregado por misión en el volátil ("instructor-code101n20: 12 activas, 8 completadas") (descartado: barato pero pierde títulos, no responde "¿qué ya hice?").
- Dos tools separadas para misión y sub-misión (descartado: un solo tool con `subMision` opcional es más limpio y el modelo decide).
- Saludo automático al iniciar sesión con resumen (decisión 2B: pospuesto a Fase 5 — primero validar que el contexto se cargue bien sin saludo automático).

**Notas de implementación:**
- `marcar_completada` en Rust localiza el frontmatter por delimitadores `---`, identifica el bloque `tags:` por indentación de array YAML (`  - `), y reemplaza solo la línea con tag de estado conocido. Si el archivo ya tiene tag `completada`, retorna el contenido sin cambios (idempotencia).
- `consultar_progreso_mision` reusa `leer_vault()` y filtra en memoria — más simple que un walker filtrado y suficientemente rápido para vaults personales (cientos de archivos, no miles).
- Cápsula del nuevo tool: "Consultando progreso de <misión>..." → "Progreso consultado: <misión>". Cuando hay sub-misión se muestra `<misión>/<sub-misión>`.
- Idempotencia y robustez verificadas en validación con Erick: marcar una tarea ya completada no rompe nada, Agatha no aluciña ids cuando no encuentra una tarea (pregunta por más datos en vez de inventar).

**Limitaciones conocidas / a observar en uso real:**
- Si el vault crece a miles de tareas, el bloque volátil con la lista completa de activas puede empezar a ser caro. Por ahora (47 activas) es ~1400 tokens — aceptable. Si crece, considerar paginación o filtrado por planeta.
- `consultar_progreso_mision` devuelve la lista completa de completadas de la misión. En misiones con cientos de completadas la respuesta del tool puede inflarse. Si pasa, agregar parámetro `limite: number` o filtro por rango de fechas.

**Documentos afectados:** `src-tauri/src/filesystem/{escritura.rs,contexto.rs,progreso.rs}` (nuevos: contexto y progreso; escritura amplía con `marcar_completada`), `src-tauri/src/filesystem/mod.rs`, `src-tauri/src/commands/mod.rs`, `src-tauri/src/lib.rs`, `src-tauri/Cargo.toml` (chrono), `src/adapters/ia/{IAProvider,AnthropicProvider,tools}.ts`, `src/hooks/{useChat.ts,useContextoVault.ts}` (nuevo el segundo), `src/components/board/TaskCard.tsx`, `src/components/chat/ChatPanel.tsx`, `src/App.tsx`.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Renombre `deadline` → `vence` + helper centralizado de fechas + fix classifier DateBoard #fase-3 #fase-2
**Decisión:** (1) Sustituir el valor `deadline` por `vence` en el enum de `fecha_tipo` en todo el sistema: skill `control-de-mision.md` §6.5 y la línea 418 del frontmatter de ejemplo, dominio TS (`FechaTipo`), tools del adapter, y tarea existente en `enter-tech-school/app-enterbase/v2-funcionalidades/matricular-estudiantes-antiguos.md`. (2) Centralizar la lógica de fechas en `src/domain/fechas.ts` (`caeEn`, `caeHoy`, `fechaPrincipal`, `formatFechaCorta`, `formatFechaLarga`, `formatRangoLargo`). (3) Fix del classifier de `DateBoard` que solo miraba `fechaInicio`: ahora respeta `fechaTipo` (rango entre inicio-fin, vence con `fechaFin`, exacta/legacy con `fechaInicio`). (4) `TaskCard` muestra badge HOY y fecha relevante según tipo. (5) `TaskDrawer` muestra label adaptativo (`Fecha`/`Vence`/`Rango`) y formato largo legible (`domingo 3 de mayo de 2026`).
**Por qué:** "vence" es más natural en español que "deadline" (decisión de UX/lenguaje del usuario, validada en sesión). El bug del DateBoard era preexistente de Fase 1/2 pero recién se hizo visible al crear tareas tipo `vence` desde el chat — caían silenciosamente en "Sin fecha". Centralizar la lógica evita que cada componente (DateBoard, TaskCard, TaskDrawer) duplique la interpretación de `fechaTipo` y la mantiene consistente. Parseo manual `YYYY-MM-DD` con `parseLocal` para evitar el bug de zona horaria de `new Date(iso)` (Lima UTC-5 mostraría el día anterior).
**Alternativas consideradas:** Mantener `deadline` y solo arreglar el classifier (descartado: prefiere vocabulario en español). Adaptar el classifier sin centralizar (descartado: tres componentes harían lo mismo y divergirían).
**Documentos afectados:** `skill/control-de-mision.md` (vault), `enter-tech-school/app-enterbase/v2-funcionalidades/matricular-estudiantes-antiguos.md` (vault), `src/domain/index.ts`, `src/domain/fechas.ts` (nuevo), `src/components/board/{DateBoard,TaskCard}.tsx`, `src/components/drawer/TaskDrawer.tsx`.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Fase 3b: tool use con `crear_tarea` + cápsulas en chat + contexto volátil #fase-3
**Decisión:** Implementar tool use de Anthropic con loop manual, no tool runner del SDK. El adapter (`AnthropicProvider.streamChat`) emite eventos discriminados (`text_delta | tool_use | tool_result | uso | fin`) que el `useChat` consume para renderizar bloques mixtos en cada mensaje del assistant: texto + cápsulas. Comando Tauri `crear_tarea` con escritura atómica (temp + fsync + rename), UTF-8 sin BOM, sanitización de slugs y segmentos. Tool `crear_tarea` con schema JSON (planeta, misión, sub_misión, nombreArchivo, título, peso, fechaTipo, fechas, detalle, contextoIa). Cápsulas naranja según guía visual §6.6 con tres estados (ejecutando con dots animados, ok con check, error con x). Inyección de fecha actual + día de la semana como segundo bloque de system **sin** `cache_control`, preservando el cache del prompt base (verificado: prompt base de 10141 tokens cachea en read tras el primer turno). Render markdown en burbujas de Agatha con `react-markdown` + `remark-gfm`.
**Por qué:** Loop manual da control para mostrar cápsulas en tiempo real, abortar y manejar errores granularmente — el tool runner del SDK es beta y oculta el flujo. Los eventos discriminados permiten que la UI decida cómo renderizar cada paso (texto inline streaming, cápsula con estado en vivo). El contexto volátil resuelve el bug de fecha alucinada (Agatha decía "vence hoy 2025-07-14" porque no tenía referencia temporal) sin romper el cache del system prompt — el bloque adicional sin `cache_control` se interpreta como continuación del system prompt pero no participa del prefix cacheado.
**Notas de implementación:**
- Renombre `slug` → `nombreArchivo` en el schema de la tool con instrucción explícita "campo técnico, no menciones al usuario al confirmar". Razón: el usuario no maneja el término "slug" y aparecía en las confirmaciones que daba Agatha.
- `crear_tarea` recibe `vault_path` desde `VITE_VAULT_PATH` y refresca el board automáticamente vía `useVault.recargar()` conectado al callback `onTareaCreada`.
- El backend valida planeta/misión/nombreArchivo contra caracteres prohibidos de Windows (`/ \ : * ? " < > |`) y `..`. No valida que existan los planetas/misiones reales — eso queda para F-07 (snapshot del vault) o post-MVP.
- La cápsula muestra "Creando '<título>'..." durante la ejecución y "Tarea creada: '<título>'" al completar; el detalle del error queda en `title` HTML para hover.
**Limitaciones conocidas (post-MVP o Fase 3c):** Agatha no conoce las tareas existentes ni la estructura real del vault (F-07 pendiente). Solo `crear_tarea` está expuesto — `marcar_completada` y `modificar_tarea` quedan para 3c. No hay validación de duplicados semánticos (solo de archivo idéntico).
**Documentos afectados:** `src-tauri/src/filesystem/escritura.rs` (nuevo), `src-tauri/src/commands/mod.rs`, `src-tauri/src/lib.rs`, `src/adapters/ia/{IAProvider,AnthropicProvider,tools}.ts`, `src/hooks/{useChat,useVault}.ts`, `src/components/chat/{ChatPanel.tsx,ChatPanel.module.css}`, `src/App.tsx`. Bitácora abajo cubre la decisión separada de vocabulario `deadline → vence`.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Fase 3a: chat conversacional con streaming + prompt caching #fase-3
**Decisión:** Adapter pattern `IAProvider` + `AnthropicProvider` con SDK oficial `@anthropic-ai/sdk` ejecutándose en frontend (TS) bajo Tauri WebView (`dangerouslyAllowBrowser: true`). Modelo `claude-sonnet-4-6`, `max_tokens: 8192`. Streaming token-by-token vía `messages.stream()`. Prompt base = `skill/control-de-mision.md` del vault, cargado en runtime con `cache_control: ephemeral` sobre el bloque de system.
**Por qué:** Frontend mantiene la simplicidad del adapter en `src/adapters/ia/` alineado con la estructura del brief §5. SDK oficial vs fetch directo: streaming, tipos y prompt caching out of the box, sin tener que implementar SSE manual. Cache verificado en runtime con `usage`: el system prompt de 10141 tokens se cachea en el primer request y se lee a ~0.1× del costo en los siguientes (≈88% reducción de input cost desde el segundo turno).
**Alternativas consideradas:** Backend Rust llamando a la API (más seguro para la API key pero más complejo — descartado para 3a, queda como opción para Fase 5 si la seguridad lo amerita). Fetch directo sin SDK (más liviano, descartado por costo de implementar SSE manual).
**Notas de implementación:**
- Burbujas simétricas siguiendo guía visual §6.7 (Variante A): Agatha con borde + bg blanco, usuario con bg gris cálido `#F4F2ED`. El mockup `01-tarjeta-y-chat.html` muestra Agatha sin borde — guía visual gana como source of truth declarado en CLAUDE.md.
- Indicador "pensando" con 3 dots naranjas pulsando hasta el primer token. Auto-scroll al fondo en cada delta.
- Loguea `usage` en consola en `import.meta.env.DEV` para verificar cache hits durante desarrollo.
- API key vive en `.env.local` como `VITE_ANTHROPIC_API_KEY` (gitignored). Onboarding queda para Fase 5.
**Documentos afectados:** `src/adapters/ia/IAProvider.ts`, `src/adapters/ia/AnthropicProvider.ts`, `src/hooks/usePromptBase.ts`, `src/hooks/useChat.ts`, `src/components/chat/ChatPanel.tsx`, `src/components/chat/ChatPanel.module.css`. `package.json` (+`@anthropic-ai/sdk`).
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Ajuste de colores de peso de tarea (dots) #fase-2
**Decisión:** Peso 1 ("rápida"): `#F2C56B` → `#F4D85A`. Peso 2 ("toma tiempo"): `#B89DD9` → `#E08D9C`.
**Por qué:** En uso real con contenido real, los colores originales causaban confusión visual. El amarillo `#F2C56B` resultaba demasiado similar al naranja del peso 3 (`#E89537`) — poca diferenciación entre "rápida" y "compleja". El púrpura `#B89DD9` del peso 2 se confundía con los chips de misión de enter-tech-school (fondo `#EEEDFE`, texto `#3C3489`). El amarillo más limpio y luminoso `#F4D85A` resuelve la primera confusión; el rosa-coral `#E08D9C` diferencia claramente el peso medio del chip de planeta.
**Alternativas consideradas:** ninguna — correcciones directas por feedback visual.
**Documentos afectados:** `variables.css`, `TaskDrawer.tsx`. Pendiente actualizar `guia-visual-agatha.md` con los valores nuevos cuando Erick confirme.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Fix avatar rail chat colapsado #fase-2
**Decisión:** Avatar del rail colapsado corregido: 28×28px → 22×22px, font-size 13px → 10px. Layout cambiado de `align-items: flex-start; justify-content: center; padding-top: 14px` a `flex-direction: column; align-items: center; padding-top: 17px` (centra el avatar en una zona de ~56px alineada con el header). Agregado `transform: scale(1.08)` en hover del avatar (ya especificado en §9.1 pero no implementado).
**Por qué:** El avatar de 28px usaba el tamaño del header expandido en lugar del tamaño especificado para el rail colapsado (22px). Con 28px en un rail de 32px, quedaban solo 2px de margen a cada lado — visualmente pegado al borde. Con 22px quedan 5px de aire a cada lado, lo que se percibe como centrado.
**Lección:** Distinguir entre las dos versiones del avatar: header expandido (28×28px) y rail colapsado (22×22px). Son contextos distintos con specs distintas. El mockup 04-chat-colapsado.html es el source of truth visual para el rail.
**Documentos afectados:** `ChatPanel.module.css`.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Badge de estado para tareas bloqueadas y en espera #fase-2
**Decisión:** Las tarjetas con estado `bloqueada` o `en-espera` muestran un badge absoluto (top-right, igual posición que HOY) con el ícono correspondiente (candado / reloj de arena). Usa los mismos tokens de color que HOY (`--color-accent-light` fondo, `--color-accent-dark` ícono). El badge HOY no se muestra cuando la tarea tiene uno de estos estados. El titleRow reserva `paddingRight: 36px` cuando cualquier badge es visible.
**Por qué:** Se evaluaron tres alternativas antes de llegar a esta solución: (1) ícono en `metaLeft` — se perdía entre fecha y chip; (2) borde izquierdo de color por estado — introducía demasiados colores nuevos difíciles de memorizar; (3) ícono en `metaRight` junto al botón ↗ — semánticamente incorrecto (estado ≠ acción). El badge absoluto reutiliza el patrón visual ya existente (HOY), no agrega colores nuevos al sistema, y tiene posición clara y consistente.
**Alternativas consideradas:** borde de color izquierdo (revertido — demasiados colores), ícono en metaRight (revertido — confusión semántica acción/estado).
**Documentos afectados:** `TaskCard.tsx`, `TaskCard.module.css`.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Refinamientos visuales menores de tarjetas #fase-2
**Decisión:** (1) Dot de peso: `margin-top: 3px` para alinear ópticamente con la primera línea del título en tarjetas multilínea. (2) Sombra hover reducida: `0 6px 16px rgba(20,18,14,0.08)` → `0 4px 12px rgba(20,18,14,0.06)`. (3) Fix borde superior primera tarjeta: wrapper `.colCards` con `padding-top: 4px` en TagBoard y DateBoard para crear buffer entre el header sticky y la primera tarjeta, evitando que el border-top desaparezca bajo el fondo del header al hacer scroll.
**Por qué:** Ajustes iterativos detectados en uso real. El dot sin margin-top quedaba pegado al borde superior del flex container en vez de centrarse con la primera línea. La sombra original era ligeramente intensa. El header sticky con `background: var(--color-canvas)` tapaba el border-top de la primera tarjeta visible al hacer scroll.
**Alternativas consideradas:** ninguna — correcciones directas por feedback visual.
**Documentos afectados:** `TaskCard.module.css`, `TagBoard.module.css`, `TagBoard.tsx`, `DateBoard.tsx`.
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-03 — Hover de elevación en tarjetas del tablero #fase-2
**Decisión:** Revertir la decisión documentada en `guia-visual-agatha.md §9.1` ("Sin cambio visual en hover"). Las tarjetas activas ahora tienen: `translateY(-2px)` + `box-shadow: 0 6px 16px rgba(20,18,14,0.08)` + `border-color: #DCD7CC` al hover, con easing `cubic-bezier(0.2,0,0,1)` a 180ms. Las tarjetas completadas solo cambian border-color (sin elevación).
**Por qué:** En uso real la tarjeta sin feedback se sentía "muerta" — no comunicaba que era un elemento interactivo. La elevación sutil resuelve esto sin romper la sobriedad del sistema. La excepción para completadas mantiene la coherencia semántica: estado cerrado → menos invitación a interactuar. Tono cálido en la sombra (`rgba(20,18,14)`) en vez de negro puro para mantener coherencia con la paleta.
**Alternativas consideradas:** Solo cambio de border-color (sin elevación) — se evaluó pero el feedback táctil de la elevación se consideró necesario para la interactividad.
**Documentos afectados:** `guia-visual-agatha.md §9.1` — pendiente actualizar reemplazando "Sin cambio visual" por la spec nueva (validación visual pendiente).
**Consultado con Erick:** sí (2026-05-03)

### 2026-05-02 — Refinamiento tipográfico del drawer #fase-2
**Decisión:** (1) Ancho del drawer: 540px → `45vw` (≈615px en pantalla 1366px). (2) H2: 15px → 21px. H3: 13px → 18px. (3) Margen simétrico de bloques de heading: `16px 0 8px` → `20px 0 20px`. (4) Texto de cuerpo (párrafos, listas, citas): 12px → 13px. (5) Código inline, bloques de código, CardBoard: 11px → 12px.
**Por qué:** Validación visual contra Obsidian post-implementación §7. Con el H1 subido a 24px, los H2/H3 quedaron subpercibidos jerárquicamente. El ancho fijo de 540px seguía sintiéndose apretado en pantalla 1366px — `45vw` se adapta al viewport. El margen asimétrico original (16px arriba / 8px abajo) rompía el ritmo vertical. El texto de cuerpo a 12px quedaba pequeño comparado con Obsidian. Lección: los valores de tipografía se calibran con contenido real en pantalla, no en abstracto.
**Alternativas consideradas:** ninguna — ajustes iterativos por feedback visual directo.
**Documentos afectados:** pendiente actualizar `guia-visual-agatha.md` §5.2, §6.9, §7.1 cuando Erick confirme los valores finales.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Limpieza de emojis en H1 del vault #fase-2
**Decisión:** Script PowerShell que removió el emoji prefijo del H1 (ej. `# 📄 Título` → `# Título`) en 81 archivos `.md` no completados del vault. Los archivos con tag `completada` en frontmatter no se tocaron.
**Por qué:** Los emojis en los títulos H1 se veían en el drawer de Agatha. Parcharlo en el renderer (strip en tiempo de render) escalaría mal — con más tareas el problema crece. La solución correcta es limpiar los datos en origen. Las tareas completadas se omitieron porque ya no se visualizan activamente.
**Alternativas consideradas:** Strip de emojis en el componente H1 del renderer (descartado — parche que no escala).
**Documentos afectados:** 81 `.md` del vault en `C:\cerebro\gestiono-mi-vida`.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Cuatro ajustes al drawer post-validación §7 #fase-2
**Decisión:** (1) Ancho del drawer: 460px → 540px. (2) Eliminar header del drawer (pesoBadge + botón ×) y mover Peso a la sección "Información" como propiedad del grid (bolita 11×11 + texto). El H1 del `.md` pasa a ser el título visible — se elimina el `<h1>` standalone y se deja de stripear el primer H1 en `stripBody()`. (3) H1 font-size: 19px → 24px. (4) Scroll único: toda la sección "Información" + body scrollea como una unidad (un solo contenedor `.scrollContent` con `overflow-y: auto`, el `.body` ya no tiene `overflow-y`).
**Por qué:** Validación visual contra Obsidian (benchmark que el usuario ya usa como visualizador rico). Párrafos hacían wrap demasiado pronto (→ ancho). Header duplicaba información ya visible en la sección Información (→ eliminado). H1 subpercibido jerárquicamente vs H2/H3 (→ 24px da presencia clara sin invadir). Sticky de Información innecesario en drawer de lectura ocasional — añadía complejidad sin valor (→ scroll único).
**Alternativas consideradas:** ninguna — correcciones directas post-validación visual.
**Documentos afectados:** pendiente de actualizar `guia-visual-agatha.md` §5.2, §6.9, §7.1, §7.7 si Erick confirma los valores.
**Consultado con Erick:** sí (2026-05-02)
**Lección:** Las specs de la guía visual son punto de partida, pero ancho del drawer y tamaños de tipografía se ajustan recién al ver contenido real. Obsidian sirve como benchmark visual de referencia.

### 2026-05-02 — Color y tamaño de nombres de columna en Tag Board #fase-1
**Decisión:** Nombres de columna (Pendiente, En espera, Bloqueada) en `#111111` a 16px Poppins 500. Completada en `#9A9690` (atenuado — estado terminal).
**Por qué:** El color original `#1A1816` se confundía visualmente con el header carbón `#2A2724`. Negro más neutro `#111111` se percibe más vivo y legible sobre el canvas claro. Completada diferenciada para comunicar que es estado cerrado.
**Alternativas consideradas:** naranja Vesper `#FF7A2A` (descartado — demasiado intenso para un label), colores por estado verde/ámbar/morado (descartado — poco uniformes).
**Documentos afectados:** ninguno.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Vista propia de Agatha en drawer (§7 guía visual) #fase-2
**Decisión:** Reescribir completamente los componentes de react-markdown en el drawer para implementar §7 de `guia-visual-agatha.md`: headings con contenedor naranja + tag de nivel (H1/H2/H3), listas con bullet • naranja via `::before`, citas en gris sutil, bloques de código en fondo carbón `#2A2724`, línea CardBoard en gris cálido `#F4F2ED`, sección "Información" con grid label/valor (estado en tag monospace, planeta en chip, fecha con highlight si es hoy), nota al pie §7.8.
**Por qué:** La primera implementación usó `react-markdown` para parsear pero aplicó estilos CSS planos en lugar de los componentes visuales propios de Agatha. Lección: `react-markdown` + `remark-gfm` define cómo se parsea el markdown — la vista propia de Agatha requiere componentes customizados para CADA elemento (heading, list, code, etc.) que apliquen §7 de la guía visual. Parseo ≠ renderizado.
**Alternativas consideradas:** ninguna — reimplementación directa de spec existente.
**Documentos afectados:** ninguno.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Tarjeta fantasma y border-radius de tarjetas #fase-2
**Decisión:** (1) Estado vacío de columna reemplazado por tarjeta fantasma con borde punteado `#C9C4BA`, fondo transparente, `border-radius: 10px`, texto "sin tareas" en cursiva. (2) `border-radius` de tarjetas hardcodeado a `10px` explícitamente.
**Por qué:** (1) El texto plano "Sin tareas" flotaba sin contexto visual — la tarjeta fantasma mantiene la estructura de la columna y comunica vacío con el lenguaje visual correcto (misma forma que tarjeta real, borde punteado = placeholder). (2) El CSS variable `--radius-card: 10px` estaba correctamente definido pero se desvió visualmente. Lección: antes de asignar valores visuales (padding, border-radius, colores), consultar primero `guia-visual-agatha.md §4` y `etapa-4-paso-2-decisiones-ux.md` — las specs ya están documentadas.
**Alternativas consideradas:** ninguna — correcciones directas de specs existentes.
**Documentos afectados:** ninguno.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Espaciado simétrico de la barra de filtros #fase-2
**Decisión:** `padding-top: 14px` en la barra de filtros (además del `padding-bottom: 14px` ya existente).
**Por qué:** Sin top padding, los chips quedaban "colgados" del header oscuro con menos aire arriba que abajo. El balance visual requiere la misma separación en ambos lados (~14px). Lección general: en zonas entre un header fijo y contenido scrolleable, siempre verificar que el padding sea simétrico verticalmente.
**Alternativas consideradas:** ninguna — corrección directa de spec documentada.
**Documentos afectados:** ninguno.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Librería de markdown rendering: react-markdown + remark-gfm #fase-2
**Decisión:** `react-markdown` v10 con plugin `remark-gfm` para renderizar el cuerpo del `.md` en el drawer.
**Por qué:** Integración natural con React, buen soporte TypeScript, componentes de renderizado customizables para aplicar el sistema visual de Agatha. `remark-gfm` agrega tablas, listas de tareas y strikethrough que el vault usa. Bundle ~50KB gzipped — aceptable.
**Alternativas consideradas:** `marked` (más ligero pero sin integración React nativa), `markdown-it` (más extensible pero más pesado), parsing manual (descartado por complejidad innecesaria).
**Documentos afectados:** ninguno. Resuelve pregunta abierta §10.1 del brief.
**Consultado con Erick:** no

### 2026-05-02 — Reversión scroll único → scroll por columna con stickies #fase-1
**Decisión:** Revertir scroll único del tablero y volver a scroll por columna. Agregar sticky real: cada `.col` es el scroll container, `.colHeader` usa `position: sticky; top: 0` dentro de su propio `.col`.
**Por qué:** El scroll único ("todo se mueve de golpe") resultó más disruptivo visualmente que el problema original. El patrón correcto siempre fue scroll por columna — lo que faltaba en la primera versión eran los stickies bien implementados. Lección: antes de cambiar el patrón macro, revisar si los detalles de ejecución están bien.
**Alternativas consideradas:** scroll único (descartado por Erick después de probar — "afecta la vista").
**Documentos afectados:** `guia-visual-agatha.md` §9.5, `etapa-4-paso-2-decisiones-ux.md` (sección añadida Fase 1). Mockup de referencia: `08-scroll-por-columna-stickies.html`.
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-02 — Correcciones visuales post-revisión inicial #fase-1
**Decisión:** Aplicar 4 correcciones detectadas por Erick en la primera versión del tablero: scroll único con headers sticky, ícono kanban en modo Tag, hourglass en columna En espera, eliminar emojis ⏳/🔒 de tarjetas en Tag Board.
**Por qué:** (1) Scroll por columna fragmenta atención → scroll único del tablero. (2) Ícono etiqueta incorrecto → ícono kanban documentado en UX decisions. (3) Reloj de pared incorrecto → hourglass (Lucide) ya definido en etapa-4. (4) Emojis redundantes en Tag Board + rompen coherencia visual → sin íconos en Tag Board, se usarán Lucide en Date Board (Fase 2).
**Alternativas consideradas:** ninguna — correcciones directas contra decisiones ya documentadas.
**Documentos afectados:** `guia-visual-agatha.md` §9.5 (actualizada por Erick), `etapa-4-paso-2-decisiones-ux.md` (sección añadida Fase 1).
**Consultado con Erick:** sí (2026-05-02)

### 2026-05-01 — Vault y app en carpetas separadas #fase-0
**Decisión:** Mantener `C:\cerebro\agatha-code` (app) y `C:\cerebro\gestiono-mi-vida` (vault) como directorios independientes. Path del vault en `.env.local` para dev, onboarding de Fase 5 para producción.
**Por qué:** El vault es datos del usuario, la app es software. Juntarlos contaminaría el git de la app con tareas personales, rompería el índice de Obsidian con archivos de código, y crearía acoplamiento innecesario. Misma lógica que una app y su base de datos.
**Alternativas consideradas:** vault dentro del repo (descartado — git/Obsidian contaminados), app dentro del vault (descartado — peor).
**Documentos afectados:** ninguno.
**Consultado con Erick:** sí (2026-05-01)

### 2026-05-01 — Scaffolding manual en vez de create-tauri-app #fase-0
**Decisión:** Crear todos los archivos del proyecto manualmente en vez de usar `npm create tauri-app@latest`.
**Por qué:** `create-tauri-app` requiere TTY real y falla con "not a terminal" en el entorno de Claude Code. El scaffolding manual da control total sobre cada archivo y es equivalente en resultado.
**Alternativas consideradas:** `create-tauri-app` (falló por TTY), `npm create vite` + `tauri init` (mismo problema de TTY).
**Documentos afectados:** ninguno.
**Consultado con Erick:** no

### 2026-05-01 — PATH de Rust no disponible en terminales existentes #fase-0
**Decisión:** Documentar que tras instalar Rust con winget, las terminales abiertas antes de la instalación necesitan cerrarse y reabrirse para que `cargo` esté en PATH.
**Por qué:** winget actualiza el PATH del sistema en el registro, pero las sesiones de terminal activas no recargan el PATH automáticamente. `npm run tauri dev` falla con "program not found" si cargo no está en PATH.
**Alternativas consideradas:** `$env:PATH = ...` manual en cada sesión (funciona pero es tedioso).
**Documentos afectados:** ninguno.
**Consultado con Erick:** no

### 2026-05-01 — Instalación mínima de MSVC para Rust/Tauri #fase-0
**Decisión:** Instalar solo `VC.Tools.x86.x64` + `Windows11SDK.26100` en vez del workload completo `NativeDesktop --includeRecommended`.
**Por qué:** Rust y Tauri solo requieren el linker MSVC (`link.exe`) y los headers del Windows SDK. CMake, Clang y las herramientas de diagnóstico de C++ que trae el workload recomendado no tienen uso en este proyecto.
**Alternativas consideradas:** `--includeRecommended` (~5-8 GB); descartado por peso innecesario.
**Documentos afectados:** ninguno.
**Consultado con Erick:** sí (2026-05-01)

---

## Índice de decisiones mayores

> Lista curada manualmente por Claude Code. Solo decisiones de impacto arquitectónico o que Erick podría querer reabrir en el futuro. No es un índice exhaustivo de todas las entradas.

_(vacío — se llenará a medida que aparezcan decisiones mayores)_

---

## Plantilla rápida (copiar y pegar)

```markdown
### 2026-MM-DD — Título #fase-X
**Decisión:**
**Por qué:**
**Alternativas consideradas:**
**Documentos afectados:**
**Consultado con Erick:** no
```
