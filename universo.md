# 🌌 Universo

Vista global de todo lo que tengo pendiente, en todos los planetas.

---

## Hoy

```dataview
TASK
FROM "enter-tech-school" OR "mis-proyectos-dev" OR "mis-sistemas-identidad" OR "nebulosa-mental"
WHERE !completed AND due = date(today)
SORT text ASC
```

## Esta semana

```dataview
TASK
FROM "enter-tech-school" OR "mis-proyectos-dev" OR "mis-sistemas-identidad" OR "nebulosa-mental"
WHERE !completed AND due >= date(today) AND due <= date(today) + dur(7 days)
SORT due ASC
```

---

## 🪐 Enter Tech School

```dataview
TASK
FROM "enter-tech-school"
WHERE !completed
SORT due ASC
```

## 🪐 Mis Proyectos Dev

```dataview
TASK
FROM "mis-proyectos-dev"
WHERE !completed
SORT due ASC
```

## 🪐 Mis Sistemas de Identidad

```dataview
TASK
FROM "mis-sistemas-identidad"
WHERE !completed
SORT due ASC
```

## 🌫️ Nebulosa Mental

```dataview
TASK
FROM "nebulosa-mental"
WHERE !completed
SORT text ASC
```

---

## ⏳ Esperando respuesta

```dataview
TASK
FROM "enter-tech-school" OR "mis-proyectos-dev" OR "mis-sistemas-identidad" OR "nebulosa-mental"
WHERE !completed AND contains(text, "⏳")
SORT text ASC
```
