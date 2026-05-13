# Caso 2: Control de asistencia y gestión de disponibilidad

## Contexto del problema
En una oficina de IT, la continuidad del servicio depende directamente de la disponibilidad del personal. Cuando no existe visibilidad suficiente sobre asistencia, permisos, trabajo remoto y vacaciones, se complica la planeación de turnos, la asignación de tareas críticas y la cobertura de incidencias. Esto puede traducirse en retrasos operativos, sobrecarga en ciertos colaboradores y riesgo en el cumplimiento de SLA.

El objetivo de este análisis es identificar patrones de asistencia, detectar colaboradores en riesgo y proponer una forma clara de monitorear la disponibilidad del equipo para apoyar la toma de decisiones del supervisor.

## Descripción del dataset
El archivo contiene **100 registros** y **10 columnas**:

`ID_Empleado`, `Nombre`, `Area`, `Dias_Laborables_Mes`, `Dias_Asistidos`, `Dias_Remotos`, `Dias_Permiso`, `Vacaciones_Disponibles`, `Fecha_Expiracion_Vacaciones`, `Estatus`.

El análisis se centra en el cumplimiento del mínimo requerido de asistencia mensual, definido como **60%**.

## Hallazgos principales

### 1. Resumen general de asistencia
La asistencia promedio general del equipo es de **72.68%**, por encima del mínimo requerido; sin embargo, el comportamiento no es homogéneo entre áreas ni entre colaboradores.

### 2. Zonas o áreas con mayor riesgo
La distribución promedio de asistencia por área es la siguiente:

| Área | Asistencia promedio |
|---|---:|
| DevOps | 77.13% |
| Security | 75.84% |
| Networking | 72.31% |
| IT Support | 65.91% |

**IT Support** es el área con menor asistencia promedio y, por tanto, la más expuesta a riesgos de cobertura operativa. Aunque su promedio sigue por encima del umbral, está más cerca del límite y concentra más casos problemáticos.

### 3. Colaboradores en riesgo
Se identificaron **31 empleados** con asistencia inferior al **60%**, lo que representa una proporción importante del total.

Casos especialmente críticos:

| Colaborador | Área | Asistencia |
|---|---|---:|
| Carlos Salas | IT Support | 36.36% |
| Mariana Salas | DevOps | 36.36% |
| Ana Salas | IT Support | 36.36% |
| Gabriela Romero | IT Support | 36.36% |
| Laura Pineda | DevOps | 36.36% |

Estos casos requieren seguimiento inmediato porque pueden afectar la cobertura de tickets, la continuidad del soporte y la distribución de carga de trabajo.

### 4. Distribución por estatus
El personal se distribuye de la siguiente forma:

| Estatus | Registros |
|---|---:|
| Activo | 39 |
| Permiso | 37 |
| Vacaciones | 24 |

La proporción de permisos y vacaciones es alta, por lo que el tablero debe permitir distinguir claramente entre disponibilidad real y ausencia programada.

### 5. Factores que influyen en la disponibilidad
Promedios mensuales observados:

| Indicador | Promedio |
|---|---:|
| Días de permiso | 3.87 |
| Días remotos | 3.10 |
| Vacaciones disponibles | 8.62 |

El volumen de permisos y el trabajo remoto influyen en la presencia física del personal. Esto no necesariamente representa una baja productividad, pero sí puede afectar la capacidad de respuesta si no se planifica con anticipación.

## Interpretación de los patrones
1. La asistencia promedio general es aceptable, pero existen colaboradores y áreas con riesgo operativo real.
2. IT Support es la zona más sensible porque combina menor asistencia con alta necesidad de cobertura.
3. El grupo de colaboradores por debajo del 60% sugiere una posible concentración de ausencias o una distribución desigual de cargas y permisos.
4. Los permisos y vacaciones deben tratarse como variables de planeación, no solo como ausencias aisladas.
5. Un tablero de seguimiento mensual permitiría anticipar faltas de cobertura antes de que impacten a la operación.

## Diseño propuesto de dashboard
El dashboard debe mostrar el estado de asistencia de forma clara y operativa. Se recomienda incluir:

### KPIs principales
- Total de colaboradores
- Asistencia promedio general
- Número de colaboradores bajo 60%
- Área con menor asistencia
- Días de permiso promedio
- Días remotos promedio
- Vacaciones disponibles promedio

### Visualizaciones clave
- Tarjetas KPI con indicadores principales.
- Barras horizontales por área para comparar el porcentaje de asistencia.
- Tabla de colaboradores en riesgo con semáforo de alertas.
- Gráfica de distribución por estatus.
- Segmentadores por área, estatus y nivel de asistencia.

### Filtros sugeridos
- Área
- Estatus
- Nivel de riesgo
- Rango de asistencia
- Disponibilidad de vacaciones

## Identificación de colaboradores en riesgo
Se recomienda clasificar a los empleados en tres niveles:

- **Riesgo alto:** menos de 60% de asistencia.
- **Riesgo medio:** entre 60% y 70%.
- **Riesgo bajo:** más de 70%.

Esta segmentación facilitaría priorizar la atención sobre los casos más críticos y distinguir entre un problema puntual y una tendencia sostenida.

## Narrativa de datos
La operación del equipo no depende solo de cuántas personas están activas, sino de cuándo y cómo están disponibles. El dataset muestra que la asistencia global es razonable, pero no uniforme. Hay áreas con mejor estabilidad, como DevOps y Security, y otras con una exposición mayor al incumplimiento, como IT Support.

Además, una parte significativa del personal se encuentra entre permisos y vacaciones, lo que obliga a planear con anticipación para no dejar áreas sin cobertura. La información de asistencia, permisos y remotos debe leerse en conjunto para evitar decisiones reactivas.

## Propuesta de mejora
Se propone una estrategia de control basada en datos para optimizar la gestión de asistencia:

1. **Monitoreo mensual automático** del cumplimiento de asistencia por colaborador y por área.
2. **Alertas tempranas** cuando un empleado baje del 60% o se acerque al umbral.
3. **Planeación de cobertura por área**, especialmente en IT Support.
4. **Control de permisos y vacaciones** con visión anticipada para evitar acumulación en periodos críticos.
5. **Tablero ejecutivo para supervisión** con filtros dinámicos y actualización periódica.
6. **Clasificación de riesgo** para priorizar seguimiento individual y evitar impacto en SLA.

## Conclusión
El análisis confirma que la asistencia del equipo se mantiene, en promedio, por encima del mínimo requerido; sin embargo, existe un grupo relevante de colaboradores en riesgo que puede comprometer la operación si no se atiende a tiempo. IT Support destaca como el área más vulnerable, por lo que conviene reforzar la planeación de turnos, el seguimiento de permisos y el control de disponibilidad.

## Entregables recomendados
- Documento de análisis en Markdown o Word.
- Dashboard interactivo en Power BI o herramienta similar.
- Tabla de riesgo de colaboradores.
- Exportación a PDF o PNG para presentación final.
