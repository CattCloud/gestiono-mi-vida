# 🪐 Mapa estelar — Mis Proyectos Dev

Todo lo que estoy construyendo por mi cuenta.

---

## Misiones activas

(Aún no hay misiones activas.)

---

## Tareas pendientes

```dataview
TASK
FROM "mis-proyectos-dev"
WHERE !completed
SORT due ASC
```

## ⏳ Esperando algo

```dataview
TASK
FROM "mis-proyectos-dev"
WHERE !completed AND contains(text, "⏳")
SORT text ASC
```

## ✅ Completadas recientemente

```dataview
TASK
FROM "mis-proyectos-dev"
WHERE completed
SORT text ASC
```
