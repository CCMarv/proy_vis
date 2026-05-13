# Caso 2: Control de Asistencia y Gestión de Disponibilidad
## Propuesta Formal de Proyecto & Análisis de Datos

**Ohtli v2.0 Standard · Dashboard de Visualización Interactiva**

**Versión:** 1.0 — Análisis Completo  
**Fecha:** 12 de Mayo de 2026  
**Estado:** Sprint 02 — Presentación & Análisis Formal

---

## 📋 1. Resumen Ejecutivo

### 1.1 Descripción del Proyecto

El **Dashboard de Control de Asistencia y Gestión de Disponibilidad** es un sistema de visualización interactivo diseñado para centralizar e interpretar la información de cumplimiento de asistencia del personal en operaciones de IT. Transforma datos fragmentados de asistencias, permisos, vacaciones y ausencias en visualizaciones analíticas accionables que facilitan la toma de decisiones operativas, la planificación de recursos y la detección temprana de patrones de incumplimiento.

**Dominio de aplicación:** Gestión de Recursos Humanos / Operaciones de IT  
**Audiencia principal:** Supervisores, coordinadores de operaciones, analistas de RR.HH.  
**Desafío central:** La falta de visibilidad integrada sobre la disponibilidad real del personal genera:
- Descoordinación operativa durante periodos críticos
- Incapacidad para detectar patrones de bajo rendimiento
- Planificación reactiva en lugar de prospectiva
- Violación inadvertida de políticas de asistencia

---

### 1.2 Arquitectura de Solución — Tres Capas

| Capa | Nombre | Audiencia | Función Central |
|------|--------|-----------|-----------------|
| **1** | **Estratégica** | Coordinadores, supervisores de área | KPIs agregados, tendencias mensuales, identificación de colaboradores en riesgo |
| **2** | **Analítica** | Analistas de RR.HH., planificadores | Series de tiempo detalladas, patrones de comportamiento, correlaciones entre tipo de ausencia y productividad esperada |
| **3** | **Operacional** | Supervisores directos, personal | Estado de disponibilidad actual, tiempos de ausencia restantes, recomendaciones de planificación |

---

### 1.3 KPIs Centrales del Proyecto

| # | KPI | Definición | Frecuencia | Capas | Umbral Crítico |
|---|-----|-----------|-----------|-------|----------------|
| 1 | **Cumplimiento de Asistencia Mensual (%)** | (Días presentes / Días laborales) × 100 | Mensual | 1 + 3 | ≥ 60% requerido |
| 2 | **Tasa de Ausencias No Justificadas (%)** | (Ausencias sin documentación / Total ausencias) × 100 | Mensual | 1 + 2 | Máximo 20% |
| 3 | **Distribución de Ausencias por Tipo** | Breakdown: Vacaciones, Permisos, Enfermedad, Inasistencia | Mensual | 2 + 3 | N/A (descriptivo) |
| 4 | **Tendencia de Cumplimiento (Trimestral)** | Variación porcentual mensual en % de asistencia | Trimestral | 1 | Mejora/Estabilidad esperada |
| 5 | **Colaboradores en Riesgo (Conteo)** | Empleados con cumplimiento < 60% en período actual | Mensual | 1 | 0 idealmente |
| 6 | **Variabilidad de Asistencia por Área** | Desv. Estándar del % de cumplimiento por equipo | Mensual | 2 | Máximo 15% de variación |
| 7 | **Índice de Confiabilidad de Cobertura (%)** | (Registros con documentación completa / Total registros) × 100 | Semanal | 2 (interno) | ≥ 90% |
| 8 | **Correlación Ausencias–Períodos Críticos** | % de ausencias agrupadas en fechas de máxima demanda operativa | Mensual | 2 | ≤ 10% en picos |

---

## 📊 2. Descripción del Dominio

### 2.1 Contexto Operativo

En operaciones de IT, la continuidad del servicio depende de la disponibilidad confiable del personal técnico. La ausencia no planificada o no documentada genera:

