# Propuesta: Plugins y Mejoras Visuales del Vault

> **Estado: APROBADA** — Aprobada el 14-abr-2026. Implementación en curso.
> Fecha: 14-abr-2026

---

## El problema

El vault funciona bien a nivel de estructura y archivos, pero la experiencia visual al usarlo en Obsidian se queda corta. Los puntos de dolor actuales son:

- Las tareas se ven como texto plano sin jerarquía visual clara.
- El plugin Tasks (Clare Macrae) solo filtra por descripción, sin opciones avanzadas de filtrado por fecha, tags, prioridad o carpeta.
- El formato de fechas doble `(14-abr-2026) 📅 2026-04-14` genera ruido visual.
- No hay vista de tablero (Kanban) para ver estados de un vistazo.
- No hay vista de calendario para ver distribución de tareas por día/semana.
- No hay conexión con Google Calendar, que es donde llegan las tareas de ClickUp del trabajo.

---

## La propuesta: 5 plugins + 1 tema

Se propone reemplazar el plugin Tasks por una combinación de herramientas especializadas que cubren cada necesidad.

### Plugin 1: Dataview — El cerebro de los dashboards

| | |
|---|---|
| **Qué hace** | Queries avanzadas sobre los archivos del vault. Filtra tareas por carpeta, fecha, tags, texto, estado, y las muestra como listas o tablas. |
| **Reemplaza a** | Plugin Tasks (las queries en universo.md y mapas estelares). |
| **Por qué** | Tasks solo permite filtros básicos por descripción. Dataview permite hacer cosas como: "muéstrame todas las tareas de enter-tech-school que tengan fecha esta semana y no estén completadas", o "muéstrame las tareas con ⏳ agrupadas por archivo". |
| **Complejidad** | Media. Las queries se escriben en los archivos .md y el agente IA las puede generar/editar. |
| **Costo** | Gratuito. |

**Ejemplo de query Dataview vs Tasks:**

Tasks (actual):
```
not done
path includes enter-tech-school
description does not include #exclude
```

Dataview (propuesto):
```dataview
TASK
FROM "enter-tech-school"
WHERE !completed
SORT due ASC
```

La query de Dataview es más legible, más potente y permite ordenar, agrupar y filtrar con mucha más flexibilidad.

---

### Plugin 2: CardBoard — Tu tablero Kanban

| | |
|---|---|
| **Qué hace** | Muestra las tareas de tus archivos .md como tarjetas en columnas tipo Trello (Por hacer, En progreso, Hecho). |
| **Cómo funciona** | Lee directamente los `- [ ]` y `- [x]` de tus archivos. Si mueves una tarjeta o la completas en el tablero, se actualiza el archivo .md automáticamente. No duplica datos. |
| **Vistas posibles** | Por tags, por fecha, o por carpeta (planeta). |
| **Por qué** | Visualmente un tablero Kanban permite ver de un vistazo el estado general de un planeta o de todo el universo. Es mucho más rápido que leer listas. |
| **Complejidad** | Baja. Se configura una vez y funciona. |
| **Costo** | Gratuito. |

---

### Plugin 3: Google Calendar — Ver tu calendario del trabajo en Obsidian

| | |
|---|---|
| **Qué hace** | Muestra tu Google Calendar dentro de Obsidian como una vista lateral o embebida. Puedes ver, crear y editar eventos. |
| **Por qué** | Las tareas de ClickUp del trabajo se sincronizan con Google Calendar. Con este plugin puedes ver esas tareas dentro de Obsidian sin salir de tu vault. Todo tu contexto en un solo lugar. |
| **Autor** | YukiGasai. |
| **Complejidad** | Media. Requiere autenticación con tu cuenta de Google (OAuth). El agente IA puede guiarte paso a paso. |
| **Costo** | Gratuito. |
| **⚠️ Advertencia** | El autor marcó el plugin como "stale" (no lo mantiene activamente). Funciona a día de hoy, pero no hay garantía de actualizaciones futuras. Si deja de funcionar, se puede reemplazar o desinstalar sin afectar el vault. |

---

### Plugin 4: Full Calendar — Vista de calendario de tus tareas del vault

| | |
|---|---|
| **Qué hace** | Crea una vista de calendario (día/semana/mes) dentro de Obsidian que lee las fechas de tus archivos .md y muestra tus tareas distribuidas en el tiempo. |
| **Diferencia con Google Calendar** | Google Calendar muestra tus eventos EXTERNOS (ClickUp, reuniones). Full Calendar muestra tus tareas INTERNAS del vault (las misiones). Son complementarios. |
| **Por qué** | Permite ver de un vistazo si tienes días sobrecargados, semanas vacías, o conflictos de fechas entre misiones. |
| **Complejidad** | Baja-media. |
| **Costo** | Gratuito. |

---

### Plugin 5: Style Settings — Personalización visual

