# Guía de instalación de plugins

> Sigue este orden. Cada paso se hace uno a la vez.
> Después de instalar cada plugin, verifica que funcione antes de pasar al siguiente.

---

## Paso 0: Activar plugins de la comunidad

Si aún no lo has hecho:

1. Abre Obsidian → **Configuración** (⚙️ abajo a la izquierda)
2. Ve a **Plugins de la comunidad**
3. Clic en **Activar plugins de la comunidad**
4. Confirma

---

## Paso 1: Tema Minimal + Style Settings

### 1a. Instalar tema Minimal

1. Configuración → **Apariencia** → **Temas** → **Administrar**
2. Busca **"Minimal"** (autor: Kepano)
3. Clic en **Instalar y usar**
4. El vault debería cambiar de aspecto inmediatamente — más limpio, tipografía más elegante

### 1b. Instalar Style Settings

1. Configuración → **Plugins de la comunidad** → **Explorar**
2. Busca **"Style Settings"**
3. **Instalar** → **Activar**
4. Ahora en Configuración verás una nueva sección **"Style Settings"** donde puedes personalizar colores, fuentes, checkboxes, etc.

**Verificación:** Abre cualquier archivo .md — debería verse con el nuevo tema. Las checkboxes deberían verse mejor.

---

## Paso 2: Dataview

1. Configuración → **Plugins de la comunidad** → **Explorar**
2. Busca **"Dataview"** (autor: Michael Brenan)
3. **Instalar** → **Activar**

**Verificación:** Abre `universo.md` o cualquier `_mapa-estelar.md`. Las secciones que antes mostraban texto plano ahora deberían renderizar las tareas como listas vivas.

**Configuración recomendada** (opcional):
- En Configuración → Dataview → activa **"Enable JavaScript Queries"** (por si necesitamos queries más avanzadas en el futuro)
- En Configuración → Dataview → activa **"Enable Inline Queries"** (para queries inline en el texto)

---

## Paso 3: Desinstalar plugin Tasks (si lo tienes instalado)

1. Configuración → **Plugins de la comunidad**
2. Busca **Tasks** en la lista de plugins instalados
3. **Desactivar** → **Desinstalar**

Ya no lo necesitas. Dataview cubre todo lo que hacía y más.

---

## Paso 4: CardBoard (Kanban)

1. Configuración → **Plugins de la comunidad** → **Explorar**
2. Busca **"CardBoard"** (autor: roovo)
3. **Instalar** → **Activar**

**Configuración inicial:**
1. Abre la paleta de comandos (Ctrl+P)
2. Escribe **"CardBoard"** y selecciona **"CardBoard: Open Board"**
3. Se abrirá un tablero. Clic en **"Add Board"** para crear tu primer tablero
4. Configura el tablero:
   - **Nombre:** "Enter Tech School" (o el que quieras)
   - **Tipo:** "Tag Based" o "Date Based" según prefieras
   - **Tags/Folders:** Apúntalo a la carpeta `enter-tech-school`

**Verificación:** Deberías ver las tareas de `app-enterbase.md` como tarjetas en el tablero.

---

## Paso 5: Full Calendar

1. Configuración → **Plugins de la comunidad** → **Explorar**
2. Busca **"Full Calendar"** (autor: Davis Haupt)
3. **Instalar** → **Activar**

**Configuración inicial:**
1. Abre la paleta de comandos (Ctrl+P)
2. Escribe **"Full Calendar"** y selecciona **"Full Calendar: Open calendar"**
3. Se abrirá una vista de calendario
4. En la configuración del plugin, añade una fuente de eventos apuntando a tus archivos del vault

**Verificación:** Las tareas con fecha `📅 YYYY-MM-DD` deberían aparecer en el calendario en su día correspondiente.

---

## Paso 6: Google Calendar (último)

> Este es el más complejo de configurar. Tómate tu tiempo.

1. Configuración → **Plugins de la comunidad** → **Explorar**
2. Busca **"Google Calendar"** (autor: YukiGasai)
3. **Instalar** → **Activar**

**Configuración (requiere cuenta de Google):**

1. Ve a [Google Cloud Console](https://console.cloud.google.com/)
2. Crea un proyecto nuevo (o usa uno existente)
3. Activa la **Google Calendar API**
4. Crea credenciales OAuth 2.0:
   - Tipo: Aplicación de escritorio
   - Descarga el archivo JSON de credenciales
5. En Obsidian → Configuración → Google Calendar:
   - Pega el Client ID y Client Secret de las credenciales
   - Sigue el flujo de autenticación que te aparece
6. Una vez autenticado, abre la paleta de comandos y busca **"Google Calendar"** para ver las opciones

**Verificación:** Deberías ver tus eventos de Google Calendar (incluyendo los que vienen de ClickUp) dentro de Obsidian.

**Nota:** Si este paso te resulta complicado, puedes dejarlo para después. El vault funciona perfectamente sin él. Cuando lo necesites, el agente IA puede guiarte con más detalle.

---

## Resumen final

| Orden | Plugin | Estado después de instalar |
|---|---|---|
| 1 | Minimal + Style Settings | El vault se ve profesional |
| 2 | Dataview | Los dashboards muestran tareas vivas |
| 3 | ~~Tasks~~ (desinstalar) | Ya no se necesita |
| 4 | CardBoard | Tienes tablero Kanban |
| 5 | Full Calendar | Tienes vista calendario de tareas |
| 6 | Google Calendar | Ves tu calendario del trabajo en Obsidian |

---

> Si algo no funciona o te trabas en algún paso, abre un chat con el agente IA y descríbele el error. Puede ayudarte a resolverlo.
