# 🪐 Mapa estelar — Enter Tech School

Todo lo que está pasando en mi trabajo.

---

## Misiones activas

- [[app-enterbase]]
- [[instructor-code101n20]]

---

## Tareas pendientes

```dataview
TASK
FROM "enter-tech-school"
WHERE !completed
SORT due ASC
```

## ⏳ Esperando respuesta

```dataview
TASK
FROM "enter-tech-school"
WHERE !completed AND contains(text, "⏳")
SORT text ASC
```

## ✅ Completadas recientemente

```dataview
TASK
FROM "enter-tech-school"
WHERE completed
SORT text ASC
```