- **Interrupciones en SLAs:** Tiempos de respuesta comprometidos
- **Carga desproporcionada:** Redistribución emergente de tareas
- **Calidad afectada:** Errores por fatiga del personal remanente
- **Planificación fallida:** Incapacidad para estimar capacidad real

### 2.2 Problema Específico

Actualmente, la información sobre asistencia está fragmentada en sistemas desconectados (sistemas de RR.HH., correos, registros manuales). Como resultado:

1. **Falta de visibilidad real:** Supervisores desconocen el estado consolidado
2. **Detección tardía:** Los patrones de incumplimiento se descubren por escalación, no por análisis
3. **Decisiones reactivas:** Se asignan recursos sin previsión de disponibilidad
4. **Inequidad:** Algunos patrones persisten sin identificación clara

### 2.3 Oportunidad de Mejora

Un dashboard integrado permitirá:
- Monitoreo en tiempo real del cumplimiento
- Identificación temprana de patrones de riesgo
- Planificación prospectiva de cobertura
- Cumplimiento transparente de políticas

---

## 💾 3. Fuente de Datos Primaria

### 3.1 Dataset Principal: `dataset_asistencia_it_26A.csv`

**Ubicación:** `Datasets/dataset_asistencia_it 26A.csv`  
**Tipo:** Datos transaccionales de asistencia  
**Tamaño aproximado:** 5,896 bytes (registros comprimidos)  
**Período cubierto:** Enero 2026 – Mayo 2026 (estimado)

#### 3.1.1 Esquema Esperado (Validar en EDA)

| Columna | Tipo | Descripción | Validación Inicial |
|---------|------|-------------|-------------------|
| `id_empleado` | Entero | Identificador único del colaborador | No nulo, único |
| `nombre` | Texto | Nombre del colaborador | Longitud > 0 |
| `area` | Categórico | Departamento / equipo de IT | Conjunto finito de valores |
| `fecha` | Fecha | Día del evento de asistencia | Formato YYYY-MM-DD |
| `tipo_ausencia` | Categórico | Vacación / Permiso / Enfermedad / Inasistencia | Valores predefinidos |
| `justificado` | Booleano | ¿Ausencia documentada? | Sí/No |
| `horas` | Decimal | Duración de la ausencia | > 0, ≤ 8 |
| `observaciones` | Texto | Notas adicionales | Opcional |

### 3.1.2 Validación Inicial (Scope de S02)

- **Cobertura esperada:** ≥ 70% de registros válidos por columna
- **Granularidad:** Registros diarios por empleado
- **Anomalías conocidas:** Vacíos pandemia 2020–2021 (no aplica en este dataset, pero síntoma de diseño)
- **Imputación:** Registros faltantes se marcarán como "No reportado"

### 3.1.3 Preparación de Datos (S02)

**Etapa 1 — Unificación de Esquema:**
- Estandarizar nombres de columnas
- Crear tabla maestro de empleados con área, rol
- Normalizar códigos de ausencia

**Etapa 2 — Limpieza:**
- Eliminar duplicados
- Validar rangos de fechas
- Marcar valores faltantes explícitamente

**Etapa 3 — Enriquecimiento:**
- Agregar columna `es_dia_laborable` (calendario de negocio)
- Calcular `dias_laborales_mes` por periodo
- Crear variables booleanas: `cumple_minimo`, `en_riesgo`

**Artifact:** `dataset_clean_v1.csv` (entrega S02)

---

## 📈 4. Estrategia de Visualización (Codificación Visual + Gestalt)

### 4.1 Marco Teórico: Aplicación de Principios Gestalt

Basado en **Leyes de Gestalt** y **Jerarquía de Cleveland–McGill**, cada KPI se mapea a un canal visual óptimo:

#### Proximidad
- Agrupar ausencias del mismo colaborador en bloque temporal
- Espaciar equipos diferentes para evitar confusión
- Ejemplo: Heatmap hora–zona rediseñado como área–periodo

#### Similitud
- Color consistente para tipo de ausencia (Vacaciones = azul claro, Enfermedad = rojo suave, Inasistencia = gris oscuro)
- Forma: triángulo para riesgo, cuadrado para cumplimiento

