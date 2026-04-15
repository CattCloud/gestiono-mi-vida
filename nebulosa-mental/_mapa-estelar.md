# 🌫️ Mapa estelar — Nebulosa Mental

Lo que anda disperso y necesita ser procesado.

---

## Destellos pendientes

```dataview
TASK
FROM "nebulosa-mental"
WHERE !completed
SORT text ASC
```

## ✅ Resueltos recientemente

```dataview
TASK
FROM "nebulosa-mental"
WHERE completed
SORT text ASC
```

---

> **Revisión semanal:** Revisa cada destello y decide — ¿se mueve a un planeta? ¿se convierte en misión? ¿se descarta?
