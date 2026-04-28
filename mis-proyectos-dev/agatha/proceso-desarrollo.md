---
tags:
  - mis-proyectos-dev
  - agatha
  - proceso-desarrollo
tipo: documento-proceso
---

# 🗺️ Proceso de Desarrollo — Agatha

> Documento operativo. Registra **dónde estamos** en el proceso de 
> planeación y desarrollo de Agatha, qué se trabajó en cada sesión, y 
> cuál es el próximo paso.
>
> **Audiencia:** el usuario (para abrirlo y saber el estado), cualquier 
> agente IA que entre al proyecto (incluido Claude Code cuando llegue 
> a implementar), y yo del futuro entre sesiones.
>
> **Mantenimiento:** el agente IA actualiza este archivo al final de 
> cada sesión de planeación o desarrollo. El usuario no tiene que 
> tocarlo — solo abrirlo cuando quiera saber dónde está el proyecto.

---

## 📍 Estado actual

**Fase:** Planeación.
**Etapa actual:** Etapa 2 — Mapear uso actual del sistema de gestión.
**Próximo paso:** El usuario llena `etapa-2-uso-actual.md` a su ritmo. 
Cuando avise, el agente procesa las respuestas y arma los casos de uso 
para la §5 Casos de uso reales del documento `vision-producto.md`.

**Última sesión:** 2026-04-25 — Cierre de Etapa 1 + apertura de Etapa 2.

---

## 🛤️ Mapa de las 5 etapas de planeación

El proceso de planeación está dividido en 5 etapas. Cada etapa tiene un 
propósito claro y un entregable concreto en `vision-producto.md` o en 
documentos auxiliares.

### Etapa 1 — Aterrizar la visión
- **Propósito:** Definir el norte del producto.
- **Entregables:** §1 Visión, §6 Anti-objetivos, §7 Glosario en 
  `vision-producto.md`.
- **Estado:** ✅ Cerrada el 2026-04-25.

### Etapa 2 — Mapear uso actual
- **Propósito:** Documentar cómo el usuario realmente usa el sistema 
  hoy (CardBoard, Obsidian, chat, captura). Sin suponer nada.
- **Entregables:** Documento auxiliar `etapa-2-uso-actual.md` con las 
  respuestas del usuario + §5 Casos de uso reales en 
  `vision-producto.md` con los casos formalizados.
- **Estado:** 🔄 En curso desde el 2026-04-25.

### Etapa 3 — Definir features del MVP
- **Propósito:** Convertir los casos de uso en una lista priorizada de 
  features. Solo entran al MVP las features que resuelven casos de uso 
  documentados en Etapa 2.
- **Entregables:** Documento auxiliar `etapa-3-features.md` con lista 
  priorizada (indispensable / importante / nice-to-have).
- **Estado:** ⏸️ Pendiente.

### Etapa 4 — Diseñar la experiencia
- **Propósito:** Bocetar cómo se ve y se siente Agatha antes de que 
  Claude Code escriba una línea de código. Puede ser dibujo en papel, 
  prosa descriptiva, mockups simples — lo que sirva.
- **Entregables:** Documento auxiliar `etapa-4-diseno.md` + posibles 
  imágenes/bocetos en `etapa-4-diseno/` si se generan.
- **Estado:** ⏸️ Pendiente.

### Etapa 5 — Brief de implementación para Claude Code
- **Propósito:** Convertir todo lo anterior en un documento ejecutable 
  por Claude Code, dividido en fases (qué construir primero, qué 
  después).
- **Entregables:** Documento auxiliar `etapa-5-brief-implementacion.md`.
- **Estado:** ⏸️ Pendiente.

---

## 📚 Bitácora de sesiones

Lista cronológica de todas las sesiones de planeación. Última al final.

### 2026-04-25 — Sesión 1

**Duración aproximada:** Larga (sesión continua de varias rondas).
**Modalidad:** Chat con agente IA en Cowork.

**Qué se trabajó:**
- Procesamiento inicial de las 6 mejoras pendientes en `notas.md`.
- Decisión de construir un Kanban propio en lugar de mejorar CardBoard.
- Decisión de ampliar el alcance a "plataforma personal unificada" en 
  lugar de solo un Kanban.
- Decisión de darle nombre propio al sistema: **Agatha**.
- Creación de la misión `mis-proyectos-dev/agatha/` con su `_aclarador.md`.
- Creación del documento vivo `vision-producto.md` con estructura de 
  8 secciones.
- **Etapa 1 completa:** §1 Visión, §6 Anti-objetivos (8 anti-objetivos 
  en 3 categorías), §7 Glosario (referencia + términos propios).
- Creación de este documento `proceso-desarrollo.md` para mantener 
  continuidad entre sesiones.
- Apertura de Etapa 2 con creación de `etapa-2-uso-actual.md` 
  (formulario para que el usuario llene a su ritmo).

**Qué se decidió:** 9 decisiones registradas en §4 de `vision-producto.md`. 
Las más importantes:
- Agatha es entidad unificada (datos + vistas + IA).
- Agatha se construye con cariño, no con exigencia.
- El Kanban es la primera vista, no el todo.
- Implementación a cargo de Claude Code en fase posterior.

**Qué quedó pendiente:**
- Etapa 2 abierta: el usuario llena `etapa-2-uso-actual.md` a su ritmo.
- Borrado manual de carpeta vieja `mi-kanban/` por parte del usuario 
  (ya completado por el usuario antes de cerrar la sesión).

**Aprendizajes capturados:** El usuario prefiere menús cerrados sobre 
preguntas abiertas extensas en flujos operativos. Anotado en memoria 
de feedback (`feedback_estilo.md`) y reflejado en el anti-objetivo A5 
de Agatha.

---

## 🧭 Cómo retomar el proceso (si vuelves después de un tiempo)

Si abres este proyecto después de varios días o entras como agente 
nuevo, sigue estos pasos para reincorporarte sin perder contexto:

1. Lee este archivo entero — te dice dónde estás.
2. Lee `_aclarador.md` de la misión Agatha — te da el contexto general.
3. Lee `vision-producto.md` — es la fuente de verdad sobre qué es 
   Agatha y qué se decidió.
4. Si hay un documento `etapa-N-*.md` activo según el estado de arriba, 
   léelo también.
5. Mira la última entrada de la bitácora — sabrás qué pasó la última vez.
6. Mira el "Próximo paso" arriba — sabrás por dónde seguir.
