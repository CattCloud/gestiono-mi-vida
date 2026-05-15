p---
título: Bloques de mejora — Plan iterativo de Agatha
proyecto: Agatha
fecha_creacion: 2026-05-07
estado: documento vivo
mantenedor: skill `planificador-mejoras`
---

# Bloques de mejora — Plan iterativo de Agatha

> **Audiencia.** Vos, Erick, cuando te sentás a trabajar 1-2h en Agatha y necesitás saber qué hacer sin tener que decidirlo desde cero.
>
> **Regla fundacional.** Agatha **ya es útil**. Cada bloque la mejora; ninguno la termina. Si abrís este doc y sentís presión por terminar todo, eso no es información sobre Agatha — es información sobre los 3 Bosses (ver `context/yo.md`). Cerralos volviendo a este recordatorio.

---

## Cómo usar este documento

1. Abrí el doc al sentarte. No revises todo — solo la primera iteración con bloques pendientes.
2. Elegí el primer bloque pendiente que **no tenga dependencias bloqueadas**. Si tenés varios elegibles, elegí el de más impacto. Si están empatados, elegí cualquiera — no rumies.
3. Trabajalo dentro del tiempo estimado. Si excedés en >50%, parálo y registralo: probablemente el bloque estaba mal-dimensionado.
4. Marcá el bloque completado, agregá fecha real y commit hash si aplica. Si querés, anotá tiempo real.
5. Si en el medio se te ocurren ideas nuevas, capturalas en `notas.md` y volvé al bloque actual. Después invocá la skill `planificador-mejoras` para que las integre al plan.

---

## Estado actual

- **Completados:** 5
- **En curso:** 0
- **Pendientes:** 30
- **Obsoletos:** 3
- **Backlog futuro:** 9

Última actualización: 2026-05-09.

---

## Iteraciones

> Cada iteración agrupa bloques relacionados temáticamente. Dentro de una iteración el orden es flexible (vos elegís), salvo cuando un bloque tiene dependencia explícita.

### Iteración 1 — Cierre UX post-V1 (completada 2026-05-07)

#### B01 — Color del peso en chat

- **Tiempo:** ~30 min  ·  **Categoría:** UX  ·  **Impacto:** alto
- **Estado:** completado (2026-05-07)
- **Listo cuando:** los emojis 🟡🟣🟠 en burbujas del chat se renderizan como dots con los colores del design system (no con su color Unicode nativo).
- **Origen:** `notas.md` § Ideas de mejora #2

Tareas:
- [x] Helper `procesarTexto` en `ChatPanel.tsx`
- [x] Custom components `p`, `strong`, `em`, `li` para ReactMarkdown
- [x] Clase CSS `pesoDotChat`
- [x] Extender cobertura a `td`, `th`, `h1`-`h4`, `blockquote` (post-validación 2026-05-07: las tablas mostraban 🟣 nativo lila)

#### B02 — Fechas DD-MM-YYYY en chat

- **Tiempo:** ~30 min  ·  **Categoría:** UX  ·  **Impacto:** medio
- **Estado:** completado (2026-05-07)
- **Listo cuando:** las fechas ISO en respuestas de Agatha se reformatean a DD-MM-YYYY solo en presentación; vault y código siguen usando ISO.
- **Origen:** `notas.md` § Ideas de mejora #3

Tareas:
- [x] Regex `\b(\d{4})-(\d{2})-(\d{2})\b` → `$3-$2-$1` en `procesarTexto`
- [x] Aplicado solo en nodos de texto markdown (code blocks intactos)

#### B03 — Botón editar en drawer

- **Tiempo:** ~45 min  ·  **Categoría:** UX  ·  **Impacto:** medio
- **Estado:** completado (2026-05-07)
- **Listo cuando:** abrir cualquier tarea desde el tablero muestra un botón "Editar en Agatha" en el footer; al click cierra el drawer, abre el chat y pre-llena el borrador con `Editá la tarea "[titulo]": `.
- **Origen:** `notas.md` § Ideas de mejora #5

Tareas:
- [x] Prop `onEditar` en `TaskDrawer`
- [x] Botón con icono lápiz + estilo `editarBtn`
- [x] Callback `editarTareaEnChat` en `App.tsx` (re-usa `abrirChatDrawer` para mutual exclusión)

---

### Iteración 2 — Verificaciones rápidas (deuda)