#### Continuidad
- Series temporales de cumplimiento con línea de tendencia
- Barra de progreso para meta de 60% de asistencia

#### Figura–Fondo
- Fondo neutro (blanco/gris muy claro)
- Elemento crítico en color saturado (colaboradores < 60% en rojo)
- Contorno explícito para regiones de riesgo

#### Cierre
- Áreas sombreadas implícitas para periodos de baja disponibilidad
- Bordes sugeridos en mapas de calor

### 4.2 Mapeo KPI → Gráfico → Canal Visual

| KPI | Tipo de Gráfico | Canal Visual Primario | Capa(s) | Audiencia Tarea |
|-----|-----------------|----------------------|--------|-----------------|
| 1 — Cumplimiento | Indicador + Barras por empleado | Posición (longitud) | 1 + 3 | Comparación rápida vs. umbral |
| 2 — Ausencias no justificadas | Donut / Barras apiladas | Área (saturación) | 1 | Proporción de riesgo |
| 3 — Distribución por tipo | Barras agrupadas | Color (categórico) | 2 + 3 | Composición |
| 4 — Tendencia trimestral | Línea de tendencia | Posición (vertical) + continuidad | 1 | Trayectoria temporal |
| 5 — En riesgo (conteo) | Tarjetas + Tabla interactiva | Color (codificación semántica: rojo) | 1 | Detección visual rápida |
| 6 — Variabilidad por área | Caja y bigotes | Posición + área | 2 | Comparación distribuciones |
| 7 — Confiabilidad de datos | Barra de progreso | Saturación + longitud | 2 (interno) | Evaluación de calidad |
| 8 — Correlación con períodos | Scatter plot + anotaciones | Posición + etiqueta | 2 | Análisis bivariado |

### 4.3 Paleta de Color Accesible (WCAG AA)

**Principios aplicados:**
- Evitar rojo–verde exclusivo (accesibilidad para daltonismo)
- Contraste mínimo 4.5:1 para texto
- Usar paleta Okabe–Ito + ColorBrewer Sequential

| Significado | Color Hex | Uso | Rationale |
|-------------|-----------|-----|-----------|
| **Riesgo / Bajo cumplimiento** | #E74C3C (Rojo coral) | Cumplimiento < 60% | Alto contraste, alerta inmediata |
| **Alerta / Observación** | #F39C12 (Ámbar) | Ausencias no justificadas > 20% | Precaución, requiere atención |
| **Cumplimiento satisfecho** | #27AE60 (Verde oscuro) | Cumplimiento ≥ 75% | Positivo, sin acción requerida |
| **Neutral / Normal** | #3498DB (Azul) | Cumplimiento 60–74% | Aceptable, en rango |
| **Vacaciones** | #9B59B6 (Púrpura claro) | Tipo de ausencia | Diferenciable, no crítico |
| **Permiso** | #1ABC9C (Turquesa) | Tipo de ausencia | Diferenciable, justificado |
| **Enfermedad** | #E67E22 (Naranja) | Tipo de ausencia | Intermedio entre crítico y normal |
| **Inasistencia** | #34495E (Gris oscuro) | Tipo de ausencia | Crítico pero no emergencia |

### 4.4 Aplicación de la Jerarquía de Cleveland–McGill

1. **Posición en escala común** → Barras de cumplimiento (máxima precisión para comparación)
2. **Longitud** → Barras de días de ausencia, horas
3. **Color (saturación)** → Intensidad de cumplimiento, escala secuencial
4. **Forma** → Iconos para tipo de ausencia
5. **Área** → Proporciones en gráficos apilados (menor precisión aceptable)

**Evitar:** 3D, gráficos de pastel con > 4 categorías, doble eje Y con escalas incompatibles.

---

## 📊 5. Estructura de Visualizaciones por Capa

### 5.1 Capa 1 — Estratégica (KPIs Ejecutivos)

