# Exploring Behavioral Factors at NovaRetail+

🌐 [English](#english) | [Español](#español)

---

<a name="english"></a>
## 🇬🇧 English

A correlational (exploratory) analysis of which customer behavior factors are most associated with annual revenue.

### 1. Context / Problem
This was an individual project developed as part of the **TripleTen Data Analyst certificate program**. NovaRetail+ is an e-commerce platform in Latin America with millions of users. As of the close of 2024, the **Growth and Retention** team wanted to answer one question: **which customer behavior factors are most strongly associated with the annual revenue a customer generates?**

The dataset covered 15,000 customers with 12 variables, including monthly visits, monthly purchases, targeted ad spend, satisfaction, premium membership, churn, device type, region, and annual revenue (`ingreso_anual`). This was framed explicitly as a **correlational, exploratory** analysis — not a causal one.

### 2. My Contribution
I was responsible for the full analysis: data exploration and cleaning, documenting assumptions, visualizing relationships, calculating correlation coefficients, and translating the statistical findings into business interpretation.

### 3. Process and Decisions
- **Exploration and cleaning:** I reviewed the dataset's structure and data types first. The only correction needed was converting `edad` (age) from float to integer, since fractional ages weren't meaningful. Binary and categorical variables were already correctly typed.
- **Documenting assumptions:** Before running any correlation, I documented which coefficient fit each variable pair, since using the wrong one would have misrepresented the relationships: Pearson for linear numeric-to-numeric relationships, Spearman for monotonic ones, point-biserial for numeric-to-binary pairs, and Cramér's V for categorical-to-categorical associations. I also stated upfront that the analysis identifies relationships, not causality.
- **Heatmap before scatterplots:** I started with a full correlation heatmap to identify which variable pairs were actually worth investigating, rather than visualizing every possible pair from the start.
- **Skipping the general pairplot:** I generated a general scatterplot matrix (pairplot) but decided not to rely on it, since with this many variables it was hard to read and the heatmap had already surfaced the key pairs — so I moved directly to targeted scatterplots for `compras_mes` and `visitas_mes` against `ingreso_anual`.
- **Choosing the right coefficient per pair:** I applied Pearson to `compras_mes` vs. `ingreso_anual` (a near-linear relationship), Spearman to `visitas_mes` vs. `ingreso_anual` (weaker, less linear), point-biserial to `miembro_premium` and `abandono` against `ingreso_anual`, and Cramér's V to `region` vs. `tipo_dispositivo`.
- **Being explicit about limitations:** Given the very high correlation (0.97) between `compras_mes` and `ingreso_anual`, I flagged the possibility that both variables could be derived from the same underlying source, which would limit `compras_mes`'s value as an independent variable in any future model — rather than presenting the finding at face value.

### 4. Outcome / Learning
- `compras_mes` (monthly purchases) shows a very strong positive correlation with `ingreso_anual` (Pearson ≈ 0.97), making it close to a direct indicator of the revenue a customer generates.
- `visitas_mes` (monthly visits) shows a weaker, moderate positive correlation with `ingreso_anual` (Spearman ≈ 0.32) — visit frequency alone is not a reliable predictor of revenue.
- `miembro_premium` and `abandono` (churn) show a nearly null relationship with `ingreso_anual` (point-biserial), meaning premium status and churn status are not strong revenue signals on their own.
- `region` and `tipo_dispositivo` show virtually no association with each other (Cramér's V = 0.012).
- Key limitation identified: correlation does not imply causation, and `compras_mes`'s near-perfect correlation with `ingreso_anual` raises the possibility both are calculated from the same source — a caveat that should inform any modeling built on this finding.
- Recommended next steps: segment customers by revenue tier, run A/B tests to validate whether increasing visit or purchase frequency actually drives revenue, and explore non-linear relationships for variables like `satisfaccion` and `edad`.

### 5. Tools Used
- Python (pandas, NumPy, Seaborn, Matplotlib, SciPy)
- Jupyter Notebook

### 6. Evidence
- 📓 Analysis notebook (English version): see repository
- 📊 Heatmap and scatterplot visualizations: see repository

---
# Explorando factores de comportamiento en NovaRetail+

<a name="español"></a>
## 🇪🇸 Español

Un análisis correlacional (exploratorio) sobre qué factores del comportamiento de los clientes están más asociados con el ingreso anual.

### 1. Contexto / Problema
Este fue un proyecto individual desarrollado como parte del **certificado de Data Analyst de TripleTen**. NovaRetail+ es una plataforma de comercio electrónico en Latinoamérica con millones de usuarios. Para el cierre de 2024, el equipo de **Crecimiento y Retención** quería responder una pregunta: **¿qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual que genera un cliente?**

El dataset abarcaba 15,000 clientes con 12 variables, incluyendo visitas mensuales, compras mensuales, gasto en publicidad dirigida, satisfacción, membresía premium, abandono, tipo de dispositivo, región e ingreso anual (`ingreso_anual`). Se planteó explícitamente como un análisis **correlacional y exploratorio**, no causal.

### 2. Mi Contribución
Este fue un **proyecto individual**. Fui responsable de todo el análisis: exploración y limpieza de datos, documentación de supuestos, visualización de relaciones, cálculo de coeficientes de correlación y traducción de los hallazgos estadísticos en interpretación de negocio.

### 3. Proceso y Decisiones
- **Exploración y limpieza:** Primero revisé la estructura del dataset y los tipos de datos. La única corrección necesaria fue convertir `edad` de float a entero, ya que las edades fraccionarias no tenían sentido. Las variables binarias y categóricas ya estaban correctamente tipificadas.
- **Documentación de supuestos:** Antes de correr cualquier correlación, documenté qué coeficiente correspondía a cada par de variables, ya que usar el incorrecto habría distorsionado las relaciones: Pearson para relaciones lineales numérica-numérica, Spearman para relaciones monótonas, punto-biserial para pares numérica-binaria y V de Cramér para asociaciones categórica-categórica. También dejé claro desde el inicio que el análisis identifica relaciones, no causalidad.
- **Heatmap antes que scatterplots:** Comencé con un heatmap de correlación completo para identificar qué pares de variables valía la pena investigar, en lugar de visualizar todos los pares posibles desde el inicio.
- **Se descartó el pairplot general:** Generé una matriz de scatterplots general (pairplot), pero decidí no basarme en ella, ya que con esta cantidad de variables era difícil de leer y el heatmap ya había identificado los pares clave; por eso pasé directamente a scatterplots dirigidos de `compras_mes` y `visitas_mes` contra `ingreso_anual`.
- **Elección del coeficiente correcto por par:** Apliqué Pearson a `compras_mes` vs. `ingreso_anual` (relación casi lineal), Spearman a `visitas_mes` vs. `ingreso_anual` (más débil y menos lineal), punto-biserial a `miembro_premium` y `abandono` contra `ingreso_anual`, y V de Cramér a `region` vs. `tipo_dispositivo`.
- **Transparencia sobre las limitaciones:** Dada la correlación muy alta (0.97) entre `compras_mes` e `ingreso_anual`, señalé la posibilidad de que ambas variables se calculen a partir de la misma fuente, lo cual limitaría el valor de `compras_mes` como variable independiente en un futuro modelo, en lugar de presentar el hallazgo sin matices.

### 4. Resultado / Aprendizaje
- `compras_mes` (compras mensuales) muestra una correlación positiva muy fuerte con `ingreso_anual` (Pearson ≈ 0.97), siendo prácticamente un indicador directo del ingreso que genera un cliente.
- `visitas_mes` (visitas mensuales) muestra una correlación positiva más débil y moderada con `ingreso_anual` (Spearman ≈ 0.32); la frecuencia de visitas por sí sola no es un predictor confiable del ingreso.
- `miembro_premium` y `abandono` muestran una relación casi nula con `ingreso_anual` (punto-biserial), lo que significa que el estatus premium y el abandono no son señales fuertes de ingreso por sí solos.
- `region` y `tipo_dispositivo` no muestran prácticamente ninguna asociación entre sí (V de Cramér = 0.012).
- Limitación clave identificada: correlación no implica causalidad, y la correlación casi perfecta de `compras_mes` con `ingreso_anual` plantea la posibilidad de que ambas se calculen a partir de la misma fuente, una advertencia que debería considerarse en cualquier modelo basado en este hallazgo.
- Próximos pasos recomendados: segmentar clientes por nivel de ingreso, correr pruebas A/B para validar si aumentar la frecuencia de visitas o compras realmente impulsa el ingreso, y explorar relaciones no lineales en variables como `satisfaccion` y `edad`.

### 5. Herramientas Utilizadas
- Python (pandas, NumPy, Seaborn, Matplotlib, SciPy)
- Jupyter Notebook

### 6. Evidencias
- 📓 Notebook de análisis (versión en español): ver repositorio
- 📊 Visualizaciones de heatmap y scatterplots: ver repositorio
