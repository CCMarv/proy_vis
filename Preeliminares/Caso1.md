# Caso 1: Mejora de la vialidad en la Zona Metropolitana de Guadalajara

## Contexto del problema
La Zona Metropolitana de Guadalajara enfrenta un problema de movilidad urbana que no depende de una sola causa, sino de una combinación de incidentes operativos, climáticos y de infraestructura. El objetivo de este análisis es identificar patrones relevantes en el dataset proporcionado para ubicar zonas críticas, detectar horarios de mayor impacto y proponer una solución orientada a mejorar la sincronización semafórica y reducir la congestión.

## Descripción del dataset
El archivo contiene 500 registros distribuidos en una sola hoja (`Sheet1`) y 12 columnas:

`ID_Reporte`, `Fecha`, `Zona`, `Tipo_Incidente`, `Severidad`, `Tiempo_Retraso_Min`, `Estado`, `Latitud`, `Longitud`, `Hora`, `Clima`, `Fuente`.

El periodo analizado corresponde a abril de 2026 y el dataset incluye variables suficientes para estudiar incidencia temporal, espacial y operativa.

## Hallazgos principales

### 1. Zonas con mayor incidencia
Las zonas con más registros son:

| Zona | Incidentes |
|---|---:|
| Tonalá | 137 |
| Zapopan | 130 |
| Centro | 123 |
| Tlaquepaque | 110 |

Tonalá concentra la mayor cantidad de reportes, mientras que Tlaquepaque destaca por presentar el mayor retraso promedio, lo que sugiere una afectación operativa más intensa aunque con menor volumen relativo de eventos.

### 2. Tipos de incidentes más frecuentes
Los eventos con mayor presencia son:

| Tipo de incidente | Frecuencia |
|---|---:|
| Accidentes | 58 |
| Semáforos descompuestos | 55 |
| Congestión por evento | 54 |

Los semáforos descompuestos y la congestión por eventos generan además los mayores retrasos promedio, por lo que son factores prioritarios para intervención.

### 3. Horarios críticos
Las horas con más incidentes son:

| Hora | Incidentes |
|---|---:|
| 20:00 | 38 |
| 15:00 | 38 |
| 13:00 | 37 |

Esto muestra una concentración de problemas en horas de alta demanda: salida laboral, flujo escolar y franja nocturna con eventos, retorno y desplazamientos de última hora.

### 4. Retrasos en la movilidad
El retraso promedio general es de **61.42 minutos**, con un máximo de **120 minutos**.

Por tipo de incidente, los mayores retrasos se observan en:

| Tipo de incidente | Retraso promedio (min) |
|---|---:|
| Semáforos descompuestos | 68.2 |
| Congestión por evento | 66.8 |

La severidad media presenta el mayor retraso promedio (**65.2 min**), seguida de la alta (**60.6 min**). Esto sugiere que algunos incidentes de impacto operativo sostenido no siempre están clasificados como los más graves al momento del reporte.

### 5. Condición climática
La distribución del clima en los reportes es relativamente equilibrada:

| Clima | Registros | Retraso promedio (min) |
|---|---:|---:|
| Lluvia | 175 | 60.8 |
| Soleado | 164 | 62.7 |
| Nublado | 161 | 60.7 |

Aunque la lluvia es una condición crítica por naturaleza, en este dataset el retraso promedio no se dispara de forma marcada respecto a otros climas. Esto sugiere que el problema principal está más relacionado con fallas de control vial y saturación que con el clima por sí solo.

## Interpretación de los patrones
1. La mayor presión vial se concentra en zonas de alta actividad urbana y corredores de conexión.
2. Los semáforos descompuestos y la congestión por eventos son los incidentes con mayor impacto real sobre el tiempo de viaje.
3. Las horas pico muestran que el problema se agrava cuando coinciden alta demanda y fallas operativas.
4. El clima influye, pero no explica por sí mismo el nivel de congestión observado.
5. La combinación de semáforos defectuosos, accidentes y eventos urbanos apunta a un problema sistémico de coordinación y respuesta.

## Diseño propuesto de dashboard
El dashboard debe ser interactivo y orientado a la toma de decisiones. Se recomienda incluir:

### KPIs principales
- Total de reportes
- Retraso promedio
- Retraso máximo
- Zonas críticas activas
- Incidentes por tipo
- Incidentes por hora pico

### Visualizaciones clave
- Tarjetas KPI con métricas principales.
- Gráfica de barras para comparar tipos de incidentes.
- Serie temporal para observar variación por fecha y hora.
- Mapa geográfico con puntos por latitud y longitud.
- Matriz o heatmap por zona y hora para detectar acumulación de incidencias.
- Segmentadores por zona, clima, severidad y estado.

### Filtros sugeridos
- Zona
- Tipo de incidente
- Clima
- Severidad
- Estado
- Franja horaria

## Representación geográfica
Con las coordenadas disponibles, se puede construir un mapa de incidentes para identificar concentraciones espaciales. La visualización geográfica debe permitir:

- Detectar corredores con saturación recurrente.
- Ubicar nodos semafóricos que generan mayor retraso.
- Comparar zonas con alta frecuencia vs. zonas con mayor impacto.
- Priorizar intervenciones en tramos donde coinciden accidentes, semáforos descompuestos y congestión por eventos.

Como visualización conceptual, el mapa debería usar marcadores con color por severidad y tamaño por retraso, para que los puntos críticos destaquen con claridad.

## Narrativa de datos
La movilidad en la ZMG no solo está afectada por el volumen de vehículos, sino por la capacidad del sistema para responder en tiempo real. Los datos muestran que el problema se intensifica cuando coinciden:

- fallas de semáforos,
- accidentes,
- eventos masivos,
- y horas de máxima demanda.

En otras palabras, la congestión no aparece de forma aislada: se amplifica cuando un incidente menor no se atiende rápido o cuando la infraestructura vial no está sincronizada. El efecto es acumulativo y termina generando retrasos superiores a una hora en promedio.

## Propuesta de solución
Se propone una estrategia de mejora basada en datos para optimizar la sincronización semafórica y reducir la congestión:

1. **Priorizar semáforos críticos** en las zonas con mayor retraso y frecuencia de incidentes.
2. **Crear un tablero operativo en tiempo real** para monitorear fallas, accidentes y eventos.
3. **Ajustar ciclos semafóricos por franja horaria** usando patrones de demanda detectados en el análisis.
4. **Integrar alertas por clima y eventos** para anticipar incrementos de congestión.
5. **Definir rutas y nodos de atención rápida** para incidentes recurrentes.
6. **Coordinar tránsito y movilidad urbana** en corredores clave para reducir tiempos de respuesta.

## Conclusión
El dataset confirma que la vialidad en Guadalajara está determinada por una interacción entre infraestructura deficiente, saturación urbana e incidentes operativos. Tonalá, Zapopan, Centro y Tlaquepaque presentan una carga relevante de eventos, pero los mayores retrasos se asocian con semáforos descompuestos y congestión por eventos. La mejor respuesta no es únicamente ampliar vías, sino mejorar el control del flujo mediante sincronización semafórica, monitoreo geográfico y análisis continuo de datos.

## Entregables recomendados
- Documento de análisis en Markdown o Word.
- Dashboard interactivo en Power BI o herramienta similar.
- Mapa de incidentes con coordenadas.
- Exportación a PDF o PNG para la presentación final.