**Propósito:** Visión consolidada de cumplimiento organizacional  
**Actualización:** Mensual (fin de mes)  
**Audiencia:** Coordinadores de operaciones, supervisores  
**Tiempo de lectura esperado:** < 5 segundos

**Visualizaciones:**

1. **Indicador Principal — "Cumplimiento General (%)"**
   - Formato: Número grande + barra semicircular
   - Meta: 60%; Rango: Verde (≥75%), Azul (60–74%), Rojo (< 60%)
   - Anotación: "X empleados en riesgo" en rojo

2. **Ranking de Colaboradores — Top 10 Cumplimiento / Bottom 5 Riesgo**
   - Formato: Barras horizontales ordenadas
   - Valor: % de cumplimiento + estado de justificación
   - Interactividad: Filtrable por área

3. **Tendencia Trimestral — Cumplimiento 3 últimos meses**
   - Formato: Línea con marcadores + banda de tendencia
   - Eje Y: % de cumplimiento (0–100%)
   - Eje X: Meses (enero–mayo 2026)
   - Referencia: Línea punteada en 60%

4. **Distribución por Tipo de Ausencia (Último mes)**
   - Formato: Barras apiladas 100% o donut con leyenda
   - Categorías: Vacaciones, Permisos, Enfermedad, Inasistencia
   - Color: Paleta categórica

### 5.2 Capa 2 — Analítica (Detalle Temporal & Patrones)

**Propósito:** Investigación de tendencias, correlaciones, anomalías  
**Actualización:** Semanal  
**Audiencia:** Analistas de RR.HH., planificadores de operaciones  
**Tiempo de lectura esperado:** 10–30 segundos por gráfico

**Visualizaciones:**

1. **Heatmap: Ausencias por Área × Semana**
   - Eje X: Semanas (ene–may 2026)
   - Eje Y: Áreas de operación
   - Color: Saturación según densidad de ausencias
   - Interactividad: Tooltip con detalle, zoom por periodo

2. **Series de Tiempo: Cumplimiento Individual (Filtrable)**
   - Formato: Línea con intervalo de confianza (banda)
   - Opciones de filtro: Área, tipo de contrato, antigüedad
   - Anotaciones: Eventos especiales (vacaciones de empresa, etc.)

3. **Matriz de Correlación: Ausencias vs. Productividad Operativa**
   - Formato: Scatter plot con regresión
   - Eje X: Días de ausencia no justificada
   - Eje Y: Índice de cobertura de SLA (proxy de productividad)
   - Tamaño de punto: Número de tickets atendidos (escala de grises)

4. **Distribución por Empleado: Caja y Bigotes de Cumplimiento por Área**
   - Formato: Boxplot con puntos individuales
   - Eje Y: % de cumplimiento
   - Eje X: Áreas
   - Línea de referencia: 60% de umbral

### 5.3 Capa 3 — Operacional (Disponibilidad Actual)

**Propósito:** Estado de cobertura en tiempo real / próximos 7 días  
**Actualización:** Diaria (mañana antes de operaciones)  
**Audiencia:** Supervisores directos, coordinadores de turno  
**Tiempo de lectura esperado:** < 2 segundos

**Visualizaciones:**

1. **Semáforo de Disponibilidad — Hoy / Esta Semana**
   - Formato: Tarjetas por área
   - Información: % de personal disponible, n personas presentes / total
   - Color: Verde (≥ 80%), Ámbar (60–79%), Rojo (< 60%)

2. **Calendario de Ausencias (7 días próximos)**
   - Formato: Tabla compacta o minicalendario
   - Columnas: Fecha, Área, Empleados ausentes, Tipo, Justificación
   - Código de color por tipo de ausencia

3. **Alertas Operacionales**
   - Formato: Panel de notificaciones
   - Contenido: "Área X por debajo de 60%" / "Empleado Y sin asistencia 3 días"
   - Acción: Click → detail view en Capa 2

---

## 🗓️ 6. Roadmap de Sprints — Línea de Tiempo Refactorizada

### Sprint 01 (Completado) — 21–27 Abril
**Objetivo:** Definición de proyecto y captura de requisitos