> Estas son baratas y descubren regresiones del MVP que pueden estar latentes. Hacelas primero — si rompieron algo, mejor saberlo ahora.

#### B04 — Verificar mecanismo "borrar memoria" con confirmación destructiva

- **Tiempo:** ~30 min  ·  **Categoría:** deuda  ·  **Impacto:** alto
- **Estado:** pendiente
- **Listo cuando:** el botón "borrar memoria" requiere doble confirmación (modal o equivalente) antes de ejecutar `DELETE FROM mensajes`. Si no la requiere, agregarla.
- **Origen:** `roadmap-post-mvp.md` § Refinamientos — Mecanismo de borrar memoria con confirmación destructiva

Tareas:
- [ ] Probar flujo actual: ¿hay confirmación visible?
- [ ] Si no, diseñar modal mínimo (texto: "Vas a borrar el historial completo. Es irreversible.")
- [ ] Implementar y probar

#### B05 — Verificar persistencia del filtro post-rediseño Fase 5

- **Tiempo:** ~30 min  ·  **Categoría:** deuda  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** confirmado que `localStorage:agatha:filtros` sobrevive al cierre/apertura de la app y al rediseño del chat. Si no, fixearlo.
- **Origen:** `roadmap-post-mvp.md` § Refinamientos — Persistencia del estado del filtro entre cierres

Tareas:
- [ ] Aplicar filtro, cerrar app, reabrir, verificar
- [ ] Hacer lo mismo abriendo y cerrando el chat varias veces
- [ ] Si falla, revisar el hook `useLocalStorage` en `App.tsx`

#### B06 — Auditar matcher CardBoard en otras zonas del código

- **Tiempo:** ~1h  ·  **Categoría:** deuda  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** todas las zonas que parsean líneas CardBoard (`vault.rs`, `escritura.rs`, `dependencias.rs`) usan el matcher endurecido `linea.trim_start().starts_with("- [")` y no `linea.contains("- [ ]")`.
- **Origen:** `roadmap-post-mvp.md` § Refinamientos — Endurecimiento del matcher CardBoard

Tareas:
- [ ] Grep `contains("- [")` en `src-tauri/src/`
- [ ] Listar zonas afectadas
- [ ] Reemplazar y validar con un .md que tenga `- [ ]` en código inline

#### B38 — Verificar prompt caching en producción (costos reales)

- **Tiempo:** ~1h  ·  **Categoría:** deuda  ·  **Impacto:** alto
- **Estado:** pendiente
- **Listo cuando:** confirmado con datos del logger de costos que las 3 capas del system prompt están cacheando como se diseñó:
  1. `control-de-mision.md` cacheado (estable durante toda la sesión).
  2. Contexto del vault cacheado (estable hasta cambio de archivos contextuales).
  3. Bloque volátil sin `cache_control` (no invalida los anteriores).
  Las interacciones recurrentes del mismo día deberían mostrar `cache_read_input_tokens` alto y `cache_creation_input_tokens` bajo. Si el ratio no es ~9:1 o mejor en una sesión típica, hay algo mal cacheado.
- **Origen:** observación post-migración Haiku 4.5 — el costo bajó de $0.09 a $0.01 por interacción, pero falta confirmar que el cache se mantiene a lo largo de sesiones largas, no solo en interacciones aisladas.

Tareas:
- [ ] Abrir el logger de costos durante una sesión real de 5+ mensajes con Agatha
- [ ] Revisar el campo `cache_read_input_tokens` vs `cache_creation_input_tokens` en cada llamada
- [ ] Verificar que el bloque volátil NO lleva `cache_control` (sería el bug más probable — invalida las capas anteriores)
- [ ] Si los ratios no cuadran, ajustar el ordering de los bloques o el `cache_control` y re-validar

---

### Iteración 3 — Quick wins UX visibles

> Bajo costo, alta visibilidad. Cada uno tiene retorno emocional inmediato — perfecto para sesiones cortas o cuando estás bajo de energía.

#### B07 — F-12 Mensajes celebratorios al completar desde UI

- **Tiempo:** ~1h  ·  **Categoría:** UX  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** al completar una tarea con clic en el tablero, aparece un toast suave con un mensaje cálido ("Hecho. Vas avanzando.", "Una menos.", etc.) elegido aleatoriamente de un set definido. Tono: nunca exigente. Lectura skill §3.
- **Origen:** `roadmap-post-mvp.md` § F-12

