# 🗒️ Notas

Captura rápida de cosas que no quiero perder. Escribo aquí al vuelo, sin preocuparme por el formato. Un chat por lote procesa estas notas y las convierte en acciones.

---

## ✏️ Tareas con modificación

Cambios que hacerle a tareas existentes: pesos, fechas, cancelaciones, cambios de estado, etc. Escribir en texto libre — la IA infiere a qué tarea se refiere.

- [ ]

---

## 💡 Ideas de mejora del sistema

Cosas que le faltan al vault, al skill o a los flujos. Se discuten cuando haya tiempo de diseñarlas.

- [ ]  Cuando cambio de peso, debo manualmente cambiar el icono de peso(bolita de color)
- [ ] **Kanban real con drag-and-drop (Etapa 2 del rediseño de estados)** — Hoy (19-abr-2026) implementamos la Etapa 1: tags de estado (`#pendiente`, `#en-espera`, `#bloqueada`, `#completada`) + Tag board de CardBoard para visualización. CardBoard NO permite arrastrar tarjetas entre columnas, solo visualiza. Cuando esto madure, explorar un Kanban real donde pueda mover una tarjeta de "Pendiente" → "En progreso" → "Completada" y que el archivo .md se actualice solo. Al hacerlo, añadir `#en-progreso` como 5º estado (hoy no está porque sin drag sería solo ceremonia: editar frontmatter manualmente para un cambio puramente visual). **Opciones técnicas exploradas:** (a) plugin Kanban (mgmeyers) → descartado porque cada tablero es autocontenido, no lee .md externos; (b) Dataview JS + botones "▶ Iniciar / ✅ Completar / ⏸ En espera" en cada tarjeta que modifiquen el frontmatter al click → camino más probable. Dataview JS ya está habilitado en el vault.
- [ ] **Sincronización automática de dependencias al completar tarea** — Cuando marco la tarea A como completada (desde CardBoard, editor, o chat), quiero que la tarea B listada en su `desbloquea:` pase automáticamente de `#bloqueada` a `#pendiente` y pierda su `🔒` en la línea CardBoard, sin que yo tenga que hacerlo a mano. Hoy la skill §4.2 describe este cambio pero como "propuesta del agente con confirmación", lo cual obliga a abrir chat. Queremos que sea reactivo en Obsidian mismo. Base técnica: Dataview JS (ya activado) puede leer frontmatter y modificar archivos — explorar si alcanza solo o si conviene sumarle Templater. Relacionado con el Kanban Etapa 2 porque comparten la capa de "scripts que editan .md al click". **2026-04-23: confirmado necesario en la práctica** — al iniciar el día se detectaron 3 desincronizaciones acumuladas (tag `#pendiente` con línea `[x]`) por marcar tareas rápidamente en CardBoard sin pasar por chat: `05a-planear-seccion-alumnos`, `clase-6-practicar`, `clase-6-generar`. Además, `05b-implementar-seccion-alumnos` quedó huérfana como `#bloqueada` aunque su `bloqueada_por` (05a) ya estaba completada. La fricción ya se manifiesta — priorizar cuando haya ventana.
- [ ] **Decisión abierta: ¿sincronización automática requiere confirmar?** — La regla maestra de la skill es "CONFIRMA ANTES DE ACTUAR" (§4 intro). Pero cuando se trate de sincronizar dependencias (A completada → B a pendiente), acordé que fuera automático sin preguntar. Esto choca con la regla maestra. Hay que decidir: (a) excepción explícita en §4.2 declarando que la sincronización de dependencias es la única acción automática porque es consecuencia mecánica de algo que el usuario ya confirmó (completar A), o (b) mantener confirmación siempre, asumiendo fricción extra. Mi intuición: (a), porque la confirmación al completar A ya cubre todo el efecto dominó. Discutir antes de implementar el script.
- [ ] **Investigar tecnología exacta para el script de sincronización** — Opciones a validar cuando arranque la implementación: (1) Dataview JS puro — ¿puede escribir frontmatter, o solo leer? (2) Templater — bueno para plantillas reactivas, disparado por eventos. (3) Plugin externo tipo QuickAdd o MetaEdit que expongan una API más cómoda. (4) Script bash/python + atajo del sistema operativo para procesar el vault fuera de Obsidian (último recurso, pierde el "tiempo real"). Criterio de decisión: mínima dependencia, menor superficie de mantenimiento, y que el cambio al frontmatter sea atómico (no quiero ver el archivo medio modificado si algo falla).
 - [ ] Filtro al cardboard y que al momento de seleccionar uno de esos filtros solo muestras esas tareas en el tablero, por ejemplo hice un tablero de app-enterbase y muestra todas las tareas de las demas submisiones pero cual digamos filtro por submisiones , por ejemplo solo exportaciones, debe mostrarme las tareas solo de exportaciones, esto para evitar tener que crear un tablero para cada submision
- [ ] **Definir convención de archivado de misiones/sub-misiones completadas** — La skill §4.10 dice "mueve el archivo a una carpeta `_archivo/` dentro del planeta", pero eso entra en conflicto con las queries Dataview que leen `FROM "enter-tech-school"` (seguirían viendo lo archivado). Decidir: (a) `_archivo/` dentro del planeta + ajustar todas las queries con `-"enter-tech-school/_archivo"`, o (b) `_archivo/` en la raíz del vault (más limpio para Dataview, pero rompe la cercanía contextual con el planeta). Además definir qué pasa con las tareas dentro — ¿se mueven junto con la sub-misión? ¿se deja solo el `_aclarador.md`? Pendiente hasta tener primera sub-misión candidata concreta (hoy `formulario-matriculados` completada, se dejó activa por no tener aún esta definición). Anotado 2026-04-22.


---

## 🌫️ Nebulosa (sin categoría)

Lo que no encaja en las otras dos secciones: referencias, preguntas sueltas, datos que no quiero olvidar, ideas que después decido dónde van.

- Mover tareas de block de notas sueltas en escritorio a notas.md
