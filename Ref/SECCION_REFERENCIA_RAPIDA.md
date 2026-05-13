# 📌 Referencia Rápida — Las 5 Secciones del Plan

## 🎯 SECCIÓN 1: RESUMEN EJECUTIVO

**Inicio en**: [planDeProyecto.html#seccion-1](planDeProyecto.html#seccion-1)

### Contenido
- **Descripción del Proyecto**: Sistema de visualización de 3 capas para movilidad urbana ZMG
- **Arquitectura**:
  - Capa 1 (Estratégica): Gobierno municipal
  - Capa 2 (Analítica): Planificadores y académicos
  - Capa 3 (Ciudadana): Población general
- **8 KPIs Principales**: Tráfico, demora, calidad del aire, siniestros, tiempos de traslado, velocidad, cobertura
- **Stack Tecnológico**: Python, R, Power BI, Folium/Mapbox

### Duración lectora: ~10 minutos

---

## 🚀 SECCIÓN 2: ROADMAP DE SPRINTS

**Inicio en**: [planDeProyecto.html#seccion-2](planDeProyecto.html#seccion-2)

### Contenido de los 6 Sprints

| Sprint | Fechas | Estado | Objetivo Principal |
|--------|--------|--------|-------------------|
| **S01** | 21–27 Abr | ✅ Completado | Arquitectura y boceto |
| **S02** | 28 Abr–4 May | ⚠️ Activo | EDA + Presentación (28 Abr) |
| **S03** | 5–11 May | ⏳ Próximo | Design Freeze (11 May) 🔒 |
| **S04** | 12–18 May | ⏳ Próximo | Visualizaciones core |
| **S05** | 19–25 May | ⏳ Próximo | Dashboard + Mapa interactivo |
| **S06** | 26 May–2 Jun | ⏳ Final | Storytelling y entrega |

### Cada sprint incluye
- Backlog detallado de tareas con esfuerzo (horas)
- Dependencias entre tareas
- Entregables específicos con nombres de archivos
- Definición de Done (DoD) con criterios de calidad

### Duración lectora: ~20 minutos

---

## 📍 SECCIÓN 3: TABLA DE HITOS Y RUTA CRÍTICA

**Inicio en**: [planDeProyecto.html#seccion-3](planDeProyecto.html#seccion-3)

### Contenido
- **Gantt Visual**: Timeline de los 6 sprints
- **Hitos Críticos** (6 principales):
  - 21 Abr: Boceto inicial ✅
  - 28 Abr: Presentación formal ⚡
  - 4 May: Dataset limpio 📦
  - 11 May: Design Freeze 🔒 (MÁS CRÍTICO)
  - 25 May: Dashboard operativo 📍
  - 2 Jun: Entrega final 🏁

### Ruta Crítica Identificada
```
[S01: Arquitectura] → [S02: Dataset] → [S03: FREEZE] → [S04: Viz] → [S05: Dashboard] → [S06: Entrega]
```

### 3 Nodos de Mayor Riesgo
1. Disponibilidad de datos SEMOV en S02
2. **Design Freeze del 11 de mayo** (punto de congelamiento)
3. Complejidad del modelo DAX en Power BI (S05)

### Duración lectora: ~8 minutos

---

## ⚠️ SECCIÓN 4: ESTRATEGIA DE MITIGACIÓN DE RIESGOS

**Inicio en**: [planDeProyecto.html#seccion-4](planDeProyecto.html#seccion-4)

### Contenido
- **8 Riesgos Identificados** con matriz de probabilidad e impacto

| ID | Riesgo | Crítica | Mitiga con |
|----|--------|---------|-----------|
| R01 | Datos SEMOV no disponibles | 🔴 Crítico | Dataset sintético INEGI OD 2022 |
| R02 | Vacíos pandemia 2020–2021 | 🟡 Moderado | Imputación con mediana 2019 |
| R03 | APIs Google/Waze fuera de alcance | 🟡 Moderado | OSM + INEGI OD; limitar RT |
| R04 | Retraso en Design Freeze | 🔴 Crítico | Buffer 1 día; reducir scope |
| R05 | Latencia SINAICA > 24h | 🟡 Moderado | Históricos 2023–24 |
| R06 | Falla sensores SEMOV/SCT | 🟡 Moderado | Umbral ETL: <40%=eliminar; >40%=imputar |
| R07 | DAX complexity exceeds estimate | 🟡 Moderado | Esquema estrella simple |
| R08 | Video C5 requiere procesamiento IA | 🟢 Bajo | Excluir del scope |

### Estrategia ETL por Fases
1. **Etapa 1** (S02): Unificación de esquema → `schema_master_v1.xlsx`
2. **Etapa 2** (S03–S04): Validación y limpieza con thresholds
3. **Etapa 3** (S04–S06): Recolección paralela (Waze, C5)

### Protocolo de Escalación
- 🟢 **Verde**: Sprint normal → Stand-up diario
- 🟡 **Amarillo**: Tarea >2 días retraso → Repriorizar
- 🔴 **Rojo**: Design Freeze en peligro → Reducir scope KPIs 1–4

### Duración lectora: ~12 minutos

---

## 📦 SECCIÓN 5: INVENTARIO COMPLETO DE ARTEFACTOS

**Inicio en**: [planDeProyecto.html#seccion-5](planDeProyecto.html#seccion-5)

### Contenido
- **24 Artefactos totales** organizados por sprint y tipo

#### Por Sprint

**S01 (Completado)**:
- `boceto_v1.pdf` (Diseño)
- `project_charter.md` (Documentación)
- `audience_map` (Diseño)
- `kpi_matrix_v1.xlsx` (Datos)

**S02 (Activo)**:
- `presentacion.pptx` (Presentación) — 28 Abr ⚡
- `eda_notebook.ipynb` (Análisis)
- `dataset_clean_v1.csv` (Datos)
- `anomaly_report.md` (Documentación)

**S03 (Próximo)**:
- `encoding_prototypes.ipynb` (Análisis)
- `color_palette.png` (Diseño)
- `chart_matrix.xlsx` (Decisiones)
- `gestalt_review.md` (Calidad)

**S04**:
- `viz_core.ipynb` (Análisis)
- `chart_exports/` (Producción SVG+PNG)
- `insights_catalog.md` (Análisis)

**S05**:
- `dashboard.pbix` (Dashboard Power BI)
- `mapa_interactivo.html` (Mapa Folium)
- `dax_measures.md` (Documentación)

**S06 (Final)**:
- `presentacion_final.pptx` (Presentación)
- `dashboard_v2.pbix` (Dashboard v2)
- `README.md` (Documentación completa)
- `proyecto_zmg_movilidad_final.zip` (Entrega final)

#### Por Tipo
- **Análisis**: 5 notebooks
- **Dashboards**: 2 archivos Power BI
- **Diseño**: 4 artefactos
- **Documentación**: 6 archivos
- **Producción**: 1 carpeta
- **Datos**: 2 archivos

### Duración lectora: ~10 minutos

---

## 💡 Cómo Navegar Este Plan

### Opción 1: Lectura Rápida (20 min)
1. Revisa esta página de referencia
2. Mira la Sección 3 (Hitos)
3. Consulta Sección 5 (Artefactos) para saber qué va en cada fecha

### Opción 2: Revisión Completa (60 min)
1. Secciones 1-2: Entender proyecto y sprints
2. Sección 3: Ruta crítica e hitos
3. Sección 4: Riesgos y mitigación
4. Sección 5: Inventario de artefactos

### Opción 3: Consulta por Sprint
- S01 ✅: Ya completado. Ver resultados en artefactos.
- S02 ⚠️: Focus en Presentación (28 Abr) y Dataset limpio (4 May)
- S03: El **Design Freeze (11 May)** es el punto más crítico
- S04–S06: Continuar según ruta

---

## 🔑 Puntos Clave a Recordar

### ⚡ CRÍTICO
- **28 de Abril**: Presentación formal ante la clase
- **11 de Mayo**: Design Freeze 🔒 — Sin cambios arquitecturales después
- **2 de Junio**: Entrega final 🏁

### ⚠️ Riesgos Mayores
- R04: Retraso en Design Freeze (buffer de 1 día)
- R01: Disponibilidad de datos SEMOV

### 📊 Los 3 Pilares
1. **Arquitectura**: 3 capas de visualización
2. **Datos**: 8 KPIs con fuentes diversas
3. **Narrativa**: Arco desde evento hasta solución

---

## 📄 Documento Completo

**Archivo principal**: `planDeProyecto.html`

**Versión**: 1.0 · Mayo 2026

**Materia**: Visualización de Datos 2025–2026

**Proyecto**: Dashboard de Movilidad Urbana ZMG

---

**Última actualización**: Mayo 2026