Tareas:
- [ ] Definir set de 6-8 frases cortas validadas por Erick
- [ ] Disparar toast en `marcarCompletada` (App.tsx)
- [ ] Variante visual: distinguir del toast de error (verde suave vs gris cálido)

#### B08 — Bolita de estado en avatar de Agatha

- **Tiempo:** ~1h  ·  **Categoría:** UX  ·  **Impacto:** bajo
- **Estado:** pendiente
- **Listo cuando:** durante streaming o ejecución de tools, el avatar de Agatha (en BoardHeader y ChatPanel) muestra una bolita pulsante. Reposo: sin bolita.
- **Origen:** `roadmap-post-mvp.md` § Decisiones técnicas postergadas — Bolita de estado en avatar

Tareas:
- [ ] CSS de la bolita (8px, esquina inferior-derecha del avatar)
- [ ] Conectar al estado `streaming` o `chat.tools` activo
- [ ] Animación pulse 1.2s

#### B09 — F-33 Slash command `/consistencia`

- **Tiempo:** ~1h  ·  **Categoría:** feature  ·  **Impacto:** bajo
- **Estado:** pendiente
- **Listo cuando:** escribir `/consistencia` en el chat dispara el barrido §5.10 manualmente sin cerrar la app.
- **Origen:** `roadmap-post-mvp.md` § F-33

Tareas:
- [ ] Agregar comando al catálogo en `adapters/chat/comandos.ts`
- [ ] Reusar la función de barrido existente
- [ ] Renderizar resultado en cápsula gris

---

### Iteración 4 — Tareas vencidas (notas item #8 + F-21)

> El item de notas.md "Que hacer con las tareas vencidas?" se cruza con F-21 del roadmap. Combinados acá. Diseño primero porque hay decisiones de tono que afectan la implementación.

#### B10 — Diseño columna "Vencidas" + reglas de tono sin culpa

- **Tiempo:** ~1h  ·  **Categoría:** design  ·  **Impacto:** alto
- **Estado:** obsoleto (2026-05-07)
- **Razón:** Decisión tomada directamente en `notas.md` § Ideas #7 (2026-05-07): las vencidas no tendrán columna propia sino badge "VENCIDA" en HOY. Reemplazado por B36 y B37.
- **Origen original:** `notas.md` § Ideas de mejora #8 + `roadmap-post-mvp.md` § F-21

#### B11 — Implementación columna Vencidas en DateBoard

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** alto
- **Estado:** obsoleto (2026-05-07)
- **Razón:** Cambio de diseño en `notas.md` § Ideas #7 (2026-05-07): no hay columna Vencidas separada. Reemplazado por B37 (badge VENCIDA en HOY).
- **Origen original:** `notas.md` § Ideas de mejora #8

#### B12 — F-21 Indicador visual de vencidas en tarjeta

- **Tiempo:** ~1h  ·  **Categoría:** UX  ·  **Impacto:** alto
- **Estado:** obsoleto (2026-05-07)
- **Razón:** Refactorizado al diseño de `notas.md` § Ideas #7 (2026-05-07): el indicador toma forma específica de badge VENCIDA que reemplaza HOY. Reemplazado por B37 con scope concreto.
- **Origen original:** `roadmap-post-mvp.md` § F-21

#### B36 — Renombrar columna "Mañana" a "Futuro" con orden cronológico

- **Tiempo:** ~1h  ·  **Categoría:** feature  ·  **Impacto:** alto
- **Estado:** completado (2026-05-08)
- **Listo cuando:** la columna actualmente llamada "Mañana" en DateBoard se renombra a "Futuro" y muestra todas las tareas con fecha posterior a hoy (mañana, pasado mañana, etc.) ordenadas por fecha ascendente — las más cercanas arriba.
- **Origen:** `notas.md` § Ideas de mejora #7

Tareas:
- [x] Cambiar título de la columna en `DateBoard.tsx`
- [x] Ampliar lógica de partición: "Futuro" recibe todas las fechas > hoy (no solo mañana)
- [x] Ordenar por fecha ascendente
- [x] Validar con tareas reales del vault

#### B37 — Badge VENCIDA en columna HOY (reemplaza badge HOY)

