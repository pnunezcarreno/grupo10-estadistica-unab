# 📦 Análisis Logístico y de Entregas en E-Commerce

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
│   └── Formativa1.ipynb         # Jupyter Notebook con el código en Python y el análisis completo según evaluación  de la Formativa 1
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

1. **Distribución Bimodal:** El peso de los paquetes despachados tiene un comportamiento atípico (concentración masiva en paquetes muy livianos y muy pesados, sin un rango intermedio fuerte).
2. **Estimación de Inventario:** Mediante la distribución t de Student, estimamos con un 95% de confianza que el costo promedio poblacional de los productos en tránsito es de $210.20 (± $0.90).
3. **Anomalía en Descuentos:** Se detectó un 8% de valores atípicos (outliers) en los descuentos ofrecidos a los clientes utilizando la regla del Rango Intercuartílico (IQR).
4. **Validación de Hipótesis:** Mediante una **Prueba t de Welch** (p-valor ≈ 0.0000) y el cálculo de la **d de Cohen**, comprobamos estadísticamente que la empresa entrega descuentos significativamente más altos a los paquetes retrasados. Esto sugiere que el descuento es una medida de "compensación" reactiva y que el área gerencial debe auditar la eficiencia de la cadena de suministro logística.

## Tecnologías y Reproducibilidad

El análisis fue desarrollado en Python. Para reproducir los resultados de manera local, asegúrate de tener instalado el siguiente stack tecnológico:

* `Python 3.x`
* `pandas` (Manipulación de datos)
* `numpy` (Cálculos numéricos)
* `scipy` (Inferencia estadística y pruebas de hipótesis)
* `matplotlib` & `seaborn` (Visualización de datos)

**Instrucciones de ejecución:**
1. Clona este repositorio: `git clone https://github.com/pnunezcarreno/grupo10-estadistica-unab.git`
2. Asegúrate de que el archivo `Train.csv` se encuentre dentro de la carpeta `/data/`.
3. Abre y ejecuta todas las celdas de `/notebook/Formativa1.ipynb` en tu entorno de Jupyter.

---
*Desarrollado con fines académicos para la asignatura de Estadística Computacional - 2026.*