| | |
|---|---|
| **Qué hace** | Permite personalizar colores, tipografía, checkboxes y otros elementos visuales del tema que uses. |
| **Por qué** | Acompaña al tema Minimal para darle tu toque personal. Puedes cambiar los colores de las checkboxes, el estilo de las tarjetas, las fuentes, etc. |
| **Complejidad** | Baja. Es un panel de ajustes visual, sin código. |
| **Costo** | Gratuito. |

---

### Tema: Minimal — La capa visual

| | |
|---|---|
| **Qué hace** | Tema comunitario que transforma la apariencia de Obsidian. Diseño limpio, tipografía profesional, soporte especial para Dataview (tarjetas), checkboxes con estilos, y un look general muy pulido. |
| **Por qué** | El tema por defecto de Obsidian es funcional pero visualmente plano. Minimal es el tema más popular de la comunidad y está activamente mantenido. |
| **Combina con** | Style Settings para personalización fina. |
| **Complejidad** | Baja. Se instala desde Apariencia → Temas. |
| **Costo** | Gratuito. |

---

## Resumen visual

```
┌─────────────────────────────────────────────────────────┐
│                    TU VAULT EN OBSIDIAN                  │
│                                                         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │  Dataview    │  │  CardBoard   │  │ Full Calendar  │  │
│  │  Dashboards  │  │  Kanban      │  │ Tareas x fecha │  │
│  │  inteligentes│  │  visual      │  │ del vault      │  │
│  └─────────────┘  └──────────────┘  └───────────────┘  │
│                                                         │
│  ┌──────────────────────┐  ┌─────────────────────────┐  │
│  │  Google Calendar      │  │  Minimal + Style        │  │
│  │  Eventos externos     │  │  Settings               │  │
│  │  (ClickUp, reuniones) │  │  Look profesional       │  │
│  └──────────────────────┘  └─────────────────────────┘  │
│                                                         │
│  ┌─────────────────────────────────────────────────────┐│
│  │  Archivos .md — Tu vault sigue siendo tuyo          ││
│  │  Los plugins leen/escriben sobre los mismos archivos││
│  │  Si algún plugin muere, tus datos siguen intactos   ││
│  └─────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

---

## Lo que se elimina

| Se elimina | Razón |
|---|---|
| **Plugin Tasks** (Clare Macrae) | Reemplazado por Dataview (queries más potentes) + CardBoard (vista visual). |
| **Formato de fecha doble** | Sin el plugin Tasks, ya no necesitamos `📅 YYYY-MM-DD`. Podemos usar solo la fecha legible `(DD-mes-AAAA)` o evaluar qué formato le funciona a Dataview. |

---

## Lo que cambia en el vault

Si se aprueba esta propuesta, los cambios en archivos serían:

1. **universo.md** — Reescribir queries de Tasks a Dataview.
2. **Cada _mapa-estelar.md** — Reescribir queries de Tasks a Dataview.
3. **skill/control-de-mision.md** — Actualizar convenciones de fechas y referencias a plugins.
4. **Tareas existentes (app-enterbase.md)** — Ajustar formato de fechas al nuevo estándar.
5. **_plantillas/** — Actualizar plantillas con el nuevo formato.

El agente IA se encarga de todos estos cambios. No hay que hacerlo manualmente.

---

## Orden de instalación propuesto

Paso a paso, uno a la vez:

1. **Minimal + Style Settings** — Primero el look, para que todo lo demás se vea bien desde el inicio.
2. **Dataview** — Reemplazar las queries de Tasks. Verificar que los dashboards funcionen.
3. **Desinstalar Tasks** — Ya no se necesita.
4. **CardBoard** — Configurar el tablero Kanban.
5. **Full Calendar** — Vista de calendario de las tareas del vault.
6. **Google Calendar** — Conectar con tu cuenta de Google para ver eventos externos.

---

## Riesgos y consideraciones

| Riesgo | Mitigación |
|---|---|
| Google Calendar plugin está "stale" | Si deja de funcionar, se desinstala. El vault no depende de él. |
| Dataview tiene curva de aprendizaje | El agente IA escribe y mantiene las queries. Tú no necesitas aprenderlas. |
| Demasiados plugins ralentizan Obsidian | Son 5 plugins + 1 tema. Es una cantidad razonable. Obsidian maneja bien hasta 15-20 plugins sin problema. |
| Full Calendar y Google Calendar se solapan | No se solapan: uno muestra tareas del vault, el otro eventos externos. Son complementarios. |

---

## Filosofía intacta

Esta propuesta respeta los principios del sistema:

- ✅ Los archivos .md siguen siendo tuyos — ningún plugin los secuestra.
- ✅ Si Obsidian o cualquier plugin desaparece, tus datos siguen funcionando.
- ✅ El agente IA sigue operando igual — lee y edita los mismos archivos.
- ✅ La estructura no cambia — solo mejora la forma de visualizarla.
- ✅ Todo es gratuito.

---

> **Siguiente paso:** Revisa esta propuesta. Dime qué apruebas, qué cambiarías, qué sobra, qué falta. Después implementamos juntos, paso a paso.