- **Tiempo:** ~1h  ·  **Categoría:** UX  ·  **Impacto:** alto
- **Estado:** completado (2026-05-08)
- **Listo cuando:** las tareas con fecha anterior a hoy aparecen en la columna HOY mostrando un badge "VENCIDA" en lugar del badge "HOY". Tono respeta skill §3 (sin culpa, no rojo alarma — preferible naranja oscuro o gris reflexivo). Si la tarea está `bloqueada` o `en-espera`, el badge de estado prevalece sobre VENCIDA (igual que prevalece sobre HOY hoy).
- **Origen:** `notas.md` § Ideas de mejora #7 (cubre intent original de F-21)

Tareas:
- [x] Decidir color exacto del badge VENCIDA (validar con `guia-visual-agatha.md`)
- [x] Lógica en `TaskCard.tsx`: si `fecha < hoy` y no completada y no bloqueada/en-espera → badge VENCIDA
- [x] Validar visualmente con tareas reales

---

### Iteración 5 — Tarjeta con visualización rica

> El drawer se abre demasiado seguido para entender de qué va una tarea. Si la tarjeta mostrara más, abriríamos menos.

#### B13 — F-19 Diseño preview rico de tarjeta

- **Tiempo:** ~1h  ·  **Categoría:** design  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** mockup decidido. Variables: ¿primer párrafo del Detalle?, ¿links?, ¿tags adicionales?, ¿peso en línea como hoy o reorganizado?
- **Origen:** `roadmap-post-mvp.md` § F-19

Tareas:
- [ ] Hacer 2-3 variantes en mockup
- [ ] Decidir altura máxima de la tarjeta para no romper el tablero
- [ ] Validar con tareas reales (las que más abrís hoy)

#### B14 — F-19 Implementación tarjeta con preview

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** medio  ·  **Depende de:** B13
- **Estado:** pendiente
- **Listo cuando:** las tarjetas muestran el preview decidido en B13. Performance OK con 50+ tareas. Se sigue pudiendo marcar completada y abrir drawer.
- **Origen:** `roadmap-post-mvp.md` § F-19

Tareas:
- [ ] Modificar `TaskCard.tsx`
- [ ] Cargar el body del .md en `useVault` o lazy-on-hover (decidir)
- [ ] Validar el rendimiento

---

### Iteración 6 — Vista Kanban con DnD (F-18)

> El DnD NO va en TagBoard ni en DateBoard — esos se mantienen intactos. Va en una **Vista Kanban nueva** (3er board). Decisión tomada 2026-05-09 basada en `notas.md` § Ideas #3. El Kanban necesita el estado `#en-progreso` (B19) antes de arrancar — hacer B19 primero.

#### B15 — F-18 diseño técnico: Vista Kanban + library DnD

- **Tiempo:** ~1h  ·  **Categoría:** design  ·  **Impacto:** alto  ·  **Depende de:** B19
- **Estado:** pendiente
- **Listo cuando:** decidido el layout del Kanban (4 columnas: Por hacer / En Progreso / Se pospone / Completado), library elegida (`dnd-kit` validado en peso y mantenimiento), patrón click vs drag definido (mousedown + threshold 5px), feedback visual diseñado, selector de 3 vistas en BoardHeader diseñado.
- **Origen:** `roadmap-post-mvp.md` § F-18 + `notas.md` § Ideas #3

Tareas:
- [ ] Confirmar `dnd-kit` (bundle < 50KB gzipped, accesibilidad, mantenimiento)
- [ ] Diseñar las 4 columnas del Kanban y su mapeo a estados del dominio
- [ ] Definir patrón click-corto (abre drawer) vs drag (mueve tarjeta) con `activationConstraint: { distance: 5 }`
- [ ] Diseñar feedback visual: tarjeta en drag opacidad 0.5, columna hover borde naranja Vesper
- [ ] Diseñar selector de 3 íconos en BoardHeader (Tag | Date | Kanban) reemplazando el toggle actual
- [ ] Validar diseño con Erick

#### B16 — F-18 fase 1: componente KanbanBoard + setup dnd-kit

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B15, B19, B25
- **Estado:** pendiente
- **Listo cuando:** existe `<KanbanBoard>` con las 4 columnas, se puede arrastrar una tarjeta entre columnas con feedback visual, NO se rompe el click-abre-drawer, las tareas `bloqueada` no aparecen. Sin persistencia al backend todavía.
- **Origen:** `roadmap-post-mvp.md` § F-18

