---
tags:
  - mis-proyectos-dev
  - agatha
  - vision-producto
tipo: documento-producto
---

# 📘 Visión de Producto — Agatha

> Documento vivo. Captura el **qué** y el **por qué** del producto, 
> separado del **cómo** técnico. Se llena con el tiempo, a medida que 
> se toman decisiones y se descubren cosas usando el sistema.
>
> **Audiencia:** yo del futuro y/o el agente IA que ayude a desarrollar 
> la app web cuando llegue el momento.
>
> **Convive con `skill/control-de-mision.md`:** la skill describe cómo 
> opera el agente sobre el sistema de gestión actual. Este documento 
> describe qué es Agatha como producto, por qué existe, y qué 
> decisiones la formaron.

---

## 1. Visión

Agatha es **mi cabina de mando personal**: una entidad unificada 
—datos, vistas y voz IA en una sola cosa— desde donde reviso todo lo 
que tengo entre manos (trabajo y vida personal), decido qué atacar, 
ejecuto cambios y mantengo el sistema vivo.

La interacción es **colaborativa**: yo actúo (marco una tarea, muevo 
una tarjeta), ella reacciona (desbloquea dependencias, automatiza 
flujos, me devuelve mensajes que me conectan con mi progreso).

Es un **organismo que evoluciona**: empieza con un Kanban filtrable 
como su primera vista, y crece incorporando otras (generador de 
horario diario, etc.) que comparten su mismo cerebro de datos —los 
`.md` del vault.

---

## 2. Problema que resuelve

El sistema de gestión personal en `gestiono-mi-vida/` ya tiene un 
modelo de datos rico (jerarquía de 4 niveles, tags de estado, pesos, 
dependencias, fechas múltiples), pero **le falta un centro unificado 
que lo opere**. Hoy la operación está fragmentada entre varias 
herramientas externas, ninguna diseñada específicamente para este 
sistema:

- **CardBoard** muestra tareas pero no permite filtros dinámicos por 
  sub-misión, no soporta drag & drop entre columnas, no expone la 
  riqueza del modelo (dependencias, pesos), y obliga a crear un 
  tablero por cada agrupación.
- **El editor de Obsidian** sirve para ver `.md` pero no es una 
  interfaz de operación —editar frontmatter a mano para cambiar 
  estado es fricción.
- **Las queries Dataview** muestran info pero no permiten interactuar 
  con ella —son solo lectura.
- **El agente IA (chat)** opera bien pero requiere abrir conversación 
  cada vez —no está integrado en la vista que el usuario consume a 
  diario.

El resultado: el usuario interactúa principalmente con CardBoard, pero 
CardBoard no fue hecho para este sistema. Las limitaciones se acumulan 
hasta que se vuelven fricción. Agatha resuelve esto siendo **una 
interfaz hecha exactamente para este sistema**, donde la visualización, 
la interacción y la IA viven en un solo lugar.

---

## 3. Principios de producto

(No negociables. Cada principio se anota con la razón por la que existe.)

- **Los datos viven en `.md` planos.** La capa visual es reemplazable; 
  los archivos no. Razón: el sistema sobrevive a cualquier herramienta 
  específica (Obsidian, app web, lo que venga).

- **El sistema se adapta al usuario, no al revés.** Razón: ya está 
  declarado en la filosofía del vault y en `context/yo.md` — el sistema 
  existe para quitar peso mental, no para agregarlo.

- **Agatha se construye con cariño, no con exigencia.** Razón: el 
  nombre Agatha lo hace explícito (ver §4 — origen del nombre). 
  Cualquier feature, mensaje o flujo que vaya en contra de este tono 
  —que agregue presión, que exija, que haga sentir mal al usuario— 
  viola este principio fundacional. Los 3 Bosses del usuario 
  (`context/yo.md`) son enemigos directos de Agatha.

- (Más principios se irán agregando con el tiempo.)

---

## 4. Decisiones de producto tomadas

Lista cronológica. Cada entrada: **fecha — decisión — contexto y razón.**

- **2026-04-25 — Construir Kanban propio en lugar de extender CardBoard.** 
  Contexto: durante la sesión de planeación se evaluó si era viable 
  agregar un filtro al CardBoard existente (modificar el plugin) o 
  construir uno propio con HTML/JS dentro de Obsidian. Razón de la 
  decisión: modificar el plugin es frágil ante updates y no resuelve 
  las otras limitaciones (drag & drop, integración IA, creación de 
  tableros). Construir uno propio es más trabajo pero abre la puerta a 
  todas las mejoras pendientes y al horizonte de la app web.

