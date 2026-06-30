# Análisis Logístico y de Entregas en E-Commerce

**Universidad Andrés Bello (UNAB)** 
**Magíster en Ciencia de Datos e Inteligencia Artificial** 
**Curso:** MCD1501 - Estadística Computacional para la Toma de Decisiones  
**Grupo 10:** Jennifer Nilo, Patricio Núñez  

---

## Descripción del Proyecto

Este repositorio contiene el análisis estadístico exploratorio e inferencial de un conjunto de datos basado en la industria logística y de comercio electrónico (E-Commerce). El objetivo principal del proyecto es analizar factores operativos y comerciales para identificar qué variables inciden estadísticamente en la probabilidad de que un envío sufra un retraso en su entrega.

El análisis aplica técnicas de **Estadística Descriptiva**, estimación de **Intervalos de Confianza** y **Pruebas de Hipótesis** para fundamentar decisiones de negocio bajo incertidumbre.

## Estructura del Repositorio

El proyecto está organizado de la siguiente manera para garantizar su reproducibilidad:

```text
grupo10-estadistica-unab/
│
├── data/
│   └── Train.csv                # Dataset original (10.999 registros, 12 variables)
│
├── notebook/
│   └── Formativa1.ipynb         # Jupyter Notebook con el código en Python y el análisis completo (Evaluación Formativa 1)
│   └── Sumativa1.ipynb          # Jupyter Notebook con el código Python, EDA e inferencia estadística (Evaluación Sumativa 1)
│
└── README.md                    # Documentación del proyecto
```

## Dataset: Customer Analytics

El conjunto de datos utilizado corresponde a registros históricos de despachos de una empresa internacional que vende productos electrónicos. 
* **Variable a predecir:** `Reached.on.Time_Y.N` (Clasificación binaria: 1 = Retrasado, 0 = A tiempo).
* **Variables predictoras clave:** Peso del producto (`Weight_in_gms`), Costo del producto (`Cost_of_the_Product`), Descuento ofrecido (`Discount_offered`), Medio de envío (`Mode_of_Shipment`), entre otras.
* **Fuente:** [Kaggle - E-Commerce Shipping Data](https://www.kaggle.com/datasets/prachi13/customer-analytics)

## Principales Hallazgos (Insights)

A través del análisis ejecutado en el notebook, logramos identificar las siguientes conclusiones preliminares:

1. **Distribución Bimodal y Outliers:** El análisis de forma reveló que el peso de los paquetes tiene un comportamiento fuertemente bimodal (extremos muy livianos o muy pesados). Asimismo, se detectó mediante el método IQR un ~7.9% de valores atípicos en los descuentos ofrecidos, con una marcada asimetría positiva.
2. **Estimación Poblacional:** Mediante distribuciones asintóticas (TLC), estimamos con un 95% de confianza los parámetros operacionales de la empresa. Destaca la estimación de la proporción de retrasos, concluyendo que la **tasa de incumplimiento logístico oscila sistemáticamente entre el 58.7% y el 60.6%**.
3. **Asociación en Políticas Comerciales:** Previa comprobación de heterocedasticidad (Prueba de Levene), ejecutamos una **Prueba t de Welch**. Constatamos con alta significancia ($p \approx 0.0000$) y un tamaño de efecto grande (d de Cohen = 1.04) que la empresa entrega descuentos estadísticamente superiores a los paquetes retrasados (promedio de $15.33 vs $10.77). Esto evidencia el uso del descuento como compensación reactiva.
4. **Impacto Logístico del Peso:** Una segunda prueba de Welch comprobó que existe una diferencia significativa en el perfil de carga: la operación logística sufre mayores cuellos de botella y tasas de retraso al procesar cargas pertenecientes al segmento de menor peso relativo.

## Tecnologías y Reproducibilidad

El análisis fue desarrollado en Python. Para reproducir los resultados de manera local, asegúrate de tener instalado el siguiente stack tecnológico:

* `Python 3.x`
* `pandas` (Manipulación y limpieza de datos)
* `numpy` (Cálculos numéricos y fijación de semilla)
* `scipy.stats` (Inferencia, Pruebas t, Levene, Cohen's d)
* `matplotlib` & `seaborn` (Dashboard visual de datos)

**Instrucciones de ejecución:**
1. Clona este repositorio: `git clone https://github.com/pnunezcarreno/grupo10-estadistica-unab.git`
2. Asegúrate de que el archivo `Train.csv` se encuentre dentro de la carpeta `/data/`.
3. **Formativa 1:** Para las fases Fases 1 y 2 abre y ejecuta todas las celdas de `/notebook/Formativa1.ipynb` en tu entorno de Jupyter.
4. **Sumativa 1:** Para las fases Fases 1 y 2 abre y ejecuta todas las celdas de `/notebook/Sumativa1.ipynb` en tu entorno de Jupyter Notebook.

---
*Desarrollado con fines académicos para la asignatura de Estadística Computacional - 2026.*