Tareas:
- [ ] Instalar `dnd-kit` (`@dnd-kit/core`, `@dnd-kit/sortable`)
- [ ] Crear `src/components/board/KanbanBoard.tsx` + `KanbanBoard.module.css`
- [ ] Reutilizar `<TaskCard>` existente (sin modificarlo)
- [ ] Filtrar tareas: excluir `bloqueada`
- [ ] Setup `DndContext`, `useDroppable` por columna, `useDraggable` por tarjeta
- [ ] Feedback visual durante drag (CSS + estado React)

#### B17 — F-18 fase 2: lógica de drop → persistencia backend

- **Tiempo:** ~1.5h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B16, B20
- **Estado:** pendiente
- **Listo cuando:** arrastrar y soltar en el Kanban persiste el cambio en el .md y el board se recarga. Mapeo de columnas: "Por hacer" → `cambiar_estado(pendiente)`, "En Progreso" → `cambiar_estado(en-progreso)`, "Se pospone" → `cambiar_estado(en-espera)`, "Completado" → `marcar_completada` (con cascade existente). Drop en misma columna es no-op. TagBoard y DateBoard no se tocan.
- **Origen:** `roadmap-post-mvp.md` § F-18

Tareas:
- [ ] `onDragEnd`: detectar columna destino e invocar backend correspondiente
- [ ] Llamar `recargar()` tras invoke (igual que al marcar completada)
- [ ] `marcar_completada` desde Kanban activa el cascade de dependencias existente
- [ ] Toast silencioso de confirmación (opcional, a decidir en implementación)

#### B18 — F-18 validación + ajustes en uso real

- **Tiempo:** ~1h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B17
- **Estado:** pendiente
- **Listo cuando:** Erick usó el Kanban durante una sesión de trabajo real y reportó qué falla, qué falta. Ajustes aplicados. TagBoard y DateBoard verificados sin regresiones.
- **Origen:** loop de uso real

Tareas:
- [ ] Sesión de uso real (mover ~20 tareas, mezclar con clic-abrir-drawer)
- [ ] Verificar cascade de dependencias al completar desde Kanban
- [ ] Anotar fricciones y aplicar fixes

---

### Iteración 7 — Estado "En progreso" (prerequisito del Kanban)

> B19-B21 son **prerequisito de la Iteración 6 (Kanban)**. Sin `#en-progreso` en el dominio, el Kanban no puede tener la columna "En Progreso". Hacer esta iteración antes de arrancar B15. El campo `avance` es secundario — se prioriza el tag y el backend primero.

#### B19 — Diseño tag `#en-progreso` + color de badge

- **Tiempo:** ~45 min  ·  **Categoría:** design  ·  **Impacto:** alto
- **Estado:** pendiente
- **Listo cuando:** decidido el tag en el .md (`- en-progreso`, igual que los demás estados), color del badge en `TaskCard` (distinto de naranja/terracota/espera — ¿verde suave? ¿azul?), reglas básicas para el barrido §5.10. El campo `avance` queda como decisión postergada (se agrega en B21 si aplica).
- **Origen:** `notas.md` § Ideas de mejora #4 + decisión de sesión 2026-05-09 (prerequisito Kanban)

Tareas:
- [ ] Decidir color del badge `en-progreso` y validar con Erick
- [ ] Definir reglas mínimas para barrido §5.10 (¿avisar si lleva más de N días en-progreso sin avance?)
- [ ] Actualizar `control-de-mision.md` skill con el nuevo estado
- [ ] Decidir si `avance` va en esta iteración o se pospone a B21

#### B20 — Backend `en-progreso` + comando `cambiar_estado`

- **Tiempo:** ~1.5h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B19
- **Estado:** pendiente
- **Listo cuando:** `vault.rs` parsea el tag `en-progreso`, `src/domain/index.ts` incluye `'en-progreso'` en `Estado`, y existe el comando Tauri `cambiar_estado(ruta, estado)` que cambia entre `pendiente | en-progreso | en-espera` de forma line-based, atómica, idempotente. (El campo `avance` es opcional — implementar solo si B19 lo decide.) Tool opcional en `adapters/ia/tools.ts` para que Agatha pueda cambiar estado via chat.
- **Origen:** `notas.md` § Ideas de mejora #4 + plan Kanban (B17 lo necesita)