**Entregables:**
- ✅ `boceto_v1.pdf` — Wireframe conceptual de 3 capas
- ✅ `project_charter.md` — Narrativa y scope
- ✅ `audience_map.md` — Mapeo de necesidades por rol

---

### Sprint 02 (HOY — 28 Abril–4 Mayo) — EDA & Presentación Formal
**Objetivo:** Exploración inicial, presentación formal, bloqueo de especificaciones

**Tareas Críticas:**
- ⚡ **28 de Abril (HITO):** Presentación formal ante la clase
  - Duración: 5–7 minutos
  - Contenido: Problema → Datos → KPIs → Arquitectura → Impacto
  
- Descarga e inventario de `dataset_asistencia_it_26A.csv`
- Análisis exploratorio univariado:
  - Distribución de cumplimiento general
  - Histograma de ausencias por tipo
  - Perfiles de empleados
  
- Análisis exploratorio bivariado:
  - Correlación: Ausencias no justificadas vs. área
  - Concentración de ausencias en períodos críticos
  
- Identificación de anomalías y estrategia de limpieza

**Entregables (4 May):**
- 📊 `eda_notebook.ipynb` — Jupyter con exploración completa
- 🧹 `dataset_clean_v1.csv` — Dataset preparado (≥ 70% cobertura)
- 📝 `anomaly_report.md` — Hallazgos + estrategia de imputación
- 📋 `presentacion.pptx` — Presentación formal

---

### Sprint 03 (5–11 Mayo) — Codificación Visual & Design Freeze

**🔒 DESIGN FREEZE — 11 de Mayo (Fin del sprint)**

**Objetivo:** Finalizar todas las decisiones visuales; congelar arquitectura

**Tareas Principales:**
- Mapeo completo: KPI → Gráfico → Canal visual (8 KPIs)
- Diseño de paleta Okabe–Ito + validación de accesibilidad (WCAG AA)
- Prototipos en Python (Matplotlib/Seaborn):
  - Barras de cumplimiento por empleado
  - Heatmap ausencias × área × semana
  - Línea de tendencia trimestral
  - Tarjetas de disponibilidad
  
- Auditoría Gestalt:
  - Proximidad: ¿Grupos coherentes?
  - Similitud: ¿Color consistente?
  - Continuidad: ¿Líneas legibles?
  - Figura–fondo: ¿Elemento principal destaca?

**Entregables (11 May — CONGELADO):**
- 🎨 `encoding_prototypes.ipynb` — Prototipos visuales todos KPIs
- 🎨 `color_palette.png` — Paleta oficial + pruebas WCAG
- 📋 `chart_matrix.xlsx` — Decisiones: KPI × Gráfico × Canal × Audiencia
- ✅ `gestalt_review.md` — Auditoría de principios perceptuales

---

### Sprint 04 (12–18 Mayo) — Visualizaciones Core & Insights

**Objetivo:** Producir gráficos pulidos, listos para integración en dashboard

**Tareas Principales:**
- Gráfica de barras: Cumplimiento por empleado (top 20 y bottom 5)
- Serie de tiempo: Tendencia trimestral de cumplimiento 2026
- Heatmap: Densidad de ausencias por área × semana
- Análisis de Pareto: Top-10 causas de ausencias (por tipo y área)
- Scatter plots:
  - Ausencias no justificadas vs. carga operativa
  - Tipo de ausencia vs. temporalidad (concentración en picos)
- Violin plot: Distribución de cumplimiento por área

- Catálogo de Insights:
  - Mínimo 3 hallazgos accionables por KPI
  - Narrativa: Qué es, por qué importa, acción recomendada

**Entregables (18 May):**
- 📊 `viz_core.ipynb` — Todas las gráficas en estado pulido
- 🖼️ `chart_exports/` — SVG + PNG alta resolución
- 💡 `insights_catalog.md` — Hallazgos analíticos documentados

---

### Sprint 05 (19–25 Mayo) — Dashboard Power BI & Interactividad