- **2026-04-25 — Alcance: tablero "nivel 3 superior".** Contexto: se 
  evaluaron 3 niveles de alcance — (1) solo lectura con filtros, (2) 
  con acciones rápidas, (3) Kanban completo con drag & drop y creación 
  de tableros. Decisión: ir directo al nivel 3 superior, incluyendo 
  todo lo que CardBoard ofrece + las mejoras visuales pendientes en 
  `notas.md`. Razón: el usuario interactúa principalmente con el 
  tablero (no con los `.md`), así que la inversión se justifica.

- **2026-04-25 — Diseñar desde el día 1 pensando en integración con IA.** 
  Contexto: hoy ya se interactúa con IA para gestionar el vault, y a 
  futuro se quiere que un modelo IA actúe de forma autónoma sobre el 
  sistema. Decisión: la arquitectura de Agatha debe contemplar esta 
  integración desde el inicio, aunque la implementación se haga después. 
  Razón: agregar IA después de un diseño que no la contempló suele 
  costar más que diseñarlo bien desde el principio.

- **2026-04-25 — Agatha es el prototipo de una futura app web.** 
  Contexto: el usuario considera evolucionar el sistema a una app web 
  más adelante. Decisión: tratar a Agatha como prototipo formal de 
  esa app — mismas decisiones de UX, mismas estructuras de datos, 
  misma lógica de negocio. Razón: lo aprendido aquí debe poder 
  reutilizarse, no descartarse.

- **2026-04-25 — Implementación a cargo de Claude Code, no del usuario.** 
  Contexto: el usuario no programará Agatha él mismo — lo hará su 
  agente de codificación. Decisión: la planeación debe ser lo 
  suficientemente clara para que Claude Code pueda ejecutar sin 
  ambigüedad. Razón: la fricción de la implementación se delega; el 
  esfuerzo del usuario está en pensar bien el producto.

- **2026-04-25 — Renombrar a "Agatha" y ampliar el alcance a plataforma 
  personal unificada.** Contexto: durante la Etapa 1 de planeación, al 
  rescatar elementos de varias alternativas de visión, el usuario 
  aterrizó que el sistema no es un tablero de tareas sino una 
  plataforma central que también incluirá generador de horario diario 
  y otras herramientas. En el mismo flujo, decidió darle un nombre 
  propio. Decisión: renombrar la misión a `agatha/` (pasando antes por 
  `mi-kanban/` y `mi-cerebro/` durante la conversación). Razón doble: 
  (1) si el nombre limita el alcance mental, frena la evolución natural 
  del producto; (2) un nombre propio crea vínculo y compañía, no 
  obligación — encaja con la filosofía del vault de "quitar peso 
  mental, no agregarlo". El Kanban pasa a ser **la primera vista** de 
  Agatha, no el todo.

- **2026-04-25 — Agatha es una entidad unificada: sistema + vistas + IA 
  son una sola cosa (no piezas separadas).** Contexto: al definir el 
  nombre se evaluaron tres formas de pensarlo: (a) Agatha es solo el 
  sistema, (b) Agatha es solo la IA, (c) Agatha es ambas 
  indistintamente. Decisión: opción (c). Razón: la sensación buscada es 
  la de tener una compañera con memoria (los `.md`), ojos (las vistas) 
  y voz (la IA) — todo siendo ella misma. Separar las piezas pierde esa 
  unidad emocional. Implicación de diseño: el lenguaje del producto 
  siempre se refiere a "Agatha" como sujeto, no a "el sistema" o "el 
  agente" o "el tablero" como entidades aparte.

- **2026-04-25 — Etapa 1 de planeación cerrada (visión, anti-objetivos, 
  glosario).** Contexto: la sesión del 25-abr completó las 3 secciones 
  fundacionales del documento: §1 Visión, §6 Anti-objetivos, §7 
  Glosario. Quedan abiertas para sesiones futuras: §5 Casos de uso 
  reales (se llena observando uso) y completar las secciones 1-7 a 
  medida que aparezcan más decisiones. Próximas etapas planeadas: 
  Etapa 2 (mapear uso actual de CardBoard para llenar §5), Etapa 3 
  (definir features del MVP), Etapa 4 (diseño visual), Etapa 5 (brief 
  de implementación para Claude Code). Razón de cerrar Etapa 1 acá: la 
  visión, los anti-objetivos y el glosario son el "norte" del producto 
  — sin ellos, las features se inventan en el aire. Con ellos, las 
  decisiones siguientes se filtran solas.