Tareas:
- [ ] Extender `Estado` en `src/domain/index.ts` y `vault.rs`
- [ ] Nueva función `cambiar_estado` en `escritura.rs` (patrón de `marcar_completada`: line-based, BOM-safe, watcher::suprimir, rename atómico)
- [ ] Exponer como Tauri command en `commands/mod.rs`
- [ ] Si B19 decide incluir `avance`: extender `Tarea` con `avance: Option<String>` y ampliar `editar_tarea`
- [ ] Tool en `adapters/ia/tools.ts` (opcional)

#### B21 — UI badge `en-progreso` en TaskCard + columna en TagBoard

- **Tiempo:** ~1h  ·  **Categoría:** UX  ·  **Impacto:** alto  ·  **Depende de:** B20
- **Estado:** pendiente
- **Listo cuando:** las tarjetas en-progreso muestran el badge con el color definido en B19. El TagBoard agrega una columna "En Progreso" (entre Pendiente y En Espera) para consistencia con el Kanban. Si B19 decidió incluir `avance`, el drawer muestra el último avance.
- **Origen:** `notas.md` § Ideas de mejora #4

Tareas:
- [ ] Badge en `TaskCard.tsx` con color del token decidido en B19
- [ ] Columna `en-progreso` en `TagBoard.tsx` (entre Pendiente y En Espera)
- [ ] Si aplica: sección `avance` en `TaskDrawer.tsx`
- [ ] Validar visualmente en TagBoard y Kanban

---

### Iteración 8 — Sincronización inversa + export

#### B22 — Sincronización inversa F-22 (descompletar re-bloquea)

- **Tiempo:** ~1h  ·  **Categoría:** deuda  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** descompletar una tarea A re-bloquea automáticamente a las B que estaban bloqueadas por A. Reportado con cápsula gris en chat.
- **Origen:** `roadmap-post-mvp.md` § Sincronización inversa de F-22

Tareas:
- [ ] Función `recompletar` complemento de `marcar_completada`
- [ ] Lógica de barrido reverso en `dependencias.rs`
- [ ] UI: ¿cómo se descompleta? (¿botón en drawer, comando chat?)

#### B23 — Export conversación a markdown

- **Tiempo:** ~1h  ·  **Categoría:** feature  ·  **Impacto:** bajo
- **Estado:** pendiente
- **Listo cuando:** comando `/exportar` (o variante) genera un .md con el histórico del chat actual y lo escribe a `aclarador-diario/chat-export-YYYY-MM-DD.md` o ruta configurable.
- **Origen:** `roadmap-post-mvp.md` § Refinamientos — Export de conversación a markdown

Tareas:
- [ ] Comando en `adapters/chat/comandos.ts`
- [ ] Lectura del histórico desde SQLite
- [ ] Serialización a markdown legible

#### B24 — F-32 Resumen de estado visual del universo

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** comando o vista que muestra todos los planetas con conteos de misiones/tareas. Al click en un planeta abre filtro.
- **Origen:** `roadmap-post-mvp.md` § F-32

Tareas:
- [ ] Decidir: ¿modal, drawer, página propia?
- [ ] Componente `<UniverseSummary>`
- [ ] Conexión con filtros existentes

---

### Iteración 9 — Vistas alternativas

> Módulos nuevos. Requieren que la base esté estable (DnD funcional, vencidas resueltas).

#### B25 — F-03 Selector de vistas (toggle multi-vista)

- **Tiempo:** ~45 min  ·  **Categoría:** feature  ·  **Impacto:** alto
- **Estado:** pendiente
- **Nota:** prerequisito de B16 (Kanban). Sin el selector de 3 vistas, el Kanban no tiene punto de entrada en la UI.
- **Listo cuando:** el BoardHeader reemplaza el botón toggle actual por 3 botones de ícono (Tag | Date | Kanban). El tipo `modo` en App.tsx es `'tag' | 'date' | 'kanban'` (preparado para `'calendar'` y `'mi-dia'` en el futuro). El modo activo se persiste en `localStorage:agatha:modo` (ya funciona). El Kanban puede mostrar un placeholder hasta que B16 esté listo.
- **Origen:** `roadmap-post-mvp.md` § F-03 + plan Kanban (prerequisito de B16)

Tareas:
- [ ] Refactor de `BoardHeader.tsx`: botón toggle → 3 botones íconos lado a lado
- [ ] Ícono activo: fondo `--color-accent-light`, texto `--color-accent-dark`
- [ ] Ícono Kanban: Lucide `Workflow` o equivalente
- [ ] Tipo `modo`: `'tag' | 'date'` → `'tag' | 'date' | 'kanban'` en App.tsx
- [ ] Rama `modo === 'kanban'` en App.tsx (renderiza `<KanbanBoard>` o placeholder)