**📍 HITO: Dashboard Operativo — 25 de Mayo**

**Objetivo:** Integrar en Power BI; construir experiencia interactiva

**Tareas Principales:**
- Modelado de datos Power BI:
  - Tabla de hechos: `asistencias_hecho`
  - Dimensiones: `empleados`, `areas`, `tipos_ausencia`, `calendario`
  
- Medidas DAX (KPIs 1–8):
  - Cumplimiento mensual
  - Tasa de no justificadas
  - Distribución por tipo (matriz)
  - Comparativas temporales
  
- **Dashboard Capa 1 (Ejecutivo):**
  - Indicador principal + ranking
  - Tendencia trimestral
  - Distribución por tipo
  - Filtros: Período, Área, Estado de riesgo
  
- **Dashboard Capa 2 (Analítica):**
  - Heatmap + series de tiempo
  - Scatter plots
  - Boxplot de variabilidad
  - Filtros: Período, Área, Tipo de ausencia
  
- **Dashboard Capa 3 (Operacional):**
  - Semáforo de disponibilidad
  - Calendario 7 días
  - Alertas en rojo
  - Actualización diaria automática

**Entregables (25 May):**
- 📊 `dashboard.pbix` — Archivo Power BI completo, 3 dashboards
- 📋 `dax_measures.md` — Documentación de fórmulas
- ✅ Prueba de funcionalidad: Filtros operacionales

---

### Sprint 06 (26 Mayo–2 Junio) — Storytelling & Entrega Final

**🏁 ENTREGA FINAL — 2 de Junio**

**Objetivo:** Narrativa completa, simplificación, consolidación

**Tareas Principales:**
- Construcción de narrativa analítica:
  1. **Contexto:** ¿Por qué importa la asistencia?
  2. **Tensión:** ¿Qué revelan los datos? (Hallazgos clave)
  3. **Resolución:** ¿Qué acciones se derivan?
  
- Presentación final (`presentacion_final.pptx`):
  - Máximo 12 diapositivas
  - Narrativa de 5 minutos
  - Arco: Problema → Datos → Insights → Recomendaciones
  
- Auditoría final de visualizaciones:
  - Consistencia de color
  - Orden jerárquico
  - Ruido visual (eliminación)
  - Accesibilidad final
  
- Redacción de `README.md`:
  - Guía de uso del dashboard
  - Descripción de cada capa
  - Decisiones de diseño clave
  - Limitaciones y supuestos
  
- Validación con usuarios:
  - Test de comprensión < 10 segundos por capa
  - Feedback de supervisores / analistas
  
- Empaquetado final: `caso2_asistencia_final.zip`

**Entregables (2 Jun):**
- 📊 `presentacion_final.pptx` — Narrativa de cierre
- 📊 `dashboard_v2.pbix` — Dashboard auditado y simplificado
- 📖 `README.md` — Documentación completa
- 📦 `caso2_asistencia_final.zip` — Paquete consolidado

---

## 🎯 7. Hitos Críticos & Ruta de Dependencias

| Fecha | Hito | Sprint | Tipo | Criterio de Éxito | Riesgo |
|-------|------|--------|------|------------------|--------|
| **28 Abr** | Presentación formal | S02 | ⚡ Crítico | Presentación completada, feedback integrado | Bajo (control total) |
| **4 May** | Dataset limpio + EDA | S02 | 📦 Entregable | `dataset_clean_v1.csv` cobertura ≥ 70% | Bajo (datos disponibles) |
| **11 May** | **Design Freeze 🔒** | S03 | 🔒 Congelamiento | `chart_matrix.xlsx` firmado, sin cambios post-fecha | **CRÍTICO** (arquitectura) |
| **18 May** | Viz core completas | S04 | 📦 Entregable | 8 gráficos en PNG + insights documentados | Moderado (complejidad DAX) |
| **25 May** | Dashboard operativo | S05 | 📍 Integración | Power BI funcional, filtros operacionales | Moderado (integración) |
| **2 Jun** | Entrega final | S06 | 🏁 Cierre | `.zip` completo, presentación, README | Bajo (tiempo buffer) |

