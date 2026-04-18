# 🧪 Prueba v2 — Modelo unificado con pesos

Esta es la versión refinada de la prueba anterior, con el modelo que propusiste:

## Cambios vs. la v1 (`app-enterbase-2/`)

- **Todas las tareas son .md individuales**, tanto las ligeras como las pesadas (antes había dos formatos distintos).
- **Campo `peso` 1/2/3** en el frontmatter para clasificar la naturaleza de cada tarea.
- **Emoji de color al INICIO de la tarea** en la línea de CardBoard para identificar el peso de un vistazo: 🟡 (1), 🟣 (2), 🟠 (3). Va al inicio porque CardBoard trunca los textos largos — si el emoji va al final, desaparece cuando el texto es largo.
- **Carpeta `_plantillas/`** con una plantilla copiable para cuando quieras crear tareas manualmente.

## Estructura

```
v2-unificado/
├── _plantillas/
│   └── plantilla-tarea.md                  ← Copia esto cuando crees tareas manualmente
├── app-enterbase/                           ← MISIÓN
│   ├── _aclarador.md
│   ├── formulario-matriculados/             ← SUB-MISIÓN
│   │   ├── _aclarador.md
│   │   ├── 01-generar-doc-bd.md             ← peso 3 🟠
│   │   ├── 02-esperar-aprobacion-bruno.md   ← peso 2 🟣
│   │   └── 03-deploy-produccion.md          ← peso 3 🟠
│   └── tareas-sueltas/                      ← Tareas de la misión que no pertenecen a una sub-misión
│       ├── revisar-backup.md                ← peso 1 🟡
│       └── limpiar-logs-staging.md          ← peso 1 🟡
```

## Escala de pesos

| Peso | Emoji | Naturaleza | Ejemplos |
|---|---|---|---|
| **1** | 🟡 | Aislada y rápida. Una acción, sin dependencias ni subtareas. Una sesión corta. | Enviar mensaje, limpiar logs, confirmar algo |
| **2** | 🟣 | Aislada pero requiere tiempo o pensamiento. Una sola cosa pero más profunda. | Investigar un tema, leer un manual, diseñar algo simple |
| **3** | 🟠 | Compleja. Subtareas, dependencias, o naturaleza impredecible. | Implementar una feature, hacer un deploy, coordinar algo con varias personas |

## Qué probar

1. Mira el tablero CardBoard — debería listar las 5 tareas (3 del formulario + 2 sueltas).
2. Fíjate si el emoji de color se ve claramente al escanear el tablero.
3. Dale click al lápiz de varias tareas y revisa cómo se ve la estructura (Detalle, Contexto IA, Notas, Tarea).
4. Compara una tarea peso-1 (ej. `revisar-backup.md`) vs peso-3 (ej. `03-deploy-produccion.md`) — ¿sientes la diferencia visual?
5. Revisa `_plantillas/plantilla-tarea.md` — ¿te serviría copiar eso cuando quieras crear manualmente?
