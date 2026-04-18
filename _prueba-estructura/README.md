# 🧪 Prueba de estructura A1

Esta carpeta es un sandbox para probar la nueva estructura propuesta antes de migrar todo el vault. **No toca tus misiones reales.**

## Lo que estás viendo aquí

Simulé cómo se vería tu misión `app-enterbase` con el nuevo modelo de 4 niveles:

```
_prueba-estructura/                        ← (carpeta de prueba, ignorar después)
└── app-enterbase/                          ← 🎯 MISIÓN (antes: archivo .md)
    ├── _aclarador.md                       ← Contexto general de la misión
    ├── tarea-ligera-ejemplo.md             ← Tareas que no necesitan .md propio
    └── formulario-matriculados/            ← 🎯 SUB-MISIÓN
        ├── _aclarador.md                   ← Contexto de la sub-misión
        ├── 01-generar-doc-bd.md            ← 🎯 TAREA PESADA (.md individual)
        ├── 02-esperar-aprobacion-bruno.md  ← 🎯 TAREA PESADA
        └── 03-deploy-produccion.md         ← 🎯 TAREA PESADA
```

## Qué probar en CardBoard

1. Abre el tablero CardBoard
2. Fíjate si aparecen las 3 tareas pesadas del formulario
3. Dale click al lápiz de una de ellas — debería abrirte el `.md` individual (no un archivo gigante mezclado)
4. Revisa el detalle, contexto y notas en ese archivo — así es como se vería una tarea autocontenida
5. Marca una como completada y ve qué pasa

## Qué NO está incluido aún

- La automatización del flujo secuencial (eso lo discutimos después — saber qué pasa cuando marcas la 01)
- El skill actualizado para manejar este modelo (también después)

Esto es solo un **esqueleto visual** para que valides el formato.

---

**Si te gusta cómo se ve:** lo pulimos y migramos todo el vault.
**Si no te convence:** lo borramos y probamos otra cosa. Cero compromiso.
