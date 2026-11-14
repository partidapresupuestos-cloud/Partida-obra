# Instrucciones para Claude

## Elección automática de modelo

El usuario ha pedido que se elija el modelo automáticamente según la dificultad de la tarea, para gastar menos. Al delegar trabajo en subagentes (herramienta Agent), fija el parámetro `model` así:

- `haiku`: tareas sencillas y mecánicas. Búsquedas en el código, leer y resumir archivos, cambios de texto o de estilo, renombrados, comprobaciones simples.
- `sonnet`: tareas normales. Funciones nuevas acotadas, corrección de errores localizados, pruebas, refactorizaciones pequeñas.
- Modelo principal de la sesión (sin delegar): tareas difíciles. Diseño, errores complicados, cambios que tocan muchas partes, decisiones con riesgo.

Reglas:

- Si la tarea es tan pequeña que se resuelve en una o dos llamadas, hazla directamente: arrancar un subagente cuesta más que el ahorro.
- Al delegar, pasa al subagente todo el contexto que necesita (archivos, objetivo, criterio de terminado), porque empieza de cero.
- Revisa el resultado del subagente antes de darlo por bueno.
- Si un modelo barato falla o deja el resultado a medias, repite con el siguiente nivel en lugar de insistir.