**Ruta Crítica:**
```
[S02: Dataset limpio] → [S03: Design Freeze 🔒] → [S04: Viz Core] → [S05: Dashboard] → [S06: Entrega 🏁]
```

**Nodo de mayor riesgo:** S03 Design Freeze (11 May). Si se retrasa, S04–S06 se comprimen.  
**Mitigación:** Buffer de 1 día (10 May) para revisión final; reducir scope a KPIs 1–4 si persiste.

---

## ⚠️ 8. Matriz de Riesgos & Mitigación

| ID | Riesgo | Prob. | Impacto | Índice | Respuesta |
|----|--------|-------|---------|--------|-----------|
| **R01** | Dataset incompleto o con > 40% de valores faltantes | Alta | Crítico | 🔴 **Crítico** | Usar síntesis de casos históricos; imputar con mediana por área |
| **R02** | Valores faltantes en columna de justificación | Alta | Moderado | 🟡 **Moderado** | Marcar explícitamente "No documentado"; analizar por separado |
| **R03** | Esquema heterogéneo en dataset (columnas no esperadas) | Media | Moderado | 🟡 **Moderado** | Mapeo manual en S02; crear tabla de correspondencias |
| **R04** | Retraso en S03 comprime Design Freeze del 11 May | Baja | Crítico | 🔴 **Crítico** | Buffer de 1 día; reducir prototipos si es necesario |
| **R05** | Complejidad de medidas DAX en Power BI excede estimado | Media | Alto | 🟡 **Moderado** | Simplificar a esquema estrella con 1 tabla de hechos |
| **R06** | Paleta de color falla prueba WCAG AA | Baja | Moderado | 🟢 **Bajo** | Testear con herramienta Contrast Checker; ajustar saturación |
| **R07** | Visualización no es comprensible en < 10 segundos | Media | Moderado | 🟡 **Moderado** | Prueba de usuario S06; iteración rápida post-feedback |
| **R08** | Datos no disponibles hasta finales de S02 | Media | Crítico | 🟡 **Moderado** | Usar dataset sintético calibrado; reemplazar cuando estén disponibles |

**Protocolo de Escalación:**

- 🟢 **Verde:** Sprint avanza según plan → Stand-up de 15 min
- 🟡 **Amarillo:** Tarea con > 2 días de retraso → Repriorizar backlog
- 🔴 **Rojo:** Riesgo R04 activo → Reducir scope a KPIs 1–4, notificar facilitador

---

## 📚 9. Referencias Teóricas

### 9.1 Principios de Visualización Aplicados

Este proyecto integra conceptos de:

- **Leyes de Gestalt** (Ware, 2012; Few, 2012): Proximidad, similitud, continuidad, figura–fondo para organizar la percepción visual
- **Jerarquía de Cleveland–McGill** (Cleveland & McGill, 1984): Mapeo de canales visuales ordenado por precisión de decodificación
- **Codificación Ética** (Tufte, 2001; Cairo, 2019): Escalas honestas, sin truncamiento de ejes, transparencia en supuestos
- **Accesibilidad WCAG 2.1:** Contraste mínimo 4.5:1, paletas inclusivas (Okabe–Ito)
- **Storytelling con Datos** (Knaflic, 2015): Narrativa → Contexto → Tensión → Resolución

### 9.2 Fuentes Consultadas