- **2026-04-25 — Definidos 8 anti-objetivos en 3 categorías (propósito, 
  comportamiento, alcance técnico).** Contexto: durante la Etapa 1 de 
  planeación se redactaron y aterrizaron los 8 anti-objetivos de la 
  Sección 6, con matices de futuro explícitos donde aplica (hábitos en 
  A2, integraciones externas en A7, evolución del canal de chat en A8). 
  Razón: los anti-objetivos son la defensa contra el scope creep — 
  permiten descartar ideas tentadoras sin tener que pensarlas desde 
  cero. También cumplen un rol terapéutico para el usuario: dan permiso 
  explícito de no hacer cosas, reduciendo la presión interna de 
  "cubrirlo todo". Hallazgo importante de la conversación: el usuario 
  aportó el matiz de A5 (no caer en interrogatorios extensos con 
  preguntas abiertas) — esto se elevó a regla de comportamiento del 
  producto y también informa cómo el agente IA debe interactuar en 
  general (preferir menús cerrados sobre preguntas abiertas en flujos 
  operativos).

- **2026-04-25 — Origen del nombre Agatha.** El usuario eligió este 
  nombre porque es el que reservaba para una hija futura. Significado: 
  del griego *agathē*, "buena". Esta nota se documenta deliberadamente 
  porque tiene peso: el sistema no se nombra con un término técnico ni 
  con un nombre arbitrario — se nombra con el nombre más cuidado que el 
  usuario tenía guardado. Eso marca el tono del producto: Agatha se 
  construye con cariño, no con exigencia. Es la antítesis del 
  perfeccionismo que el usuario combate (ver `context/yo.md` → "los 3 
  Bosses"). Cualquier decisión futura sobre Agatha que vaya en contra 
  de este tono — agregar fricción, exigir, hacer sentir mal al usuario 
  — viola este principio fundacional.

---

## 5. Casos de uso reales

(Se llena con el tiempo. Cada caso describe **cómo** el usuario usa 
realmente el tablero en su día a día — no cómo *debería* usarlo.)

- (Por documentar.)

---

## 6. Anti-objetivos

Lo que Agatha **no** debe ser. Importante para no caer en scope creep 
cuando aparezcan ideas tentadoras.

### Categoría 1 — Anti-objetivos de propósito

- **A1. Agatha NO es una herramienta de productividad genérica.** 
  No compite con Notion, Trello, Asana, ClickUp, Todoist. No intenta 
  servir a otros usuarios. Está diseñada exclusivamente para el 
  usuario, su cerebro, su vida. Si una decisión va en dirección de 
  "esto sería útil para más gente", se descarta.

- **A2. Agatha NO es una app de hábitos ni de tracking emocional 
  (en su versión actual).** No registra estado de ánimo, no cuenta 
  rachas, no muestra métricas de productividad ("llevas 7 días seguidos 
  completando tareas"), no da insignias ni gamifica nada. Razón: 
  contar activa al perfeccionista, y la prioridad es **hacer lo que 
  importa, no medirlo**.
  
  *Excepción futura:* cuando se integre un sistema de hábitos a Agatha 
  (planeta `mis-sistemas-identidad/` aún sin misiones activas), esto 
  se revisará — pero con cuidado: las métricas que se permitan deben 
  servir al usuario, no juzgarlo.

- **A3. Agatha NO reemplaza a Obsidian.** Vive **dentro** de Obsidian 
  (al menos en su primera vida, antes de la app web). No intenta 
  reemplazar el editor de markdown, ni el sistema de links, ni los 
  plugins generales. Solo reemplaza la **capa de operación** sobre 
  las tareas.

### Categoría 2 — Anti-objetivos de comportamiento

- **A4. Agatha NO genera culpa, presión ni urgencia artificial.** 
  No usa colores rojos para "tareas atrasadas", no muestra contadores 
  de "días vencidos", no manda notificaciones que dicen "tienes 5 
  tareas pendientes". Si hay tareas viejas, las muestra con respeto: 
  "tienes algunas cosas pendientes de antes, ¿quieres revisarlas?". 
  El lenguaje y los colores deben ser cuidadosos.

- **A5. Agatha NO actúa sin que el usuario sepa qué hizo, pero 
  tampoco debe interrumpir el flujo con preguntas innecesarias.** 
  Hay dos errores opuestos a evitar: (a) magia silenciosa (Agatha 
  cambia cosas sin avisar) y (b) interrogatorio (Agatha frena al 
  usuario con preguntas abiertas extensas cada vez que actúa). Ambos 
  generan fricción. La solución correcta es:
  - **Acciones con consecuencia mecánica obvia** (ej: completar una 
    tarea desbloquea a su dependiente) se ejecutan **automáticamente y 
    se reflejan visiblemente** en el tablero. Sin preguntar. Si el 
    usuario quiere revertir, lo ve y revierte.
  - **Acciones con ambigüedad real** (ej: "¿esta nota va como destello 
    o como tarea?") se resuelven con **menús de opciones cerradas** 
    (3-5 botones), no con preguntas abiertas. Click, decidido, sigue.
  - **Las preguntas abiertas se reservan para conversaciones reales 
    con la IA**, no para flujos operativos.
  
  Principio: la confianza con un sistema autónomo se construye con 
  **transparencia visible**, no con confirmaciones constantes.

- **A6. Agatha NO trata al usuario como si fuera frágil.** No suaviza 
  todo, no dora la píldora, no usa lenguaje terapéutico exagerado. 
  Habla como un amigo cercano que lo conoce: directo, cálido, sin 
  condescendencia. Si algo está mal, lo dice. Si algo va bien, lo 
  celebra brevemente. No hace discursos.

### Categoría 3 — Anti-objetivos de alcance técnico

- **A7. Agatha NO sincroniza con servicios externos en su versión 
  inicial.** No se conecta a Google Calendar (más allá de leer el 
  plugin existente), no jala de ClickUp, no integra Slack, no sube 
  nada a la nube. Vive 100% local, sobre los `.md` del vault.
  
  *Excepción futura planeada:* el usuario hoy captura manualmente 
  tareas que llegan desde Gmail y WhatsApp. La integración con esos 
  servicios para auto-capturar tareas es un horizonte conocido, pero 
  **no entra en el MVP**. Se aborda como evolución posterior, cuando 
  Agatha sea sólida sobre datos locales.

- **A8. Agatha NO requiere configuración compleja para empezar a 
  usarla.** No tiene wizard de onboarding de 10 pasos, no requiere 
  definir 20 ajustes antes de la primera vista útil. Funciona bien con 
  defaults sensatos desde el primer momento. La personalización 
  avanzada existe pero está oculta para quien no la busca.
  
  *Nota sobre la evolución del canal de interacción:* hoy el chat con 
  Agatha sucede vía Cowork. En etapas futuras se integrará un chat 
  propio dentro de Agatha, posiblemente con modelo Claude vía API y 
  eventualmente con interfaz de voz. La filosofía "sin fricción para 
  empezar" debe sostenerse en cada etapa: el usuario no debería tener 
  que configurar nada complejo para abrir Agatha y empezar a hablarle.

---

## 7. Glosario de negocio

Términos del dominio explicados desde el **por qué**, no desde el qué. 
El "qué" técnico ya vive en `README.md` y `skill/control-de-mision.md`; 
acá se documenta el sentido y la intención detrás de cada término.

### Términos heredados del vault (referencia)

Estos términos ya están definidos en `README.md` (sección "Glosario 
astronómico"). Se listan acá solo para que un agente externo sepa que 
existen y dónde encontrarlos:

- **Universo, Planeta, Mapa estelar, Misión, Sub-misión, Aclarador, 
  Aclarador diario, Nebulosa mental, Destellos, Notas, Control de 
  Misión.** → Ver `README.md` para la definición completa.

**Por qué la metáfora astronómica importa para Agatha:** no es 
decoración. Es una arquitectura mental que separa **escalas de 
atención**: lo cercano y operativo (tareas), lo de mediano plazo 
(misiones), lo de largo plazo (planetas), lo no procesado (nebulosa). 
Agatha debe respetar esas escalas en su diseño visual y de interacción 
— no aplanar todo a "una lista de tareas".

### Términos propios de Agatha

(Se irán agregando con el tiempo. Estos son los aterrizados en la Etapa 
1 de planeación.)

- **Agatha.** Nombre propio del sistema. Significa "buena" en griego 
  (*agathē*). El usuario eligió este nombre porque es el que reservaba 
  para una hija futura. **Por qué importa:** marca el tono fundacional 
  del producto — Agatha se construye con cariño, no con exigencia. Es 
  la antítesis de los "3 Bosses" del usuario (perfeccionista, 
  controlador rígido, juez interior). Cualquier feature, mensaje o 
  comportamiento que viole este tono, viola la identidad del producto.

- **Cabina de mando.** Forma de referirse a Agatha como interfaz. 
  Significa que es el **lugar único** desde donde se opera todo el 
  sistema — no una herramienta más entre varias. **Por qué importa:** 
  define una expectativa de cobertura — si el usuario tiene que salir 
  de Agatha para hacer algo importante de su gestión personal, Agatha 
  está incompleta para ese caso.

- **Vista.** Cada forma distinta de mirar y operar los datos del vault 
  dentro de Agatha. La primera vista es el **Kanban**. Vendrán otras 
  (generador de horario diario, etc.). **Por qué importa:** las vistas 
  son intercambiables y se agregan sin romper las anteriores — todas 
  comparten el mismo cerebro de datos (los `.md`). Esto hace que 
  Agatha pueda crecer sin reescribirse.

- **Cerebro de datos.** Los archivos `.md` del vault. Son la fuente 
  única de verdad. Las vistas, la IA y cualquier futura app web son 
  capas sobre el cerebro de datos. **Por qué importa:** garantiza que 
  Agatha es portable y sobrevive a cualquier herramienta. Si Obsidian 
  desaparece mañana, el cerebro de datos sigue intacto y se puede leer 
  con otra herramienta.

- **Colaboración Usuario ↔ Agatha.** Modelo de interacción donde el 
  usuario actúa (marca tareas, mueve tarjetas, escribe en chat) y 
  Agatha reacciona (sincroniza dependencias, automatiza flujos, 
  responde con mensajes que conectan al usuario con su progreso). **Por 
  qué importa:** Agatha NO es un asistente pasivo que solo responde 
  cuando se le pregunta, ni un automatizador silencioso que actúa solo. 
  Es una compañera reactiva — siempre presente, siempre transparente.

- **MVP de Agatha.** Versión mínima viable del producto que se 
  construye primero. Alcance: el Kanban filtrable como única vista, 
  con las funcionalidades esenciales para reemplazar a CardBoard en el 
  uso diario. **Por qué importa:** el MVP es la prueba de concepto que 
  decide si el rumbo de Agatha es correcto. Si el MVP funciona en el 
  uso real del usuario, se construyen las siguientes vistas. Si falla, 
  se replantea sin haber gastado meses construyendo todo de una.

- **Modo enfoque.** Capacidad de Agatha de mostrar **solo lo necesario 
  en cada momento**, no todo siempre. Implementación concreta por 
  definir, pero el principio es claro: el usuario decide qué subset de 
  su universo quiere ver (por planeta, por misión, por sub-misión, por 
  estado, por fecha) sin tener que crear un tablero por cada 
  combinación. **Por qué importa:** la sobrecarga visual es enemiga de 
  la atención. Mostrarlo todo al mismo tiempo es lo que hace que 
  CardBoard frustre al usuario hoy.

- **Acción con consecuencia mecánica.** Cualquier acción del usuario 
  que tiene un efecto directo y predecible sobre otros datos del 
  sistema (ej: completar una tarea desbloquea a sus dependientes). 
  **Por qué importa:** según el anti-objetivo A5, estas acciones se 
  ejecutan automáticamente sin pedir confirmación al usuario. La 
  confirmación implícita está en la acción inicial.

- **Acción con ambigüedad real.** Cualquier acción donde el sistema no 
  puede inferir la intención del usuario sin preguntar (ej: clasificar 
  una nota suelta entre destello, tarea o referencia). **Por qué 
  importa:** según A5, estas acciones se resuelven con menús de 
  opciones cerradas, no con preguntas abiertas extensas.

---

## 8. Preguntas abiertas

Decisiones aún por tomar. Se anotan acá para no perderlas.

- ¿La sincronización automática de dependencias (A completada → B a 
  pendiente) requiere confirmación del usuario, o es automática? 
  (Heredada de `notas.md` → "Decisión abierta: ¿sincronización 
  automática requiere confirmar?")
- ¿Qué tecnología exacta soporta el script de sincronización: 
  Dataview JS, Templater, otra? (Heredada de `notas.md`.)
- ¿Cómo se archivan misiones/sub-misiones completadas sin romper las 
  queries de Dataview? (Heredada de `notas.md`.)
- ¿En qué momento Agatha reemplaza completamente a CardBoard, o 
  conviven indefinidamente?
- ¿La integración con IA es vía MCP, vía API directa, o vía un agente 
  embebido en la app?