#### B26 — F-35 Vista Calendario — diseño

- **Tiempo:** ~2h  ·  **Categoría:** design  ·  **Impacto:** alto  ·  **Depende de:** B25
- **Estado:** pendiente
- **Listo cuando:** mockup de la vista (semanal? mensual? ambas?) con paleta y comportamiento de tareas-en-rango.
- **Origen:** `roadmap-post-mvp.md` § F-35

Tareas:
- [ ] Investigar libraries (FullCalendar, react-big-calendar)
- [ ] Decidir si construir desde cero o usar lib
- [ ] Mockup en Excalidraw

#### B27 — F-35 Vista Calendario — implementación base

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B26
- **Estado:** pendiente
- **Listo cuando:** la vista calendario muestra las tareas con fecha en sus celdas. Click en tarea abre drawer.
- **Origen:** `roadmap-post-mvp.md` § F-35

Tareas:
- [ ] Componente `<CalendarBoard>`
- [ ] Render con tareas filtradas
- [ ] Integración con el watcher

#### B28 — F-34 Vista Mi Día / Bloques — diseño

- **Tiempo:** ~2h  ·  **Categoría:** design  ·  **Impacto:** alto  ·  **Depende de:** B25
- **Estado:** pendiente
- **Listo cuando:** mockup del Método 100 Bloques aplicado, decisión sobre granularidad de bloques de tiempo, decisiones sobre si las tareas tienen duración estimada o no.
- **Origen:** `roadmap-post-mvp.md` § F-34 + `notas.md` § Ideas de mejora #6

Tareas:
- [ ] Investigar el método 100 bloques
- [ ] Mockup
- [ ] Decidir si requiere campo nuevo en frontmatter (`duracion_aprox`)

#### B29 — F-34 Vista Mi Día — implementación base

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B28
- **Estado:** pendiente
- **Listo cuando:** la vista muestra el día como bloques de tiempo según diseño B28. Tareas se asignan a bloques.
- **Origen:** `roadmap-post-mvp.md` § F-34

Tareas:
- [ ] Componente `<MiDiaBoard>`
- [ ] Lógica de asignación tarea → bloque
- [ ] Persistencia (¿en frontmatter o en estado de sesión?)

#### B30 — Vista Bloques: DnD interno + check + duración aprox

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B17, B29
- **Estado:** pendiente
- **Listo cuando:** dentro de la vista Mi Día se pueden arrastrar tareas entre bloques de tiempo, marcarlas con check, y editar la duración aprox.
- **Origen:** `notas.md` § Ideas de mejora #6

Tareas:
- [ ] Reusar setup DnD de B16
- [ ] Check inline en tarjeta de bloque
- [ ] Edit-in-place de duración

---

### Iteración 10 — Telemetría + IA con memoria de patrones

> Los items #7 y #9 de notas.md piden que la IA aprenda patrones. Eso requiere telemetría primero, captura de razones después, y solo entonces integración al modelo. Iteración pesada — solo arrancar cuando el resto esté estable y haya uso real medible.

#### B31 — Diseño esquema logs de interacción + razones de postergación

- **Tiempo:** ~1h  ·  **Categoría:** design  ·  **Impacto:** medio
- **Estado:** pendiente
- **Listo cuando:** decidido qué se loguea (vista, filtro, click, marca completada, postponer), dónde (SQLite extendida o tabla nueva), y cómo se captura la razón al postergar.
- **Origen:** `notas.md` § Ideas de mejora #7 y #9

Tareas:
- [ ] Esquema de tablas
- [ ] Decidir privacy (todo local, sin telemetría externa)
- [ ] Decidir cuánto histórico se mantiene

#### B32 — Telemetría básica (vista, filtro, click, marca)

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** medio  ·  **Depende de:** B31
- **Estado:** pendiente
- **Listo cuando:** los eventos definidos en B31 se registran en SQLite. Hay un comando para inspeccionar el log.
- **Origen:** `notas.md` § Ideas de mejora #9

Tareas:
- [ ] Tabla nueva (`interactions` o similar)
- [ ] Hooks de captura en App.tsx
- [ ] Comando `/log` o vista admin

#### B33 — Captura razón de postergación al cambiar fecha

