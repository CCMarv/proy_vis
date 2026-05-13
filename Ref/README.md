# Plan de Proyecto — Dashboard de Movilidad Urbana ZMG

**Documento de Gestión Ágil · Versión 1.0 · Mayo 2026**

## 📋 Descripción

Este archivo contiene el **Plan de Proyecto Completo** del Dashboard de Movilidad Urbana de la Zona Metropolitana de Guadalajara. Es un sistema de visualización de tres capas diseñado para transformar datos fragmentados de tráfico, calidad del aire y siniestralidad vial en inteligencia accionable.

---

## 🎯 Estructura del Proyecto

El plan está organizado en **5 secciones principales** identificadas por navegación menú:

### 1. **Resumen Ejecutivo** 📋
- Descripción general del proyecto
- Arquitectura de solución (3 capas)
- KPIs centrales (8 métricas clave)
- Stack tecnológico

### 2. **Roadmap de Sprints** 🚀
- **Sprint 1** (21–27 Abr): Definición del proyecto ✅ COMPLETADO
- **Sprint 2** (28 Abr–4 May): EDA & Presentación Formal ⚠️ SPRINT ACTIVO
- **Sprint 3** (5–11 May): Diseño de Codificación Visual
- **Sprint 4** (12–18 May): Visualizaciones Core
- **Sprint 5** (19–25 May): Dashboard & Mapas Interactivos
- **Sprint 6** (26 May–2 Jun): Storytelling & Entrega Final

### 3. **Tabla de Hitos y Ruta Crítica** 📍
- Gantt visual por sprint
- Tabla de hitos críticos
- Ruta crítica del proyecto
- Identificación de nodos de riesgo

### 4. **Estrategia de Mitigación de Riesgos** ⚠️
- Matriz de 8 riesgos identificados
- Probabilidad e impacto de cada riesgo
- Estrategia ETL por fases
- Protocolo de escalación (Verde → Amarillo → Rojo)

### 5. **Inventario Completo de Artefactos** 📦
- Tabla de todos los entregables por sprint
- Tipos de artefactos: Diseño, Documentación, Análisis, Dashboard, etc.
- Fechas límite de entrega

---

## 🔑 Elementos Clave

### Las 3 Capas del Dashboard

| Capa | Nombre | Audiencia | Función |
|------|--------|-----------|---------|
| **1** | Estratégica | Ayuntamiento, SEMOV, SITEUR | KPIs agregados, mapas coropléticos |
| **2** | Analítica | Planificadores urbanos, equipo académico | Series de tiempo, heatmaps, correlaciones |
| **3** | Operacional/Ciudadana | Población general | Semáforo de congestión, tiempos de traslado |

### Los 8 KPIs Centrales

1. Volumen de Tráfico (veh/30 min)
2. Demora en Hora Pico (min adicionales)
3. ICA — NO₂ / PM₂.₅ (µg/m³ / IMECA)
4. Tasa de Siniestros Viales
5. Tiempo de Traslado en Corredores
6. Distribución Pico / Valle
7. Velocidad Media de Circulación
8. Índice de Cobertura de Datos

---

## ⚡ Hitos Críticos

| Fecha | Hito | Estado |
|-------|------|--------|
| **21 Abr** | Entrega de boceto inicial | ✅ Completado |
| **28 Abr** | Presentación formal | ⚡ CRÍTICO |
| **11 May** | Design Freeze 🔒 | Congelamiento de decisiones |
| **25 May** | Dashboard operativo | 📍 Integración |
| **2 Jun** | Entrega final | 🏁 Cierre |

---

## 📂 Archivos Relacionados

Este proyecto se desarrolla con los siguientes artefactos principales:

- **Notebooks**: `eda_notebook.ipynb`, `encoding_prototypes.ipynb`, `viz_core.ipynb`
- **Dashboard**: `dashboard.pbix`, `dashboard_v2.pbix` (Power BI)
- **Mapa**: `mapa_interactivo.html` (Folium/Mapbox)
- **Datasets**: `dataset_clean_v1.csv`
- **Documentación**: `project_charter.md`, `anomaly_report.md`, `README.md`

---

## 🚀 Cómo Usar Este Documento

1. **Abre `planDeProyecto.html`** en tu navegador web
2. Usa el **menú de navegación superior** para saltar entre secciones
3. Cada sección incluye:
   - Descripción clara del objetivo
   - Tablas detalladas con tareas y entregables
   - Indicadores visuales (emojis) para identificar estados
   - Referencias cruzadas entre sprints

---

## ⚠️ Nodos de Riesgo Críticos

1. **R01**: Disponibilidad de datos SEMOV
   - Mitiga con: Dataset sintético basado en INEGI OD 2022

2. **R04**: Retraso en Design Freeze (11 May)
   - Mitiga con: Buffer de 1 día, reducir scope si es necesario

3. **R07**: Complejidad del modelo DAX en Power BI
   - Mitiga con: Esquema estrella simplificado

---

## 📧 Contacto

**Proyecto**: Dashboard de Movilidad Urbana ZMG  
**Materia**: Visualización de Datos 2025–2026  
**Versión del Plan**: 1.0 · Mayo 2026

---

**Última actualización**: Mayo 2026

