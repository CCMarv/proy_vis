---
title: Visualización de Datos — Notas de referencia y guía de estudio
author: Licenciatura en Inteligencia Artificial y Ciencia de Datos
version: "2.0"
date: 2026-05
language: es
topic: visualización de datos
---

# Visualización de Datos
## Notas de referencia y guía de estudio
**Licenciatura en Inteligencia Artificial y Ciencia de Datos**
*Versión 2.0 — Mayo 2026*

> **Cómo usar este documento.** Funciona en dos modos: como *guía* cuando estudias un tema por primera vez y como *referencia* cuando necesitas revisar algo específico. Cada sección termina con fuentes reales, verificadas y en su mayoría gratuitas. Las marcadas con 🌐 son de acceso libre en línea.

---

## 0. Recursos transversales

Estos recursos cubren múltiples temas del curso. Conviene tenerlos siempre a mano:

| Recurso | Formato | Acceso |
|---|---|---|
| Wilke, C. O. *Fundamentals of Data Visualization* | Libro completo en línea | 🌐 [clauswilke.com/dataviz](https://clauswilke.com/dataviz) |
| Munzner, T. *Visualization Analysis and Design* | Libro + diapositivas de la autora | 🌐 [cs.ubc.ca/~tmm/vadbook](https://www.cs.ubc.ca/~tmm/vadbook/) |
| Tufte, E. R. *The Visual Display of Quantitative Information* | Libro impreso | Biblioteca; edición 2001 |
| Knaflic, C. N. *Storytelling with Data* | Libro + blog | [storytellingwithdata.com](https://www.storytellingwithdata.com) |
| The Turing Way — *Guide for Communication* | Manual colaborativo en línea | 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app) |
| Healy, K. *Data Visualization: A Practical Introduction* | Libro completo en línea | 🌐 [socviz.co](https://socviz.co) |

---

## 1. Fundamentos

### 1.1 Definición

La visualización de datos convierte información en representaciones gráficas para hacerla más comprensible. Su valor práctico aparece cuando permite analizar datos con mayor rapidez, encontrar relaciones no evidentes y comunicar resultados a una audiencia concreta.

#### Ejemplo

Un analista de seguridad que recibe cientos de miles de registros de tráfico puede perder patrones relevantes en tablas. Al representar las solicitudes por minuto en una gráfica de líneas, un pico abrupto puede revelar un posible ataque DDoS o una anomalía operativa, facilitando la identificación y respuesta rápida.

### 1.2 Funciones principales

La visualización cumple tres funciones según el momento del análisis:

- **Explorar**: descubrir patrones, tendencias y anomalías antes de formular hipótesis.
- **Validar**: contrastar una hipótesis con evidencia visual.
- **Comunicar**: presentar hallazgos a una audiencia con el nivel de claridad adecuado.

### 1.3 Lugar en el proceso analítico

La visualización no se agrega al final como adorno. Aparece después de la limpieza y transformación de datos, pero su diseño depende desde el inicio de la pregunta que se quiere responder. Una visualización mal diseñada puede responder la pregunta incorrecta con gran precisión.

### 1.4 Dimensión ética

Toda visualización implica decisiones que afectan la interpretación: escala, color, nivel de agregación y forma. El profesional de datos asume la responsabilidad de buscar claridad sin sacrificar honestidad. Este tema se desarrolla con más profundidad en la sección de visualización ética.

### 1.5 Para profundizar

- Wilke, caps. 1–2: *Introduction* y *Visualizing amounts*. 🌐 [clauswilke.com/dataviz](https://clauswilke.com/dataviz)
- Munzner, cap. 1: *What's Viz, and Why Do It?*. 🌐 [cs.ubc.ca/~tmm/vadbook](https://www.cs.ubc.ca/~tmm/vadbook/)
- Tufte, cap. 1: *Graphical Excellence*.
- Cairo, A. *The Truthful Art*, cap. 1.

---

## 2. Tipos de datos

### 2.1 Clasificación

En visualización, los datos se agrupan en cuatro categorías que orientan tanto la elección del gráfico como el canal visual:

| Tipo | Características | Ejemplos |
|---|---|---|
| **Nominal / Categórico** | Sin orden natural | País, carrera, marca |
| **Ordinal** | Con orden, sin intervalos iguales | Bajo / Medio / Alto, nivel educativo |
| **Cuantitativo** | Magnitud medible | Ventas, temperatura, edad |
| **Temporal** | Ordenado en el tiempo | Fecha, hora, serie histórica |

### 2.2 Datos nominales

Representan clases sin jerarquía. Para distinguir grupos nominales funcionan bien el color categórico y la posición. Conviene limitar el número de categorías: más de 7–8 colores distintos dificultan la lectura.

### 2.3 Datos ordinales

Tienen orden pero no necesariamente distancias iguales entre niveles. La representación debe preservar la secuencia y evitar escalar como si los intervalos fueran iguales cuando no lo son.

### 2.4 Datos cuantitativos

Expresan magnitudes. Son los más adecuados para gráficos de comparación precisa como barras, líneas y dispersión. Se subdividen en continuos y discretos.

### 2.5 Datos temporales

Se ordenan a lo largo del tiempo. Su representación más natural es la línea de tiempo. El orden de los puntos no debe alterarse; hacerlo distorsiona la percepción de tendencia.

### 2.6 Para profundizar

- Munzner, cap. 2: *What: Data Abstraction*.
- Wilke, cap. 6: *Visualizing amounts* y cap. 9: *Visualizing many distributions at once*.
- Wickham, H. y Grolemund, G. *R for Data Science*, cap. 3. 🌐 [r4ds.had.co.nz](https://r4ds.had.co.nz)

---

## 3. Codificación visual

### 3.1 Idea central

La codificación visual traduce datos en atributos gráficos o canales. La eficacia de una visualización depende en gran parte de elegir el canal correcto para cada tipo de dato y tarea.

### 3.2 Jerarquía de Cleveland–McGill

Cleveland y McGill demostraron empíricamente que la precisión con que los humanos decodificamos información visual varía según el canal [web:12]. Este ranking ayuda a decidir qué codificación usar cuando se requiere comparación precisa.

1. **Posición en escala común**: máxima precisión.
2. **Posición en escalas no alineadas**.
3. **Longitud**.
4. **Ángulo / pendiente**.
5. **Área**.
6. **Volumen / densidad**.
7. **Saturación / tono de color**: menor precisión para magnitudes.

Cuando necesites comparación precisa, usa posición o longitud. Reserva el área y el color para categorías o para reforzar, no para codificar la variable principal.

### 3.3 Canales principales

- **Posición**: el canal más preciso. Fundamental en barras, dispersión y líneas.
- **Longitud**: útil para magnitudes y rankings.
- **Ángulo**: menos exacto. Los gráficos de pastel dependen de él.
- **Área**: útil para proporciones generales, no para comparaciones finas.
- **Color (tono)**: distingue categorías.
- **Color (saturación/luminosidad)**: puede codificar magnitudes cuando la paleta es secuencial.
- **Forma**: distingue grupos, pero con pocos símbolos.

### 3.4 Errores frecuentes

- Usar gráfico de pastel para comparar más de 3–4 categorías.
- Comparar áreas cuando una barra sería más clara.
- Aplicar colores sin función.
- Usar 3D sin necesidad analítica.
- Ordenar barras de forma arbitraria cuando hay un orden natural o relevante.

### 3.5 Para profundizar

- Cleveland, W. S. y McGill, R. (1984). *Graphical Perception: Theory, Experimentation, and Application to the Development of Graphical Methods*. [doi:10.2307/2288400](https://doi.org/10.2307/2288400)
- Munzner, cap. 5: *Marks and Channels*.
- Wilke, cap. 2: *Aesthetic mappings*.
- Heer, J. y Bostock, M. (2010). *Crowdsourcing Graphical Perception*. 🌐 [idl.cs.washington.edu](https://idl.cs.washington.edu/papers/crowdsourcing-graphical-perception/)

---

## 4. Principios perceptuales

### 4.1 Por qué importa la percepción

La efectividad de una visualización depende de cómo el sistema visual humano organiza lo que ve. Un diseño que respeta la percepción reduce el esfuerzo de interpretación y mejora la comprensión.

### 4.2 Leyes Gestalt aplicadas

| Ley | Efecto | Aplicación práctica |
|---|---|---|
| **Proximidad** | Los elementos cercanos se perciben como grupo | Agrupar barras relacionadas, espaciar grupos distintos |
| **Similitud** | Los elementos iguales se perciben como categoría | Color y forma consistentes para la misma variable |
| **Continuidad** | La mirada sigue líneas o curvas | Líneas de tiempo, curvas de tendencia |
| **Cierre** | Las formas incompletas se completan mentalmente | Bordes implícitos, áreas sombreadas |
| **Figura–fondo** | El objeto de interés se destaca del fondo | Colores de alto contraste para el elemento principal |

### 4.3 Memoria visual y carga cognitiva

La memoria visual de trabajo es limitada. Los gráficos con demasiados elementos simultáneos obligan al lector a hacer trabajo extra. El principio práctico es simple: cada elemento visual debe ganar su lugar o debe eliminarse.

### 4.4 Atributos preatencionales

Ciertos atributos son procesados por el sistema visual antes de la atención consciente: color, movimiento, tamaño y orientación. Usarlos para destacar lo importante acelera la comprensión.

### 4.5 Para profundizar

- Ware, C. *Information Visualization: Perception for Design*, cap. 5.
- Few, S. *Show Me the Numbers*, cap. 4.
- Wilke, cap. 17: *Redundant coding* y cap. 18: *Handling overlapping points*.
- Cairo, A. *The Functional Art*, cap. 3.

---

## 5. Visualización ética

### 5.1 Alcance

La visualización ética se ocupa de las decisiones de diseño que afectan la interpretación. Un mismo conjunto de datos puede narrar cosas distintas según cómo se presente. La responsabilidad profesional consiste en presentar los datos con honestidad [web:18].

### 5.2 Riesgos técnicos

- **Eje Y truncado**: omitir el cero en gráficos de barras exagera diferencias.
- **Escala logarítmica no declarada**: transforma la percepción sin aviso.
- **Comparaciones de área vs. longitud**: sobreestimamos áreas, lo que puede inflar diferencias.
- **Agregación excesiva**: promediar datos heterogéneos puede ocultar variación importante.
- **Cherry-picking temporal**: elegir el rango de fechas que favorece una narrativa.

### 5.3 Justicia informativa

La discusión reciente amplía la ética hacia la empatía, la representación y la justicia informativa. Cuando los datos representan personas, las decisiones de diseño tienen consecuencias sociales reales.

### 5.4 Para profundizar

- Tufte, cap. 2: *Graphical Integrity*.
- Cairo, A. *How Charts Lie*.
- D'Ignazio, C. y Klein, L. F. *Data Feminism*. 🌐 [data-feminism.mitpress.mit.edu](https://data-feminism.mitpress.mit.edu)
- Hullman, J. y Diakopoulos, N. (2011). *Visualization Rhetoric*. [doi:10.1109/TVCG.2011.255](https://doi.org/10.1109/TVCG.2011.255)

---

## 6. Accesibilidad

### 6.1 Relevancia

Una visualización inaccesible excluye a parte de la audiencia. Diseñar con accesibilidad desde el inicio es más eficiente que corregirla después, y suele mejorar la claridad para todos.

### 6.2 Daltonismo y paletas

Aproximadamente el 8% de los hombres y el 0.5% de las mujeres tienen alguna forma de deficiencia en la visión del color. Las recomendaciones principales son evitar dependencia exclusiva de rojo–verde, usar paletas validadas y añadir redundancia visual.

### 6.3 Contraste y legibilidad

La guía WCAG 2.1 recomienda una relación de contraste mínima de 4.5:1 para texto normal [web:17]. Aplicar este criterio al texto dentro de gráficos mejora la legibilidad.

### 6.4 Descripción alternativa

Para visualizaciones en contextos digitales, añadir texto alternativo descriptivo permite que personas que usan lectores de pantalla accedan a la información.

### 6.5 Para profundizar

- ColorBrewer 2.0. 🌐 [colorbrewer2.org](https://colorbrewer2.org)
- Okabe, M. e Ito, K. *Color Universal Design*. 🌐 [jfly.uni-koeln.de/color](https://jfly.uni-koeln.de/color/)
- Wilke, cap. 19: *Common pitfalls of color use*.
- WCAG 2.1 (W3C). 🌐 [w3.org/TR/WCAG21](https://www.w3.org/TR/WCAG21/)

---

## 7. Color, forma y estilo

### 7.1 Tres esquemas de color

| Esquema | Cuándo usarlo | Ejemplo |
|---|---|---|
| **Secuencial** | Magnitud ordenada de menor a mayor | Densidad de población |
| **Divergente** | Datos con punto central significativo | Cambio respecto a la media |
| **Categórico** | Grupos sin jerarquía | Países, marcas, categorías |

### 7.2 Jerarquía visual

La jerarquía visual guía la mirada hacia lo importante. Se construye con tamaño, color, posición, contraste y espacio en blanco.

### 7.3 Consistencia y simplificación

La consistencia en símbolos, colores y tipografía permite al lector construir un modelo mental estable. El ruido visual consume capacidad de procesamiento sin aportar información.

### 7.4 Para profundizar

- Wilke, cap. 4: *Color scales* y cap. 23: *Balance the data and context*.
- Tufte: concepto de *data-ink ratio* y *chartjunk*.
- ColorBrewer 2.0. 🌐 [colorbrewer2.org](https://colorbrewer2.org)
- Zeileis, A. et al. (2020). *colorspace: A Toolbox for Manipulating and Assessing Colors and Palettes*. [doi:10.18637/jss.v096.i01](https://doi.org/10.18637/jss.v096.i01)

---

## 8. Propósito analítico

### 8.1 Cuatro tipos de visualización según propósito

| Tipo | Objetivo | Características de diseño |
|---|---|---|
| **Exploratoria** | Descubrir patrones y anomalías | Flexible, rápida de generar, no necesita pulido |
| **Explicativa** | Comunicar una conclusión específica | Controlada, centrada en un mensaje |
| **Operativa** | Monitorear indicadores en tiempo real | Clara, rápida de leer, actualizable |
| **Estratégica** | Apoyar decisiones de alto nivel | Contextualizada, tendencia e impacto visibles |

### 8.2 Criterio práctico

Antes de diseñar una visualización, responde dos preguntas:
1. ¿Quién la va a leer?
2. ¿Qué decisión o comprensión debe producir?

La respuesta define el nivel de detalle, el tipo de gráfico y el grado de interactividad necesarios.

### 8.3 Para profundizar

- Munzner, cap. 3: *Why: Task Abstraction*.
- Knaflic, *Storytelling with Data*, cap. 1.
- Few, S. *Show Me the Numbers*, cap. 2.

---

## 9. Tipos de gráficos

### 9.1 Gráficos analíticos principales

| Gráfico | Mejor para | Precaución |
|---|---|---|
| **Barras** | Comparar magnitudes entre categorías | No truncar el eje Y |
| **Líneas** | Mostrar tendencia temporal | Solo conectar puntos ordenados en tiempo |
| **Dispersión** | Mostrar relación entre dos variables cuantitativas | Distinguir correlación de causalidad |
| **Histograma** | Distribución de una variable continua | El ancho del bin afecta la percepción |
| **Caja y bigotes** | Distribución y outliers | La audiencia necesita saber leerlo |
| **Mapa de calor** | Patrones en matrices | Usar color secuencial o divergente según el caso |
| **Área apilada** | Composición acumulada en el tiempo | Dificulta comparar partes intermedias |

### 9.2 Gráficos para ciencia de datos e IA

- **Curva ROC / AUC**: evaluar clasificadores binarios.
- **Matriz de confusión**: visualizar errores de clasificación.
- **Importancia de características**: interpretar modelos de árbol o SHAP.
- **Proyecciones de alta dimensión** (t-SNE, UMAP): explorar embeddings y clusters.
- **Banda de confianza / intervalo de predicción**: representar incertidumbre en regresión.
- **Violin plot**: alternativa más rica al boxplot.

### 9.3 Diagramas de proceso y gestión

Estos no son gráficos de datos, pero sí herramientas visuales importantes: diagrama de flujo, mapa mental, Ishikawa, Pareto, Gantt, línea de tiempo, Venn, mapa de stakeholders, journey map, blueprint de servicio, arquitectura, UML y Kanban.

> **Distinción clave**: los gráficos analíticos describen datos. Los diagramas de proceso representan relaciones, secuencias o estructuras. No son intercambiables.

### 9.4 Para profundizar

- Wilke, caps. 5–16.
- Munzner, caps. 7–12.
- Chart Chooser (Juice Analytics).
- Schwabish, J. *Better Data Visualizations*.

---

## 10. Errores comunes en codificación visual

### 10.1 Lista de verificación negativa

Antes de publicar una visualización, comprobar que no incurre en:

- [ ] Eje Y truncado en gráfico de barras.
- [ ] Gráfico de pastel con más de 4–5 categorías.
- [ ] Comparación de áreas cuando las longitudes serían más precisas.
- [ ] Colores sin función analítica.
- [ ] 3D aplicado sin necesidad real.
- [ ] Barras desordenadas cuando hay un orden natural o relevante.
- [ ] Demasiadas categorías de forma.
- [ ] Doble eje Y con escalas incompatibles.
- [ ] Escala logarítmica sin indicarlo explícitamente.

### 10.2 Para profundizar

- Tufte, cap. 2: *Graphical Integrity*.
- Cairo, A. *How Charts Lie*.
- Wilke, cap. 17 y cap. 26.

---

## 11. Herramientas de visualización

### 11.1 Python

El entorno más completo para ciencia de datos e IA. Permite integrar la visualización con el análisis en el mismo notebook.

| Biblioteca | Uso principal | Nivel |
|---|---|---|
| **Matplotlib** | Base; control total | Intermedio–avanzado |
| **Seaborn** | Estadística; API de alto nivel sobre Matplotlib | Básico–intermedio |
| **Plotly** | Gráficos interactivos para web y dashboards | Básico–intermedio |
| **Altair** | Gramática declarativa basada en Vega-Lite | Intermedio |
| **Bokeh** | Visualizaciones interactivas en navegador | Intermedio |

### 11.2 R

Referencia en estadística formal y visualizaciones para publicación académica.

- **ggplot2**: gramática de gráficos.
- **ggplotly**: convierte gráficos de ggplot2 en interactivos.

### 11.3 JavaScript / Web

- **D3.js**: máxima flexibilidad para visualización interactiva en navegador.
- **Vega-Lite**: especificación declarativa de alto nivel.

### 11.4 Business intelligence

- **Tableau**: análisis y dashboards interactivos para grandes volúmenes de datos.
- **Power BI**: integración con fuentes corporativas y Excel.
- **Looker / Google Looker Studio**: análisis en la nube.

### 11.5 Para profundizar

- Documentación oficial de Matplotlib. 🌐 [matplotlib.org](https://matplotlib.org)
- Documentación oficial de Seaborn. 🌐 [seaborn.pydata.org](https://seaborn.pydata.org)
- Documentación oficial de Plotly. 🌐 [plotly.com/python](https://plotly.com/python)
- Documentación oficial de Altair. 🌐 [altair-viz.github.io](https://altair-viz.github.io)
- Wickham, H. *ggplot2: Elegant Graphics for Data Analysis*. 🌐 [ggplot2-book.org](https://ggplot2-book.org)
- Murray, S. *Interactive Data Visualization for the Web*.
- VanderPlas, J. *Python Data Science Handbook*. 🌐 [jakevdp.github.io/PythonDataScienceHandbook](https://jakevdp.github.io/PythonDataScienceHandbook/)

---

## 12. Geovisualización

### 12.1 Definición

La geovisualización aplica los principios de visualización al análisis de datos espaciales. Su base conceptual proviene de la cartografía, los sistemas de información geográfica y el visual analytics.

### 12.2 Proyecciones cartográficas

Toda proyección convierte la superficie esférica de la Tierra en un plano, introduciendo distorsiones en área, forma, distancia o dirección. La selección depende del objetivo.

- **Mercator**: preserva ángulos, distorsiona áreas.
- **Robinson / Winkel Tripel**: compromiso entre distorsiones.
- **Albers / Lambert**: preserva áreas para mapas regionales o nacionales.

### 12.3 Tipos de mapa temático

| Tipo | Cuándo usarlo |
|---|---|
| **Coroplético** | Valor normalizado por área o población |
| **Burbuja / Proporcional** | Magnitud absoluta |
| **De puntos** | Distribución espacial de eventos individuales |
| **De flujo** | Movimiento entre orígenes y destinos |
| **De calor** | Densidad de eventos sobre una superficie |

### 12.4 Mapas interactivos

La geovisualización moderna permite exploración dinámica: zoom, filtros por región, capas dinámicas e interacción en tiempo real. Plataformas como Mapbox, Kepler.gl y Deck.gl facilitan mapas interactivos personalizables; el mapa puede operar como una interfaz analítica completa.

### 12.5 Para profundizar

- Wilke, cap. 15: *Visualizing geospatial data*.
- Dorling, D. y Fairbairn, D. *Mapping: Ways of Representing the World*.
- Geopandas documentation. 🌐 [geopandas.org](https://geopandas.org)
- Kepler.gl. 🌐 [kepler.gl](https://kepler.gl)
- Deck.gl. 🌐 [deck.gl](https://deck.gl)

- Mapbox. 🌐 [mapbox.com](https://www.mapbox.com)

---

## 13. Evaluación de visualizaciones

### 13.1 Por qué es necesario evaluar

Una visualización no está terminada porque parece correcta al autor. Conviene verificar si comunica el mensaje previsto a la audiencia prevista.

### 13.2 Lista de verificación de calidad

- [ ] ¿Se entiende el mensaje principal en menos de 10 segundos?
- [ ] ¿El punto focal es claro?
- [ ] ¿Los colores tienen función analítica?
- [ ] ¿Se eliminó el ruido visual innecesario?
- [ ] ¿Está alineada con la tarea o pregunta que motivó el análisis?
- [ ] ¿Genera comprensión o acción, no solo muestra datos?
- [ ] ¿Es accesible?
- [ ] ¿Es ética?
- [ ] ¿Puede reproducirse con el mismo resultado?

### 13.3 Métodos de evaluación

- **Revisión experta**.
- **Prueba con usuarios**.
- **Eye tracking**.

### 13.4 Para profundizar

- Munzner, cap. 4: *Analysis: Four Levels for Validation*.
- Isenberg, T. et al. (2013). *A Systematic Review on the Practice of Evaluating Visualization*. [doi:10.1109/TVCG.2013.126](https://doi.org/10.1109/TVCG.2013.126)
- Nielsen, J. *10 Usability Heuristics*. 🌐 [nngroup.com/articles/ten-usability-heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)

---

## 14. Incertidumbre y límites del dato

### 14.1 El problema de los datos "perfectos"

Las introducciones suelen presentar la visualización como si los datos fueran exactos y completos. En la práctica, rara vez lo son. Ignorar la incertidumbre en la visualización puede llevar a decisiones mal informadas.

### 14.2 Fuentes de incertidumbre

- **Error de medición**.
- **Variabilidad natural**.
- **Datos faltantes**.
- **Supuestos del modelo**.

### 14.3 Cómo representar incertidumbre visualmente

| Técnica | Cuándo usarla |
|---|---|
| **Barras de error** | Error estándar o desviación estándar |
| **Bandas de confianza** | Intervalo de confianza en regresión o series de tiempo |
| **Intervalos de predicción** | Rango esperado para observaciones futuras |
| **Transparencia** | Reducir certeza visual de estimaciones inciertas |
| **Múltiples líneas** | Mostrar espacio de posibles trayectorias |
| **Nota textual** | Aclarar fuente, fecha, muestra y limitaciones |

### 14.4 Conexión con IA/CD

En modelos de machine learning, la incertidumbre es central. Los modelos de clasificación producen probabilidades, no certezas. Los modelos de regresión producen intervalos de predicción. Los modelos bayesianos producen distribuciones posteriores completas.

### 14.5 Para profundizar

- Wilke, cap. 16: *Visualizing uncertainty*.
- Hullman, J. (2020). *Why Authors Don't Visualize Uncertainty*. [doi:10.1109/TVCG.2019.2934287](https://doi.org/10.1109/TVCG.2019.2934287)
- Kay, M. *ggdist*. 🌐 [mjskay.github.io/ggdist](https://mjskay.github.io/ggdist/)
- The Turing Way, sección *Reproducible Research*. 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app)

---

## 15. Visualización de modelos de machine learning

### 15.1 Por qué es fundamental

Esta es una de las conexiones más directas entre la materia de visualización y el resto de la carrera. Los modelos de ML producen outputs difíciles de interpretar sin representación gráfica.

### 15.2 Evaluación de clasificadores

**Curva ROC y AUC**
- Eje X: tasa de falsos positivos.
- Eje Y: sensibilidad.
- AUC = área bajo la curva.

**Matriz de confusión**
- Cuadrícula de clases reales vs. predichas.
- Mapa de calor para lectura visual.

**Curva precisión–recall**
- Más informativa que ROC cuando las clases están desbalanceadas.

### 15.3 Interpretabilidad de modelos

**Importancia de características**
- En árboles y bosques aleatorios: medida de reducción de impureza.
- Gráfico recomendado: barras ordenadas de mayor a menor importancia.

**SHAP**
- Summary plot, waterfall plot y dependence plot.

**LIME**
- Aproxima localmente el comportamiento del modelo con un modelo simple.

### 15.4 Exploración de espacios de alta dimensión

| Técnica | Uso | Precaución |
|---|---|---|
| **PCA** | Visualización rápida, interpretable | Solo captura varianza lineal |
| **t-SNE** | Exploración de clusters | Hiperparámetros influyen mucho |
| **UMAP** | Más rápido que t-SNE | Depende de hiperparámetros |

t-SNE y UMAP son herramientas exploratorias. No conviene concluir similitud o diferencia entre clusters solo por la proximidad visual.

### 15.5 Visualización del entrenamiento

- **Curva de aprendizaje**: loss y métrica en entrenamiento vs. validación.
- **Curva de validación**: métrica vs. valor de hiperparámetro.

### 15.6 Para profundizar

- Lundberg, S. M. y Lee, S. I. (2017). *A Unified Approach to Interpreting Model Predictions*. 🌐 [arxiv.org/abs/1705.07874](https://arxiv.org/abs/1705.07874)
- SHAP library documentation. 🌐 [shap.readthedocs.io](https://shap.readthedocs.io)
- Molnar, C. *Interpretable Machine Learning*. 🌐 [christophm.github.io/interpretable-ml-book](https://christophm.github.io/interpretable-ml-book)
- Scikit-learn: visualización de métricas. 🌐 [scikit-learn.org/stable/visualizations.html](https://scikit-learn.org/stable/visualizations.html)
- McInnes, L. et al. (2018). *UMAP: Uniform Manifold Approximation and Projection*. 🌐 [arxiv.org/abs/1802.03426](https://arxiv.org/abs/1802.03426)
- Wattenberg, M. et al. (2016). *How to Use t-SNE Effectively*. 🌐 [distill.pub/2016/misread-tsne](https://distill.pub/2016/misread-tsne/)

---

## 16. Storytelling con datos

### 16.1 Qué aporta

El storytelling organiza la información para que una audiencia comprenda qué ocurre, por qué importa y qué puede hacerse. Convierte la visualización en herramienta de comunicación, no solo de exploración [web:18].

### 16.2 Estructura narrativa básica

1. **Contexto**: qué problema o pregunta motiva el análisis.
2. **Tensión**: qué revelan los datos que no era evidente.
3. **Resolución**: qué conclusión o acción se desprende.

### 16.3 Principio de equilibrio

La historia debe apoyar la evidencia, no sustituirla. Cuando la narrativa se adelanta a los datos, la visualización pierde rigor y puede convertirse en persuasión disfrazada de análisis.

### 16.4 Para profundizar

- Knaflic, C. N. *Storytelling with Data*.
- Dykes, B. *Effective Data Storytelling*.
- Segel, E. y Heer, J. (2010). *Narrative Visualization: Telling Stories with Data*. [doi:10.1109/TVCG.2010.179](https://doi.org/10.1109/TVCG.2010.179)

---

## 17. Reproducibilidad en visualización

### 17.1 Importancia

Una visualización es parte del trabajo científico y debe poder reconstruirse. La reproducibilidad evita inconsistencias entre versiones y facilita la colaboración.

### 17.2 Prácticas recomendadas

- Usar scripts o notebooks.
- Guardar datos originales y procesados por separado.
- Documentar paletas, rangos y filtros.
- Versionar el código con Git.
- Separar visualizaciones exploratorias de las de comunicación final.

### 17.3 Para profundizar

- The Turing Way, capítulo *Reproducible Research*. 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app)
- Quarto. 🌐 [quarto.org](https://quarto.org)
- Wilson, G. et al. (2017). *Good Enough Practices in Scientific Computing*. [doi:10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510)

---

## 18. Lista de verificación de calidad

Antes de cerrar una visualización:

| Criterio | Verificado |
|---|---|
| Se entiende el mensaje en menos de 10 segundos | ☐ |
| El foco es claro y no hay elementos que compitan con él | ☐ |
| El canal visual corresponde a la jerarquía de Cleveland–McGill | ☐ |
| El color tiene función analítica, no decorativa | ☐ |
| No hay ruido visual innecesario | ☐ |
| Está alineada con la tarea o pregunta analítica | ☐ |
| Es accesible | ☐ |
| Es ética | ☐ |
| Representa o declara la incertidumbre cuando existe | ☐ |
| Puede reproducirse con el mismo resultado | ☐ |

---

## 19. Ruta de profundización recomendada

1. **Fundamentos y propósito** — Wilke caps. 1–2; Munzner cap. 1.
2. **Tipos de datos** — Munzner cap. 2; Wickham & Grolemund cap. 3.
3. **Codificación visual** — Munzner cap. 5; Cleveland & McGill (1984).
4. **Percepción y Gestalt** — Ware, *Information Visualization*, cap. 5.
5. **Ética y accesibilidad** — Tufte; Cairo; D'Ignazio & Klein.
6. **Color y estilo** — Wilke cap. 4; ColorBrewer.
7. **Tipos de gráficos** — Wilke caps. 5–16; Munzner caps. 7–12.
8. **Herramientas** — documentación oficial de Seaborn, Plotly y ggplot2.
9. **Visualización de modelos ML** — Molnar; SHAP docs.
10. **Incertidumbre** — Wilke cap. 16; Hullman (2020).
11. **Geovisualización** — Wilke cap. 15; Geopandas docs.
12. **Evaluación, storytelling y reproducibilidad** — Munzner cap. 4; Knaflic; The Turing Way.

---

## 20. Bibliografía completa

### Libros de referencia

- Cairo, A. *How Charts Lie: Getting Smarter About Visual Information*. Norton, 2019.
- Cairo, A. *The Functional Art*. New Riders, 2012.
- Cairo, A. *The Truthful Art*. New Riders, 2016.
- D'Ignazio, C. y Klein, L. F. *Data Feminism*. MIT Press, 2020. 🌐 [data-feminism.mitpress.mit.edu](https://data-feminism.mitpress.mit.edu)
- Dykes, B. *Effective Data Storytelling*. Wiley, 2019.
- Few, S. *Show Me the Numbers*, 2ª ed. Analytics Press, 2012.
- Healy, K. *Data Visualization: A Practical Introduction*. Princeton UP, 2018. 🌐 [socviz.co](https://socviz.co)
- Knaflic, C. N. *Storytelling with Data*. Wiley, 2015.
- Molnar, C. *Interpretable Machine Learning*, 2ª ed. 2022. 🌐 [christophm.github.io/interpretable-ml-book](https://christophm.github.io/interpretable-ml-book)
- Munzner, T. *Visualization Analysis and Design*. CRC Press, 2014. 🌐 [cs.ubc.ca/~tmm/vadbook](https://www.cs.ubc.ca/~tmm/vadbook/)
- Murray, S. *Interactive Data Visualization for the Web*, 2ª ed. O'Reilly, 2017.
- Schwabish, J. *Better Data Visualizations*. Columbia UP, 2021.
- Tufte, E. R. *The Visual Display of Quantitative Information*, 2ª ed. Graphics Press, 2001.
- VanderPlas, J. *Python Data Science Handbook*. O'Reilly, 2016. 🌐 [jakevdp.github.io/PythonDataScienceHandbook](https://jakevdp.github.io/PythonDataScienceHandbook/)
- Ware, C. *Information Visualization: Perception for Design*, 3ª ed. Morgan Kaufmann, 2012.
- Wickham, H. *ggplot2: Elegant Graphics for Data Analysis*, 3ª ed. Springer, 2016. 🌐 [ggplot2-book.org](https://ggplot2-book.org)
- Wickham, H. y Grolemund, G. *R for Data Science*, 2ª ed. O'Reilly, 2023. 🌐 [r4ds.hadley.nz](https://r4ds.hadley.nz)
- Wilke, C. O. *Fundamentals of Data Visualization*. O'Reilly, 2019. 🌐 [clauswilke.com/dataviz](https://clauswilke.com/dataviz)

### Artículos clave

- Cleveland, W. S. y McGill, R. (1984). *Graphical Perception: Theory, Experimentation, and Application to the Development of Graphical Methods*. [doi:10.2307/2288400](https://doi.org/10.2307/2288400)
- Heer, J. y Bostock, M. (2010). *Crowdsourcing Graphical Perception*. 🌐 [idl.cs.washington.edu](https://idl.cs.washington.edu/papers/crowdsourcing-graphical-perception/)
- Hullman, J. y Diakopoulos, N. (2011). *Visualization Rhetoric*. [doi:10.1109/TVCG.2011.255](https://doi.org/10.1109/TVCG.2011.255)
- Hullman, J. (2020). *Why Authors Don't Visualize Uncertainty*. [doi:10.1109/TVCG.2019.2934287](https://doi.org/10.1109/TVCG.2019.2934287)
- Lundberg, S. M. y Lee, S. I. (2017). *A Unified Approach to Interpreting Model Predictions*. 🌐 [arxiv.org/abs/1705.07874](https://arxiv.org/abs/1705.07874)
- McInnes, L. et al. (2018). *UMAP: Uniform Manifold Approximation and Projection*. 🌐 [arxiv.org/abs/1802.03426](https://arxiv.org/abs/1802.03426)
- Segel, E. y Heer, J. (2010). *Narrative Visualization: Telling Stories with Data*. [doi:10.1109/TVCG.2010.179](https://doi.org/10.1109/TVCG.2010.179)
- Wattenberg, M. et al. (2016). *How to Use t-SNE Effectively*. 🌐 [distill.pub/2016/misread-tsne](https://distill.pub/2016/misread-tsne/)
- Wilson, G. et al. (2017). *Good Enough Practices in Scientific Computing*. [doi:10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510)

### Recursos en línea permanentes

- ColorBrewer 2.0. 🌐 [colorbrewer2.org](https://colorbrewer2.org)
- Okabe–Ito Color Universal Design. 🌐 [jfly.uni-koeln.de/color](https://jfly.uni-koeln.de/color/)
- SHAP library documentation. 🌐 [shap.readthedocs.io](https://shap.readthedocs.io)
- The Turing Way. 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app)
- Quarto. 🌐 [quarto.org](https://quarto.org)
- Distill.pub. 🌐 [distill.pub](https://distill.pub)

*Documento generado para uso académico en la Licenciatura en Inteligencia Artificial y Ciencia de Datos. Versión 2.0 — Mayo 2026.*

---

## Interactividad

### Interactividad: eventos, tooltips, selección y filtrado

La interactividad extiende el valor de las representaciones estáticas permitiendo que los usuarios exploren los datos de forma dinámica. Eventos como clic, hover y selección permiten mostrar detalles (tooltips), resaltar subconjuntos o aplicar filtros sin recargar la vista principal. Esto facilita la investigación dirigida y el análisis ad hoc.

Ejemplo: en un panel de monitoreo, pasar el cursor sobre un punto puede mostrar la IP, la hora exacta y el tipo de evento; al hacer clic en un nodo se filtran los registros asociados, permitiendo un análisis detallado sin perder el contexto global.

### Bibliotecas y patrones

D3.js y Plotly son herramientas habituales para añadir interactividad: D3 ofrece máxima flexibilidad para eventos y animaciones finas; Plotly facilita desarrollar componentes interactivos con menos código. Patrones comunes incluyen tooltips informativos, selección ligada (linked brushing) y filtros por facetas o rangos temporales.

Para diseños accesibles, mantén alternativas a la interacción basada en hover (por ejemplo, clics o controles visibles) y garantiza que la información clave sea legible sin depender exclusivamente de tooltips.