- **Tiempo:** ~1h  ·  **Categoría:** feature  ·  **Impacto:** medio  ·  **Depende de:** B31
- **Estado:** pendiente
- **Listo cuando:** al posponer una tarea (cambiar fecha hacia adelante), se le pregunta opcionalmente la razón. Se guarda en el log.
- **Origen:** `notas.md` § Ideas de mejora #7

Tareas:
- [ ] Modal/prompt al detectar postergación
- [ ] Guardar en SQLite
- [ ] Permitir saltarlo (no presionar)

#### B34 — Integración de patrones al contexto de Agatha

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** alto  ·  **Depende de:** B32, B33
- **Estado:** pendiente
- **Listo cuando:** el system prompt de Agatha incluye un resumen de patrones detectados (tareas que se postergan seguido, horas en que más completás, etc.). Cacheado.
- **Origen:** `notas.md` § Ideas de mejora #7 y #9

Tareas:
- [ ] Función agregadora de patrones (Rust)
- [ ] Inyección al prompt en `usePromptBase`
- [ ] Validar que no rompa el cache de Anthropic

#### B35 — F-31 Sugerencias proactivas de qué atacar

- **Tiempo:** ~2h  ·  **Categoría:** feature  ·  **Impacto:** medio  ·  **Depende de:** B34
- **Estado:** pendiente
- **Listo cuando:** Agatha puede sugerir tareas en el saludo de inicio de día basándose en peso, fecha y patrones aprendidos. Tono respeta anti-objetivo "sin presión".
- **Origen:** `roadmap-post-mvp.md` § F-31

Tareas:
- [ ] Lógica de scoring para tareas
- [ ] Modificar saludo en skill o en código
- [ ] Validar tono

---

## Backlog futuro

> Bloques sin iteración asignada. Esperan signal del uso real para activarse. La skill `planificador-mejoras` los puede mover a una iteración cuando aparezca contexto que los justifique.

- `[ ]` BF01 — F-36 Integración Gmail (captura desde mails marcados)
- `[ ]` BF02 — F-37 Integración WhatsApp (captura desde mensajes forwardeados)
- `[ ]` BF03 — F-38 Integración Google Calendar (lectura)
- `[ ]` BF04 — F-39 Interfaz de voz (STT/TTS)
- `[ ]` BF05 — F-29 Modo oscuro
- `[ ]` BF06 — F-30 Wizard de onboarding visual (post-MVP, si Agatha llega a otra máquina)
- `[ ]` BF07 — F-26 Sección rápida de Nebulosa accesible desde Agatha
- `[ ]` BF08 — F-27 Procesamiento por lotes asistido
- `[ ]` BF09 — Refresh diferencial del watcher (solo si vault crece a miles de tareas)

---

## Reglas del plan

> Invariantes que respeta la skill `planificador-mejoras` al modificar este doc. También aplican si lo editás a mano.

1. **Bloque ≤ 2h.** Si una idea excede, dividir en sub-bloques. Sesión = bloque.
2. **Listo cuando obligatorio.** Sin un criterio claro, no es bloque ejecutable.
3. **Bloques completados nunca se borran.** Son historia útil.
4. **Bloques obsoletos no se borran**, se marcan con `estado: obsoleto` + razón.
5. **No renumerar.** Los IDs son referencia estable.
6. **Categorías exclusivas.** Un bloque es UX o feature, no las dos.
7. **Dependencias hard.** Un bloque dependiente NO se trabaja antes que su prerequisito.
8. **Diseño antes de implementar.** Para features grandes (>2h totales o que tocan UX), preceder con bloque `design`.
9. **Estado actual sincronizado.** Los contadores arriba reflejan los bloques abajo.
10. **Capturas inmutables.** `notas.md` y `roadmap-post-mvp.md` no se modifican desde acá. Son fuente, no destino.

---

## Cómo se mantiene este documento

Cuando agregás ideas a `notas.md` (sección "Ideas de mejora del sistema") o features al `roadmap-post-mvp.md`, invocá la skill `planificador-mejoras` (decile a Claude Code "actualizá el plan" o "agregué ideas nuevas a notas"). La skill lee las fuentes, identifica lo nuevo, lo clasifica (categoría/tiempo/impacto/dependencias), y lo inserta acá donde corresponda.

La skill nunca borra bloques completados, nunca renumera, y siempre reporta qué cambió. Si hace algo que no esperabas, podés volver atrás vía git.
