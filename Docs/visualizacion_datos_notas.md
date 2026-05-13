# Visualización de Datos
## Notas de referencia y guía de estudio
**Licenciatura en Inteligencia Artificial y Ciencia de Datos**
*Versión 2.0 — Mayo 2026*

---

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

### 1.2 Funciones principales

La visualización cumple tres funciones según el momento del análisis:

- **Explorar**: descubrir patrones, tendencias y anomalías antes de formular hipótesis.
- **Validar**: contrastar una hipótesis con evidencia visual.
- **Comunicar**: presentar hallazgos a una audiencia con el nivel de claridad adecuado.

### 1.3 Lugar en el proceso analítico

La visualización no se agrega al final como adorno. Aparece después de la limpieza y transformación de datos, pero su diseño depende desde el inicio de la pregunta que se quiere responder. Una visualización mal diseñada puede responder la pregunta incorrecta con gran precisión.

### 1.4 Dimensión ética (adelanto)

Toda visualización implica decisiones que afectan la interpretación: escala, color, nivel de agregación, forma. El profesional de datos asume la responsabilidad de buscar claridad sin sacrificar honestidad. Este tema se desarrolla en la sección 5.

### 1.5 Para profundizar

- Wilke, caps. 1–2: *Introduction* y *Visualizing amounts*. 🌐 [clauswilke.com/dataviz](https://clauswilke.com/dataviz)
- Munzner, cap. 1: *What's Viz, and Why Do It?*. [cs.ubc.ca/~tmm/vadbook](https://www.cs.ubc.ca/~tmm/vadbook/)
- Tufte, cap. 1: *Graphical Excellence*.
- Cairo, A. *The Truthful Art*, cap. 1 (introducción al pensamiento visual).

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

Expresan magnitudes. Son los más adecuados para gráficos de comparación precisa (barras, líneas, dispersión). Se subdividen en *continuos* (temperatura) y *discretos* (número de hijos).

### 2.5 Datos temporales

Se ordenan a lo largo del tiempo. Su representación más natural es la línea de tiempo. El orden de los puntos no debe alterarse; hacerlo distorsiona la percepción de tendencia.

### 2.6 Para profundizar

- Munzner, cap. 2: *What: Data Abstraction*. Taxonomía formal de tipos de datos y atributos.
- Wilke, cap. 6: *Visualizing amounts* y cap. 9: *Visualizing many distributions at once*.
- Wickham, H. y Grolemund, G. *R for Data Science*, cap. 3: tipos de variables. 🌐 [r4ds.had.co.nz](https://r4ds.had.co.nz)

---

## 3. Codificación visual

### 3.1 Idea central

La codificación visual traduce datos en atributos gráficos (canales). La eficacia de una visualización depende en gran parte de elegir el canal correcto para cada tipo de dato y tarea.

### 3.2 Jerarquía de Cleveland–McGill

Cleveland y McGill (1984) establecieron empíricamente que la precisión con que los humanos decodificamos información visual varía según el canal. Este ranking es la base teórica de por qué ciertos gráficos funcionan mejor:

1. **Posición en escala común** — máxima precisión (ej: gráfico de barras alineadas)
2. **Posición en escalas no alineadas** (ej: gráficos pequeños múltiples)
3. **Longitud**
4. **Ángulo / Pendiente**
5. **Área**
6. **Volumen / Densidad**
7. **Saturación / Tono de color** — menor precisión para magnitudes

> **Implicación directa**: cuando necesites comparación precisa, usa posición o longitud. Reserva el área y el color para categorías o para reforzar, no para codificar la variable principal.

### 3.3 Descripción de canales principales

- **Posición**: el canal más preciso. Fundamental en barras, dispersión y líneas.
- **Longitud**: útil para magnitudes y rankings.
- **Ángulo**: menos exacto. Los gráficos de pastel dependen de él, de ahí su debilidad.
- **Área**: útil para proporciones generales, no para comparaciones finas.
- **Color (tono)**: distingue categorías. No codifica magnitudes ordinales bien.
- **Color (saturación/luminosidad)**: puede codificar magnitudes cuando la paleta es secuencial.
- **Forma**: distingue grupos, pero con pocos símbolos (máx. 5–6).

### 3.4 Errores frecuentes

- Usar gráfico de pastel para comparar más de 3–4 categorías.
- Comparar áreas cuando una barra sería más clara.
- Aplicar colores sin función (decorativo).
- Usar 3D sin necesidad analítica real: añade área/volumen sin información.
- Ordenar barras de forma arbitraria cuando hay un orden natural o relevante.

### 3.5 Para profundizar

- Cleveland, W. S. y McGill, R. (1984). *Graphical Perception: Theory, Experimentation, and Application to the Development of Graphical Methods*. Journal of the American Statistical Association, 79(387), 531–554. [doi:10.2307/2288400](https://doi.org/10.2307/2288400)
- Munzner, cap. 5: *Marks and Channels*.
- Wilke, cap. 2: *Aesthetic mappings*.
- Heer, J. y Bostock, M. (2010). *Crowdsourcing Graphical Perception*. CHI 2010. 🌐 [idl.cs.washington.edu](https://idl.cs.washington.edu/papers/crowdsourcing-graphical-perception/)

---

## 4. Principios perceptuales

### 4.1 Por qué importa la percepción

La efectividad de una visualización depende de cómo el sistema visual humano organiza lo que ve. Un diseño que respeta la percepción reduce el esfuerzo de interpretación y mejora la comprensión.

### 4.2 Leyes Gestalt aplicadas a visualización

| Ley | Efecto | Aplicación práctica |
|---|---|---|
| **Proximidad** | Los elementos cercanos se perciben como grupo | Agrupar barras relacionadas, espaciar grupos distintos |
| **Similitud** | Los elementos iguales se perciben como categoría | Color y forma consistentes para la misma variable |
| **Continuidad** | La mirada sigue líneas o curvas | Líneas de tiempo, curvas de tendencia |
| **Cierre** | Las formas incompletas se completan mentalmente | Bordes implícitos, áreas sombreadas |
| **Figura–fondo** | El objeto de interés se destaca del fondo | Colores de alto contraste para el elemento principal |

### 4.3 Memoria visual y carga cognitiva

La memoria visual de trabajo es limitada. Los gráficos con demasiados elementos simultáneos obligan al lector a hacer trabajo extra. El principio práctico: cada elemento visual debe ganar su lugar o debe eliminarse.

### 4.4 Pre-attentive attributes

Ciertos atributos son procesados por el sistema visual antes de la atención consciente: color, movimiento, tamaño, orientación. Usarlos para destacar lo importante acelera la comprensión.

### 4.5 Para profundizar

- Ware, C. *Information Visualization: Perception for Design*, cap. 5. Estándar en el campo.
- Few, S. *Show Me the Numbers*, cap. 4: *Tapping the Power of Visual Perception*.
- Wilke, cap. 17: *Redundant coding* y cap. 18: *Handling overlapping points*.
- Cairo, A. *The Functional Art*, cap. 3: *The Eye and the Visual Brain*.

---

## 5. Visualización ética

### 5.1 Alcance

La visualización ética se ocupa de las decisiones de diseño que afectan la interpretación. Un mismo conjunto de datos puede narrar cosas distintas según cómo se presente. La responsabilidad profesional consiste en presentar los datos con honestidad.

### 5.2 Riesgos técnicos

- **Eje Y truncado**: omitir el cero en gráficos de barras exagera diferencias.
- **Escala logarítmica no declarada**: transforma la percepción sin aviso.
- **Comparaciones de área vs. longitud**: sobreestimamos áreas, lo que puede inflar diferencias.
- **Agregación excesiva**: promediar datos heterogéneos puede ocultar variación importante.
- **Cherry-picking temporal**: elegir el rango de fechas que favorece una narrativa.

### 5.3 Dimensión contemporánea: justicia informativa

La discusión reciente amplía la ética hacia la empatía, la representación y la justicia informativa. Cuando los datos representan personas (salud, desigualdad, violencia, economía), las decisiones de diseño tienen consecuencias sociales reales.

### 5.4 Para profundizar

- Tufte, cap. 2: *Graphical Integrity* — análisis clásico de gráficos engañosos.
- Cairo, A. *How Charts Lie*. Libro accesible sobre engaño visual intencional y no intencional. (2019)
- D'Ignazio, C. y Klein, L. F. *Data Feminism*, cap. 3. 🌐 [data-feminism.mitpress.mit.edu](https://data-feminism.mitpress.mit.edu)
- Hullman, J. y Diakopoulos, N. (2011). *Visualization Rhetoric: Framing Effects in Narrative Visualization*. IEEE TVCG, 17(12). [doi:10.1109/TVCG.2011.255](https://doi.org/10.1109/TVCG.2011.255)

---

## 6. Accesibilidad

### 6.1 Relevancia

Una visualización inaccesible excluye a parte de la audiencia. Diseñar con accesibilidad desde el inicio es más eficiente que corregirla después, y suele mejorar la claridad para todos.

### 6.2 Daltonismo y paletas

Aproximadamente el 8% de los hombres y el 0.5% de las mujeres tienen alguna forma de deficiencia en la visión del color. Las recomendaciones principales:

- Evitar dependencia exclusiva de rojo–verde.
- Usar paletas validadas (ColorBrewer, Okabe–Ito).
- Añadir redundancia visual: formas, patrones o etiquetas directas que no dependan solo del color.

### 6.3 Contraste y legibilidad

La guía WCAG 2.1 recomienda una relación de contraste mínima de 4.5:1 para texto normal. Aplicar este criterio al texto dentro de gráficos mejora la legibilidad.

### 6.4 Descripción alternativa

Para visualizaciones en contextos digitales, añadir texto alternativo descriptivo permite que personas que usan lectores de pantalla accedan a la información.

### 6.5 Para profundizar

- ColorBrewer 2.0 — paletas diseñadas para mapas y accesibilidad. 🌐 [colorbrewer2.org](https://colorbrewer2.org)
- Okabe, M. e Ito, K. *Color Universal Design*. 🌐 [jfly.uni-koeln.de/color](https://jfly.uni-koeln.de/color/)
- Wilke, cap. 19: *Common pitfalls of color use*.
- WCAG 2.1 (W3C). 🌐 [w3.org/TR/WCAG21](https://www.w3.org/TR/WCAG21/)

---

## 7. Color, forma y estilo

### 7.1 Tres esquemas de color

| Esquema | Cuándo usarlo | Ejemplo |
|---|---|---|
| **Secuencial** | Magnitud ordenada de menor a mayor | Densidad de población |
| **Divergente** | Datos con punto central significativo | Cambio respecto a la media, temperatura sobre/bajo 0 |
| **Categórico** | Grupos sin jerarquía | Países, marcas, categorías |

### 7.2 Jerarquía visual

La jerarquía visual guía la mirada hacia lo importante. Se construye con:
- **Tamaño**: lo grande atrae primero.
- **Color**: la saturación alta sobre fondo neutro destaca.
- **Posición**: el ojo occidental lee de arriba a la izquierda.
- **Contraste**: la diferencia fondo–figura dirige la atención.
- **Espacio en blanco**: da respiro y define bloques.

### 7.3 Consistencia y simplificación

La consistencia en símbolos, colores y tipografía permite al lector construir un modelo mental del gráfico y mantenerlo. El ruido visual (elementos decorativos sin función) consume capacidad de procesamiento sin aportar información.

### 7.4 Para profundizar

- Wilke, cap. 4: *Color scales* y cap. 23: *Balance the data and context*.
- Tufte: concepto de *data-ink ratio* y *chartjunk* en *The Visual Display of Quantitative Information*, cap. 4.
- ColorBrewer 2.0. 🌐 [colorbrewer2.org](https://colorbrewer2.org)
- Zeileis, A. et al. (2020). *colorspace: A Toolbox for Manipulating and Assessing Colors and Palettes*. JSS, 96(1). 🌐 [doi:10.18637/jss.v096.i01](https://doi.org/10.18637/jss.v096.i01)

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
1. ¿Quién la va a leer? (audiencia y contexto)
2. ¿Qué decisión o comprensión debe producir? (propósito)

La respuesta define el nivel de detalle, el tipo de gráfico y el grado de interactividad necesarios.

### 8.3 Para profundizar

- Munzner, cap. 3: *Why: Task Abstraction* — taxonomía formal de tareas analíticas.
- Knaflic, *Storytelling with Data*, cap. 1: *The importance of context*.
- Few, S. *Show Me the Numbers*, cap. 2.

---

## 9. Tipos de gráficos

### 9.1 Gráficos analíticos principales

| Gráfico | Mejor para | Precaución |
|---|---|---|
| **Barras** | Comparar magnitudes entre categorías | No truncar el eje Y |
| **Líneas** | Mostrar tendencia temporal | Solo conecta puntos ordenados en tiempo |
| **Dispersión** | Mostrar correlación entre dos variables cuantitativas | Distinguir correlación de causalidad |
| **Histograma** | Distribución de una variable continua | El ancho del bin afecta la percepción |
| **Caja y bigotes** | Distribución + outliers + comparación entre grupos | La audiencia necesita saber leerlo |
| **Mapa de calor** | Patrones en matrices de datos | Color secuencial o divergente según el caso |
| **Área apilada** | Composición acumulada en el tiempo | Dificulta comparar partes intermedias |

### 9.2 Gráficos para ciencia de datos e IA

Específicos para el trabajo en esta carrera:

- **Curva ROC / AUC**: evaluar clasificadores binarios.
- **Matriz de confusión**: visualizar errores de clasificación.
- **Gráfico de importancia de características**: interpretar modelos de árbol o SHAP.
- **Proyecciones de alta dimensión** (t-SNE, UMAP): explorar embeddings y clusters.
- **Banda de confianza / intervalo de predicción**: representar incertidumbre en regresión.
- **Violin plot**: alternativa más rica al boxplot para distribuciones.

### 9.3 Diagramas de proceso y gestión

Estos no son gráficos de datos pero son herramientas visuales importantes:
Diagrama de flujo, mapa mental, Ishikawa, Pareto, Gantt, línea de tiempo, Venn, mapa de stakeholders, journey map, blueprint de servicio, arquitectura, UML, Kanban.

> **Distinción clave**: los gráficos analíticos describen datos. Los diagramas de proceso representan relaciones, secuencias o estructuras. No son intercambiables.

### 9.4 Para profundizar

- Wilke, cap. 5–16: cubre cada tipo de gráfico con criterio de uso y ejemplos.
- Munzner, cap. 7–12: taxonomía de representaciones visuales.
- Chart Chooser (Juice Analytics). 🌐 Diagrama de decisión gratuito.
- Schwabish, J. *Better Data Visualizations*. Oxford University Press, 2021.

---

## 10. Errores comunes en codificación visual

### 10.1 Lista de verificación negativa

Antes de publicar una visualización, comprobar que no incurre en:

- [ ] Eje Y truncado en gráfico de barras (exagera diferencias).
- [ ] Gráfico de pastel con más de 4–5 categorías.
- [ ] Comparación de áreas cuando las longitudes serían más precisas.
- [ ] Colores sin función analítica (decorativos).
- [ ] 3D aplicado sin necesidad real.
- [ ] Barras desordenadas cuando hay un orden natural o relevante.
- [ ] Demasiadas categorías de forma (más de 5–6 símbolos distintos).
- [ ] Doble eje Y con escalas incompatibles que sugieren relaciones falsas.
- [ ] Escala logarítmica sin indicarlo explícitamente.

### 10.2 Para profundizar

- Tufte, cap. 2: *Graphical Integrity* — análisis de gráficos reales engañosos.
- Cairo, A. *How Charts Lie*, cap. 2–4.
- Wilke, cap. 17: *Redundant coding* y cap. 26: *Don't go 3D*.

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

- **ggplot2**: gramática de gráficos (Grammar of Graphics). Muy usado en investigación.
- **ggplotly**: convierte gráficos de ggplot2 en interactivos.

### 11.3 JavaScript / Web

- **D3.js**: máxima flexibilidad para visualización interactiva en navegador. Curva de aprendizaje alta.
- **Vega-Lite**: especificación declarativa de alto nivel construida sobre D3.

### 11.4 Herramientas de business intelligence

- **Tableau**: análisis y dashboards interactivos para grandes volúmenes de datos.
- **Power BI** (Microsoft): integración con fuentes corporativas y Excel.
- **Looker / Google Looker Studio**: análisis en la nube, gratis para proyectos pequeños.

### 11.5 Para profundizar

- Documentación oficial de Matplotlib. 🌐 [matplotlib.org](https://matplotlib.org)
- Documentación oficial de Seaborn. 🌐 [seaborn.pydata.org](https://seaborn.pydata.org)
- Documentación oficial de Plotly. 🌐 [plotly.com/python](https://plotly.com/python)
- Documentación oficial de Altair. 🌐 [altair-viz.github.io](https://altair-viz.github.io)
- Wickham, H. *ggplot2: Elegant Graphics for Data Analysis*, 3ª ed. 🌐 [ggplot2-book.org](https://ggplot2-book.org)
- Murray, S. *Interactive Data Visualization for the Web*, 2ª ed. O'Reilly, 2017. (D3.js)
- VanderPlas, J. *Python Data Science Handbook*, cap. 4. 🌐 [jakevdp.github.io/PythonDataScienceHandbook](https://jakevdp.github.io/PythonDataScienceHandbook/)

---

## 12. Geovisualización

### 12.1 Definición

La geovisualización aplica los principios de visualización al análisis de datos espaciales. Su base conceptual proviene de la cartografía, los sistemas de información geográfica (SIG) y el visual analytics.

### 12.2 Proyecciones cartográficas

Toda proyección convierte la superficie esférica de la Tierra en un plano, introduciendo distorsiones en área, forma, distancia o dirección. La selección depende del objetivo:

- **Mercator**: preserva ángulos (navegación), distorsiona áreas.
- **Robinson / Winkel Tripel**: compromiso entre distorsiones para mapas del mundo.
- **Albers / Lambert**: preserva áreas para mapas regionales o nacionales.

### 12.3 Tipos de mapa temático

| Tipo | Cuándo usarlo |
|---|---|
| **Coroplético** | Valor normalizado por área o población (ej: % desempleo por estado) |
| **Burbuja / Proporcional** | Magnitud absoluta (ej: número total de casos) |
| **De puntos** | Distribución espacial de eventos individuales |
| **De flujo** | Movimiento entre orígenes y destinos |
| **De calor (heatmap espacial)** | Densidad de eventos sobre una superficie |

### 12.4 Mapas interactivos

La geovisualización moderna permite exploración dinámica: zoom, filtros por región, capas dinámicas e interacción en tiempo real. El mapa puede operar como una interfaz analítica completa.

### 12.5 Para profundizar

- Wilke, cap. 15: *Visualizing geospatial data*.
- Dorling, D. y Fairbairn, D. *Mapping: Ways of Representing the World*. Addison Wesley, 1997.
- Geopandas documentation. 🌐 [geopandas.org](https://geopandas.org)
- Kepler.gl — herramienta de geovisualización en el navegador. 🌐 [kepler.gl](https://kepler.gl)
- Deck.gl — visualización geoespacial de grandes datos. 🌐 [deck.gl](https://deck.gl)

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
- [ ] ¿Es accesible (contraste, paleta, alternativas)?
- [ ] ¿Es ética (sin escalas engañosas ni cherry-picking)?
- [ ] ¿Puede reproducirse con el mismo resultado?

### 13.3 Métodos de evaluación

- **Revisión experta** (heurística): una persona con experiencia revisa contra principios conocidos. Rápida y económica.
- **Prueba con usuarios**: personas reales intentan leer la visualización. Detecta problemas que el experto no ve.
- **Eye tracking**: registra el recorrido visual real del observador. Más costoso, pero muy revelador.

### 13.4 Para profundizar

- Munzner, cap. 4: *Analysis: Four Levels for Validation* — marco sistemático para evaluar diseños de visualización.
- Isenberg, T. et al. (2013). *A Systematic Review on the Practice of Evaluating Visualization*. IEEE TVCG, 19(12). [doi:10.1109/TVCG.2013.126](https://doi.org/10.1109/TVCG.2013.126)
- Nielsen, J. *10 Usability Heuristics* — aplicables a visualizaciones interactivas. 🌐 [nngroup.com/articles/ten-usability-heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)

---

## 14. Incertidumbre y límites del dato

### 14.1 El problema de los datos "perfectos"

Las introducciones suelen presentar la visualización como si los datos fueran exactos y completos. En la práctica, rara vez lo son. Ignorar la incertidumbre en la visualización puede llevar a decisiones mal informadas.

### 14.2 Fuentes de incertidumbre

- **Error de medición**: el instrumento o el proceso de recolección tiene un margen de error.
- **Variabilidad natural**: la variable fluctúa por razones fuera del modelo.
- **Datos faltantes**: hay observaciones no registradas.
- **Supuestos del modelo**: un modelo predictivo tiene intervalos de confianza que no son certeza.

### 14.3 Cómo representar incertidumbre visualmente

| Técnica | Cuándo usarla |
|---|---|
| **Barras de error** | Error estándar o desviación estándar de la media |
| **Bandas de confianza** | Intervalo de confianza en regresión o series de tiempo |
| **Intervalos de predicción** | Rango de valores esperados para observaciones futuras |
| **Transparencia / opacidad** | Reducir certeza visual de estimaciones más inciertas |
| **Múltiples líneas (ensemble)** | Mostrar el espacio de posibles trayectorias |
| **Nota textual explícita** | Aclarar fuente, fecha, tamaño de muestra y limitaciones |

### 14.4 Conexión con IA/CD

En modelos de machine learning, la incertidumbre es central:
- Los modelos de clasificación producen probabilidades, no certezas.
- Los modelos de regresión producen intervalos de predicción.
- Los modelos bayesianos producen distribuciones posteriores completas.
Visualizar esto correctamente es parte fundamental del trabajo del científico de datos.

### 14.5 Para profundizar

- Wilke, cap. 16: *Visualizing uncertainty*.
- Hullman, J. (2020). *Why Authors Don't Visualize Uncertainty*. IEEE TVCG, 26(1). [doi:10.1109/TVCG.2019.2934287](https://doi.org/10.1109/TVCG.2019.2934287)
- Kay, M. *ggdist* — biblioteca R para visualizar distribuciones e incertidumbre. 🌐 [mjskay.github.io/ggdist](https://mjskay.github.io/ggdist/)
- The Turing Way, sección *Reproducible Research*. 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app)

---

## 15. Visualización de modelos de machine learning *(tema prioritario para IA/CD)*

### 15.1 Por qué es fundamental en esta carrera

Esta es una de las conexiones más directas entre la materia de visualización y el resto de la carrera. Los modelos de ML producen outputs que son difíciles de interpretar sin representación gráfica. Visualizar un modelo no es lo mismo que graficar sus predicciones: implica entender qué aprendió, dónde falla y por qué toma ciertas decisiones.

### 15.2 Evaluación de clasificadores

**Curva ROC y AUC**
- Eje X: tasa de falsos positivos; eje Y: sensibilidad (TPR).
- AUC = área bajo la curva. Un clasificador aleatorio da AUC = 0.5.
- Permite comparar clasificadores independientemente del umbral de decisión.

**Matriz de confusión**
- Cuadrícula de clases reales vs. predichas.
- Mapa de calor para leerla visualmente.
- Derivados: precisión, recall, F1 por clase.

**Curva precisión–recall**
- Más informativa que ROC cuando las clases están desbalanceadas.

### 15.3 Interpretabilidad de modelos

**Importancia de características (feature importance)**
- En árboles y bosques aleatorios: medida de cuánto reduce la impureza cada variable.
- Gráfico recomendado: barras ordenadas de mayor a menor importancia.

**SHAP (SHapley Additive exPlanations)**
- Cuantifica la contribución de cada variable a la predicción de una instancia específica.
- *Summary plot*: dispersión de valores SHAP por variable.
- *Waterfall plot*: contribuciones para una instancia individual.
- *Dependence plot*: relación entre el valor de una variable y su SHAP value.

**LIME (Local Interpretable Model-agnostic Explanations)**
- Aproxima localmente el comportamiento del modelo con un modelo simple.

### 15.4 Exploración de espacios de alta dimensión

Los embeddings (Word2Vec, BERT, representaciones latentes) no pueden visualizarse directamente. Las técnicas de reducción de dimensionalidad permiten proyectarlos:

| Técnica | Uso | Precaución |
|---|---|---|
| **PCA** | Visualización rápida, interpretable | Solo captura varianza lineal |
| **t-SNE** | Exploración de clusters | Hiperparámetros afectan mucho el resultado |
| **UMAP** | Más rápido que t-SNE, preserva estructura global | Resultado depende de hiperparámetros |

> **Importante**: t-SNE y UMAP son herramientas exploratorias. Las distancias entre clusters no son directamente comparables. No concluir similitud o diferencia solo por proximidad en el mapa.

### 15.5 Visualización del entrenamiento

- **Curva de aprendizaje**: loss y métrica en entrenamiento vs. validación por época. Permite detectar overfitting y underfitting.
- **Curva de validación**: métrica vs. valor de hiperparámetro. Útil para tuning.

### 15.6 Para profundizar

- Lundberg, S. M. y Lee, S. I. (2017). *A Unified Approach to Interpreting Model Predictions*. NeurIPS 2017. 🌐 [arxiv.org/abs/1705.07874](https://arxiv.org/abs/1705.07874)
- SHAP library documentation. 🌐 [shap.readthedocs.io](https://shap.readthedocs.io)
- Molnar, C. *Interpretable Machine Learning*, 2ª ed. 🌐 [christophm.github.io/interpretable-ml-book](https://christophm.github.io/interpretable-ml-book)
- Scikit-learn: visualización de métricas de clasificación. 🌐 [scikit-learn.org/stable/visualizations.html](https://scikit-learn.org/stable/visualizations.html)
- McInnes, L. et al. (2018). *UMAP: Uniform Manifold Approximation and Projection*. 🌐 [arxiv.org/abs/1802.03426](https://arxiv.org/abs/1802.03426)
- Wattenberg, M. et al. (2016). *How to Use t-SNE Effectively*. Distill. 🌐 [distill.pub/2016/misread-tsne](https://distill.pub/2016/misread-tsne/)

---

## 16. Storytelling con datos

### 16.1 Qué aporta

El storytelling organiza la información para que una audiencia comprenda qué ocurre, por qué importa y qué puede hacerse. Convierte la visualización en herramienta de comunicación, no solo de exploración.

### 16.2 Estructura narrativa básica

1. **Contexto**: ¿qué problema o pregunta motiva el análisis?
2. **Tensión**: ¿qué revelan los datos que no era evidente?
3. **Resolución**: ¿qué conclusión o acción se desprende?

### 16.3 Principio de equilibrio

La historia debe apoyar la evidencia, no sustituirla. Cuando la narrativa se adelanta a los datos, la visualización pierde rigor y puede convertirse en persuasión disfrazada de análisis.

### 16.4 Para profundizar

- Knaflic, C. N. *Storytelling with Data*. Wiley, 2015. Cap. 1–3 y 6.
- Dykes, B. *Effective Data Storytelling*. Wiley, 2019.
- Segel, E. y Heer, J. (2010). *Narrative Visualization: Telling Stories with Data*. IEEE TVCG, 16(6). [doi:10.1109/TVCG.2010.179](https://doi.org/10.1109/TVCG.2010.179)

---

## 17. Reproducibilidad en visualización

### 17.1 Importancia

Una visualización es parte del trabajo científico y debe poder reconstruirse. La reproducibilidad evita inconsistencias entre versiones y facilita la colaboración.

### 17.2 Prácticas recomendadas

- Usar scripts o notebooks (Jupyter, R Markdown, Quarto) en lugar de herramientas de apuntar-y-hacer-clic.
- Guardar los datos originales y los datos procesados en archivos separados.
- Documentar paletas de color, rangos de ejes y filtros aplicados.
- Versionar el código con Git.
- Separar visualizaciones de exploración de las de comunicación final.

### 17.3 Para profundizar

- The Turing Way, capítulo *Reproducible Research*. 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app)
- Quarto — sistema de publicación reproducible para Python y R. 🌐 [quarto.org](https://quarto.org)
- Wilson, G. et al. (2017). *Good Enough Practices in Scientific Computing*. PLOS Computational Biology. 🌐 [doi:10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510)

---

## 18. Lista de verificación de calidad (resumen)

Antes de cerrar una visualización:

| Criterio | Verificado |
|---|---|
| Se entiende el mensaje en menos de 10 segundos | ☐ |
| El foco es claro y no hay elementos que compitan con él | ☐ |
| El canal visual corresponde a la jerarquía de Cleveland–McGill | ☐ |
| El color tiene función analítica, no decorativa | ☐ |
| No hay ruido visual innecesario | ☐ |
| Está alineada con la tarea o pregunta analítica | ☐ |
| Es accesible (paleta, contraste, alternativas textuales) | ☐ |
| Es ética (sin escalas engañosas, sin cherry-picking) | ☐ |
| Representa o declara la incertidumbre cuando existe | ☐ |
| Puede reproducirse con el mismo resultado | ☐ |

---

## 19. Ruta de profundización recomendada

Para el perfil de esta carrera, el orden sugerido es:

1. **Fundamentos y propósito** — Wilke caps. 1–2; Munzner cap. 1.
2. **Tipos de datos** — Munzner cap. 2; Wickham & Grolemund cap. 3.
3. **Codificación visual y jerarquía de Cleveland–McGill** — Munzner cap. 5; artículo Cleveland & McGill (1984).
4. **Percepción y Gestalt** — Ware, *Information Visualization*, cap. 5.
5. **Ética y accesibilidad** — Tufte cap. 2; Cairo, *How Charts Lie*; D'Ignazio & Klein cap. 3.
6. **Color y estilo** — Wilke cap. 4; ColorBrewer.
7. **Tipos de gráficos** — Wilke caps. 5–16; Munzner caps. 7–12.
8. **Herramientas** (Python / R) — documentación oficial de Seaborn, Plotly, ggplot2.
9. **Visualización de modelos ML** *(prioritario para la carrera)* — Molnar, *Interpretable ML*; SHAP docs.
10. **Incertidumbre** — Wilke cap. 16; Hullman (2020).
11. **Geovisualización** — Wilke cap. 15; Geopandas docs.
12. **Evaluación, storytelling y reproducibilidad** — Munzner cap. 4; Knaflic caps. 1–3; The Turing Way.

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

- Cleveland, W. S. y McGill, R. (1984). *Graphical Perception: Theory, Experimentation, and Application to the Development of Graphical Methods*. JASA, 79(387). [doi:10.2307/2288400](https://doi.org/10.2307/2288400)
- Heer, J. y Bostock, M. (2010). *Crowdsourcing Graphical Perception*. CHI 2010. 🌐 [idl.cs.washington.edu](https://idl.cs.washington.edu/papers/crowdsourcing-graphical-perception/)
- Hullman, J. y Diakopoulos, N. (2011). *Visualization Rhetoric*. IEEE TVCG, 17(12). [doi:10.1109/TVCG.2011.255](https://doi.org/10.1109/TVCG.2011.255)
- Hullman, J. (2020). *Why Authors Don't Visualize Uncertainty*. IEEE TVCG, 26(1). [doi:10.1109/TVCG.2019.2934287](https://doi.org/10.1109/TVCG.2019.2934287)
- Lundberg, S. M. y Lee, S. I. (2017). *A Unified Approach to Interpreting Model Predictions*. NeurIPS 2017. 🌐 [arxiv.org/abs/1705.07874](https://arxiv.org/abs/1705.07874)
- McInnes, L. et al. (2018). *UMAP: Uniform Manifold Approximation and Projection*. 🌐 [arxiv.org/abs/1802.03426](https://arxiv.org/abs/1802.03426)
- Segel, E. y Heer, J. (2010). *Narrative Visualization: Telling Stories with Data*. IEEE TVCG, 16(6). [doi:10.1109/TVCG.2010.179](https://doi.org/10.1109/TVCG.2010.179)
- Wattenberg, M. et al. (2016). *How to Use t-SNE Effectively*. Distill. 🌐 [distill.pub/2016/misread-tsne](https://distill.pub/2016/misread-tsne/)
- Wilson, G. et al. (2017). *Good Enough Practices in Scientific Computing*. PLOS CB. [doi:10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510)

### Recursos en línea permanentes

- ColorBrewer 2.0. 🌐 [colorbrewer2.org](https://colorbrewer2.org)
- Okabe–Ito Color Universal Design. 🌐 [jfly.uni-koeln.de/color](https://jfly.uni-koeln.de/color/)
- SHAP library documentation. 🌐 [shap.readthedocs.io](https://shap.readthedocs.io)
- The Turing Way. 🌐 [the-turing-way.netlify.app](https://the-turing-way.netlify.app)
- Quarto. 🌐 [quarto.org](https://quarto.org)
- Distill.pub — artículos de ML con visualizaciones interactivas. 🌐 [distill.pub](https://distill.pub)

---

*Documento generado para uso académico en la Licenciatura en Inteligencia Artificial y Ciencia de Datos. Versión 2.0 — Mayo 2026.*
