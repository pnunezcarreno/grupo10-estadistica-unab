# Análisis Logístico y de Entregas en E-Commerce

**Universidad Andrés Bello (UNAB)** 
**Magíster en Ciencia de Datos e Inteligencia Artificial** 
**Curso:** MCD1501 - Estadística Computacional para la Toma de Decisiones  
**Grupo 10:** Jennifer Nilo, Patricio Núñez  

---

## Descripción del Proyecto

Este repositorio contiene el análisis estadístico progresivo de un conjunto de datos basado en la industria logística y de comercio electrónico (E-Commerce). El objetivo principal del proyecto es analizar factores operativos y comerciales para identificar qué variables inciden estadísticamente en la probabilidad de que un envío sufra un retraso en su entrega.

El proyecto se desarrolla en fases metodológicas incrementales:
1. **Fase Exploratoria e Inferencia Clásica (Sumativa 1):** Análisis descriptivo, pruebas de hipótesis tradicionales y detección inicial de anomalías distribucionales.
2. **Fase de Validación Computacional (Sumativa 2):** Aplicación de métodos de remuestreo computacional intensivo (Bootstrap, Permutaciones, Jackknife) y simulaciones probabilísticas (Monte Carlo) para validar los estimadores, superar los supuestos restrictivos de normalidad y evaluar el riesgo operativo real.

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
├── S1/
│   └── Sumativa1.ipynb          # Jupyter Notebook con el código Python, EDA e inferencia estadística (Evaluación Sumativa 1)
├── S2/
│   └── Sumativa2.ipynb          # Jupyter Notebook con el código Python, Validación, Simualación y Métodos de Remuestreo (Evaluación Sumativa 2)
├── S3/
│   └── Sumativa3.ipynb          # Jupyter Notebook con el código Python, Modelamiento Predictivo Integrado (Evaluación Sumativa 3)
│
└── README.md                    # Documentación del proyecto
```

## Dataset: Customer Analytics

El conjunto de datos utilizado corresponde a registros históricos de despachos de una empresa internacional que vende productos electrónicos. 
* **Variable a predecir:** `Reached.on.Time_Y.N` (Clasificación binaria: 1 = Retrasado, 0 = A tiempo).
* **Variables predictoras clave:** Peso del producto (`Weight_in_gms`), Costo del producto (`Cost_of_the_Product`), Descuento ofrecido (`Discount_offered`), Medio de envío (`Mode_of_Shipment`), entre otras.
* **Fuente:** [Kaggle - E-Commerce Shipping Data](https://www.kaggle.com/datasets/prachi13/customer-analytics)

## Principales Hallazgos (Validados Computacionalmente)

Tras someter los resultados iniciales a pruebas de estrés y simulaciones de remuestreo (10.000 iteraciones), se consolidan los siguientes descubrimientos estructurales:

1. **Variables Predictoras Clave:** El mapa de calor inicial evidenció que las relaciones lineales más fuertes respecto al retraso logístico provienen del **Descuento Ofrecido** ($r = 0.397$) y el **Peso del Paquete** ($r = -0.269$).
2. **Efecto de Compensación Comercial:** Mediante un test exacto de Permutación, se confirmó con irrefutable significancia estadística ($p = 0.0002$) que la empresa asigna mayores descuentos (Diferencia $\approx 13.12$) a los envíos que sufren retrasos. Esta política actúa como una medida reactiva de mitigación.
3. **Estabilidad Estructural:** El análisis con intervalos de confianza Bootstrap confirmó que la relación negativa entre el Peso de la carga y el Descuento ($r = -0.3761$) es robustamente estable. Los paquetes más livianos reciben sistemáticamente mayores compensaciones económicas.
4. **Riesgo Financiero Operativo:** A través de una simulación Monte Carlo, se dimensionó la variabilidad de la tasa de retrasos. Los resultados mostraron que el porcentaje de incumplimiento esperado se mantiene sumamente estable en un promedio del **59.67%**, reflejando un problema logístico estructural crónico en el modelo de distribución de la empresa.
5. **Robustez ante Valores Atípicos:** La aplicación del método Jackknife demostró que los descuentos extremos (de hasta \$65) no distorsionan la tendencia central (variabilidad máxima de $0.0058$). Representan operaciones reales de negocio, por lo que **no deben ser eliminados**, aunque requerirán escalamiento (`RobustScaler`) en fases predictivas.
6. **Preservación Multivariada en Faltantes:** Ante una pérdida simulada del 5% de los datos en el costo del producto (mecanismo MCAR), el uso de una imputación por regresión lineal múltiple demostró ser superior al reemplazo simple por la mediana. Este método avanzado logró restituir el tamaño completo de la muestra a 10.999 registros, protegiendo las correlaciones históricas y la estructura de covarianzas compartidas con las variables de peso y descuento.
7. **Resolución de Volatilidad por Bloques:** La transformación del peso de los paquetes desde una variable continua hacia una categoría binaria (con un punto de corte en los 4.000 gramos) resolvió de forma definitiva el vacío distributivo bimodal detectado en la Sumativa 1. Esta ingeniería de características purificó la señal predictiva del perfil de carga, impidiendo que el algoritmo trazara tendencias sobre sectores sin datos reales y evitando un subajuste operativo.
8. **Cuantificación del Impacto Logístico:** El análisis de los impactos comerciales confirmó al **Descuento Ofrecido** como el factor con mayor fuerza explicativa en el sistema: por cada unidad de incremento en el descuento escalado, las probabilidades (chances) de sufrir un retraso aumentan un 91,59% ($OR = 1.9159$), consolidando su naturaleza reactiva y compensatoria. En contraste, la **Carga Pesada** opera como un potente factor protector ($OR = 0.4602$), disminuyendo el riesgo de demora a menos de la mitad respecto a la paquetería menor.
9. **Ausencia de Distorsiones Estructurales:** Los diagnósticos econométricos ratificaron la validez y estabilidad del clasificador seleccionado. El Factor de Inflación de Varianza ($VIF = 1.0037$) descartó problemas de variables redundantes, mientras que el análisis de la Distancia de Cook (máximo de 0.0016) demostró que el modelo es inmune al sesgo por observaciones individuales. Asimismo, un remuestreo logístico de 1.000 iteraciones bootstrap confirmó que ningún intervalo de confianza al 95% incluye el valor cero.
10. **Eficacia y Mitigación Preventiva:** Evaluado en un conjunto de prueba independiente y oculto del 30%, el clasificador alcanzó una precisión del **72.18%** y un área bajo la curva ROC de 0.728. En el contexto estratégico del negocio, esta capacidad permite alertar y capturar de forma oportuna a 2 de cada 3 entregas rezagadas ($Recall = 68.26\%$), proporcionando una herramienta confiable para optimizar presupuestos logísticos y automatizar medidas de contingencia antes del despacho.

## Tecnologías y Reproducibilidad

El análisis fue desarrollado en Python. Para reproducir los resultados de manera local, asegúrate de tener instalado el siguiente stack tecnológico:

* **Línea Base y Operaciones:** `Python 3.x`
* **Manejo de Estructuras:** `pandas` (Manipulación, limpieza y reconstrucción de datos)
* **Cálculos y Generación Sintética:** `numpy` (Cálculos numéricos, álgebra lineal y fijación de semilla de aleatoriedad)
* **Inferencia Clásica y Computacional:** `scipy.stats` (Inferencia paramétrica, Pruebas t, Levene, Cohen's d y generadores de simulaciones)
* **Modelamiento y Regresión Logística:** `statsmodels` (`Logit`, `add_constant`, `variance_inflation_factor`) para extraer estadísticos de contraste y diagnóstico.
* **Preprocesamiento y Machine Learning:** `scikit-learn` (`LinearRegression`, `RobustScaler`, `train_test_split`, `metrics`).
* **Dashboard Visual:** `matplotlib` & `seaborn` (Generación de mapas de calor, matrices de confusión y curvas de rendimiento ROC).

**Instrucciones de ejecución:**
1. Clona este repositorio: `git clone https://github.com/pnunezcarreno/grupo10-estadistica-unab.git`
2. Asegúrate de que el archivo `Train.csv` se encuentre dentro de la carpeta `/data/`.
3. **Formativa 1:** Para las fases Fases 1 y 2 abre y ejecuta todas las celdas de `/notebook/Formativa1.ipynb` en tu entorno de Jupyter.
4. **Sumativa 1:** Para las fases Fases 1 y 2 abre y ejecuta todas las celdas de `/S1/Sumativa1.ipynb` en tu entorno de Jupyter Notebook.
5. **Sumativa 2:** Para la fase 3 abre y ejecuta todas las celdas de `/S2/Sumativa2.ipynb` en tu entorno de Jupyter Notebook.
6. **Sumativa 3:** Para la fase 4 abre y ejecuta todas las celdas de `/S3/Sumativa3.ipynb` en tu entorno de Jupyter Notebook.

---
*Desarrollado con fines académicos para la asignatura de Estadística Computacional - 2026.*