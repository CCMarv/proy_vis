# Proyecto de Visualización de Datos

Repositorio de trabajo para el curso de Visualización de Datos. El proyecto está en una fase de exploración dual: actualmente se desarrollan dos propuestas de caso en paralelo y más adelante se hará *lock in* para continuar solo con una de ellas.

Este README funciona como una introducción rápida al repositorio y como guía de contexto para usar su contenido como entrada de modelos LLM.

## Estado actual

- Se mantienen dos líneas de trabajo: **Caso 1** y **Caso 2**.
- Ambos casos cuentan con una descripción base en `Descripcion/` y una propuesta desarrollada en la raíz del proyecto.
- La carpeta `Ref/` contiene un proyecto parcialmente desarrollado que sirve como **referencia de diseño, estructura y metodología**.
- El proyecto final se consolidará en **un solo caso** cuando se complete el proceso de selección.

## Organización del proyecto

```text
Proyecto/
├── Datasets/
│   └── Archivos fuente y datasets de trabajo del proyecto.
├── Descripcion/
│   ├── Desc_caso1.md
│   │   └── Consigna y contexto del Caso 1.
│   ├── Desc_caso2.md
│   │   └── Consigna y contexto del Caso 2.
│   ├── Caso1.md
│   │   └── Desarrollo del análisis, narrativa y propuesta del Caso 1.
│   └── Caso2.md
│       └── Desarrollo del análisis, narrativa y propuesta del Caso 2.
├── Docs/
│   └── visualizacion_datos_notas.md
│       └── Notas teóricas y de referencia sobre visualización de datos.
├── Preeliminares/
│   └── Material preliminar, borradores o apoyos de exploración.
├── Ref/
│   ├── README.md
│   ├── INDICE_VISUAL.md
│   ├── SECCION_REFERENCIA_RAPIDA.md
│   └── planDeProyecto.html
│       └── Proyecto de referencia parcial que guía la estructura y el estilo del trabajo.
└── README.md
    └── Este archivo.
```

## Función de cada carpeta

### `Datasets/`
Contiene los archivos de datos que alimentan los análisis. Es la fuente primaria para construir métricas, tablas, visualizaciones y narrativas.

### `Descripcion/`
Reúne la consigna de cada caso y su versión desarrollada. Los archivos `Desc_caso*.md` funcionan como brief; los archivos `Caso*.md` funcionan como entrega analítica.

### `Docs/`
Incluye notas, referencias conceptuales y material de apoyo teórico para redactar y justificar decisiones de visualización.

### `Preeliminares/`
Espacio para exploración temprana, pruebas, bocetos o material de trabajo que todavía no forma parte de la entrega final.

### `Ref/`
Contiene un proyecto parcialmente construido que sirve como base de referencia. Su función es orientar la forma de organizar el trabajo, la narrativa y la presentación, no reemplazar el caso final.

## Uso del proyecto como entrada para LLMs

Este repositorio está pensado para ser usado como contexto de generación, edición o revisión con modelos de lenguaje. Para evitar ambigüedad, sigue este orden de lectura:

1. `README.md` para entender el estado general del proyecto.
2. `Descripcion/Desc_caso1.md` o `Descripcion/Desc_caso2.md` según el caso activo.
3. `Descripcion/Caso1.md` o `Descripcion/Caso2.md` para ver la propuesta ya desarrollada.
4. `Docs/visualizacion_datos_notas.md` para reforzar criterios de visualización.
5. `Ref/` para tomar estructura, estilo y flujo de presentación como referencia.

### Recomendación para prompts de LLM

Cuando uses este repositorio como input, especifica siempre:

- Qué caso está activo.
- Qué archivo es la fuente de la consigna.
- Qué archivo es la propuesta desarrollada.
- Si el objetivo es resumir, reescribir, comparar o extender contenido.

Eso evita que el modelo mezcle el Caso 1 con el Caso 2 antes del *lock in*.

## Flujo de trabajo esperado

1. Revisar la consigna del caso en `Descripcion/`.
2. Analizar el dataset correspondiente en `Datasets/`.
3. Redactar la propuesta en `Caso1.md` o `Caso2.md`.
4. Usar `Ref/` como guía de estructura y presentación.
5. Consolidar una sola línea de trabajo cuando se defina el caso final.

## Referencia rápida de archivos principales

- `Descripcion/Desc_caso1.md` y `Descripcion/Desc_caso2.md`: instrucciones base.
- `Descripcion/Caso1.md` y `Descripcion/Caso2.md`: desarrollo del análisis.
- `Ref/planDeProyecto.html`: plan de referencia con estructura navegable.
- `Ref/README.md`: visión general del proyecto de referencia.
- `Ref/INDICE_VISUAL.md`: mapa de navegación del material de referencia.
- `Ref/SECCION_REFERENCIA_RAPIDA.md`: resumen operativo de lectura rápida.
- `Docs/visualizacion_datos_notas.md`: soporte teórico y conceptual.

## Nota sobre el lock in

El repositorio todavía mantiene dos propuestas activas. El objetivo intermedio es documentar ambas con suficiente claridad para compararlas. Después del lock in, este README puede actualizarse para reflejar únicamente el caso seleccionado y simplificar la estructura de trabajo.

## Resultado esperado

Al usar este repositorio como contexto de trabajo, un LLM debe poder identificar rápidamente:

- cuál es el problema a resolver,
- qué archivos contienen la consigna,
- qué archivos contienen la propuesta,
- qué material sirve de referencia,
- y en qué punto del proceso se encuentra el proyecto.