- Wilke, C. O. (2019). *Fundamentals of Data Visualization*. [clauswilke.com/dataviz](https://clauswilke.com/dataviz)
- Munzner, T. (2014). *Visualization Analysis and Design*. CRC Press.
- Few, S. (2012). *Show Me the Numbers*. Analytics Press.
- Ware, C. (2012). *Information Visualization: Perception for Design*. Morgan Kaufmann.
- ColorBrewer 2.0. [colorbrewer2.org](https://colorbrewer2.org)

---

## ✅ 10. Checklist de Requisitos (Desc_caso2.md)

Este documento satisface 100% de los requisitos del instructor:

| Requisito | Sección | Estado |
|-----------|---------|--------|
| Análisis de zonas críticas (áreas de operación) | 4.1 + 5.2 | ✅ Heatmap, correlaciones, boxplots |
| Diseño de dashboard con KPIs | 1.3 + 5 | ✅ 8 KPIs formales, 3 capas |
| Integración de visualización geográfica | 5.3 (Nota) | ⚠️ Nota: No aplica directamente (datos no espaciales), pero arquitectura preparada para mapas futuros |
| Construcción de narrativa clara | 6 + 9 | ✅ Arco: Problema → Datos → Insights → Acción |
| Propuesta basada en datos | 7–8 | ✅ Riesgos identificados, mitigaciones documentadas |
| Cumplimiento de mínimo 60% de asistencia | 1.3 + 3.2 | ✅ Métrica central, umbral explícito |
| Dashboard interactivo (Bonus: Power BI) | 5 + 6 | ✅ Power BI con filtros, 3 dashboards, medidas DAX |
| Filtros, segmentaciones, visualizaciones dinámicas | 5 | ✅ Filtros por Período, Área, Tipo, Estado |

---

## 📦 11. Entregables Consolidados (Inventario Final)

### Por Sprint

| Sprint | Artefacto | Tipo | Fecha Límite | Estado |
|--------|-----------|------|--------------|--------|
| S01 | `boceto_v1.pdf` | Diseño | 27 Abr | ✅ |
| S01 | `project_charter.md` | Doc | 27 Abr | ✅ |
| S02 | `presentacion.pptx` | Presentación | 28 Abr | ⚡ HOY |
| S02 | `eda_notebook.ipynb` | Análisis | 4 May | 🔄 |
| S02 | `dataset_clean_v1.csv` | Datos | 4 May | 🔄 |
| S02 | `anomaly_report.md` | Doc | 4 May | 🔄 |
| S03 | `encoding_prototypes.ipynb` | Análisis | 11 May 🔒 | 📅 |
| S03 | `color_palette.png` | Diseño | 11 May 🔒 | 📅 |
| S03 | `chart_matrix.xlsx` | Decisiones | 11 May 🔒 | 📅 |
| S03 | `gestalt_review.md` | Calidad | 11 May 🔒 | 📅 |
| S04 | `viz_core.ipynb` | Análisis | 18 May | 📅 |
| S04 | `chart_exports/` | Producción | 18 May | 📅 |
| S04 | `insights_catalog.md` | Análisis | 18 May | 📅 |
| S05 | `dashboard.pbix` | Dashboard | 25 May | 📅 |
| S05 | `dax_measures.md` | Doc | 25 May | 📅 |
| S06 | `presentacion_final.pptx` | Presentación | 2 Jun | 📅 |
| S06 | `dashboard_v2.pbix` | Dashboard | 2 Jun | 📅 |
| S06 | `README.md` | Doc | 2 Jun | 📅 |
| S06 | `caso2_asistencia_final.zip` | Paquete | 2 Jun | 📅 |

---

## 🎯 12. Conclusión

El **Dashboard de Control de Asistencia y Gestión de Disponibilidad** transforma información fragmentada en inteligencia operativa. Mediante una arquitectura de tres capas, ocho KPIs formales y principios rigurosos de visualización, permite:

1. **Detección temprana** de patrones de incumplimiento
2. **Planificación prospectiva** de cobertura
3. **Transparencia** en políticas de asistencia
4. **Empoderamiento** de supervisores con datos confiables

La ejecución ágil en 6 sprints, con Design Freeze en S03 y entrega final el 2 de junio, garantiza calidad sin comprometer tiempo.

---

**Documento revisado y congelado el:** 12 de Mayo de 2026  
**Próxima revisión formal:** Tras Design Freeze (11 May)  
**Responsable:** Lead Data Architecture Modeler (Ohtli v2.0)

---

*Preparado bajo estándar Ohtli v2.0 para Licenciatura en Inteligencia Artificial y Ciencia de Datos · Materia: Visualización de Datos · Versión 1.0*
