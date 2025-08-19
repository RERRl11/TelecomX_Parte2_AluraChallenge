# Telecom X - Análisis y Predicción de Evasión de Clientes (Churn)

## Propósito del Análisis

El objetivo principal de este proyecto es realizar un análisis profundo sobre los datos de clientes de TelecomX para **predecir la probabilidad de que un cliente cancele (churn)** sus servicios. Identificando los factores más relevantes que influyen en esta decisión, buscamos proporcionar insights accionables para desarrollar estrategias de retención efectivas y reducir la pérdida de clientes.

## Estructura del Proyecto

Este repositorio contiene los siguientes archivos y directorios:

*   `TelecomX_Churn_Analysis.ipynb`: El cuaderno principal de Jupyter que contiene todo el código del análisis de datos, preprocesamiento, modelado predictivo y evaluación.
*   `TelecomX_Data_Procesados.csv`: El conjunto de datos tratado y utilizado para el análisis.
*   `./visualizaciones` (Opcional): Directorio para almacenar gráficos o figuras generadas durante el análisis exploratorio de datos (si se guardan como archivos).

## Proceso de Preparación de los Datos

El proceso de preparación de los datos fue crucial para adaptar el conjunto de datos original para el modelado predictivo. Las etapas clave incluyeron:

*   **Carga Inicial:** Se cargaron los datos desde el archivo `TelecomX_Data_Procesados.csv`.
*   **Clasificación de Variables:** Se identificaron variables **categóricas** (como `Servicio_Internet`, `Contrato`, `Metodo_Pago`) y **numéricas** (como `Antiguedad_Meses`, `Cargos_Mensuales`, `Cargos_Totales`).
*   **Limpieza:** Se eliminó la columna `ID_Cliente` por ser un identificador único sin valor predictivo.
*   **Codificación de Variables Categóricas:** Las variables categóricas se transformaron a un formato numérico utilizando **One-Hot Encoding** (`pd.get_dummies`) para que fueran compatibles con los algoritmos de machine learning.
*   **Escalado de Características Numéricas:** Se aplicó **Normalización (MinMaxScaler)** a las características numéricas seleccionadas para asegurar que estuvieran en una escala similar (entre 0 y 1). Esta etapa es importante para modelos sensibles a la escala como la Regresión Logística.
*   **Balanceo de Clases:** Para abordar el desbalance significativo en la variable objetivo (`Evasion`), se aplicó la técnica de **Sobremuestreo SMOTE (Synthetic Minority Over-sampling Technique)** para igualar el número de instancias en las clases mayoritaria y minoritaria.
*   **Separación de Datos:** El conjunto de datos balanceado se dividió en conjuntos de **entrenamiento** y **prueba** (80% entrenamiento, 20% prueba) para entrenar y evaluar los modelos de manera robusta.

## Justificaciones de las Decisiones de Modelado

Durante la fase de modelado, se tomaron las siguientes decisiones:

*   **Elección de Modelos:** Se seleccionaron dos modelos de clasificación: **Regresión Logística** (un modelo lineal de referencia, sensible a la escala) y **Random Forest** (un modelo de ensamble basado en árboles, menos sensible a la escala pero capaz de capturar interacciones no lineales). Esto permitió comparar diferentes enfoques.
*   **Evaluación de Modelos:** Los modelos se evaluaron utilizando métricas clave como **Exactitud (Accuracy)**, **Precisión**, **Recall**, **F1-score** y la **Matriz de Confusión**. Estas métricas son esenciales para entender el rendimiento del modelo, especialmente en un problema de clasificación donde el balance de clases fue un factor.
*   **Análisis de Importancia de Características (Random Forest):** Se utilizó la capacidad del modelo Random Forest para calcular la importancia de las variables. Esto ayudó a identificar los principales impulsores de la evasión.

## Insights del Análisis Exploratorio de Datos (EDA) y Visualizaciones

El análisis exploratorio de datos reveló varios insights clave sobre la evasión de clientes, visualizados a través de gráficos:

*   La proporción de clientes que evaden es significativamente menor que la de los que no evaden (desbalance de clases inicial).
*   **La Antigüedad del cliente** está negativamente correlacionada con la evasión: los clientes más antiguos son menos propensos a cancelar (ver boxplot de `Antiguedad_Meses` vs `Evasion`).
*   **Los Cargos Totales y Mensuales/Diarios** también mostraron relaciones importantes con la evasión (ver boxplots y análisis de correlación).
*   El **Tipo de Contrato** es un factor muy influyente. Los clientes con contratos **mensuales** tienen una tasa de evasión considerablemente más alta que aquellos con contratos a largo plazo (ver gráfico de barras apiladas de `Contrato` vs `Evasion`).
*   El **Servicio de Internet (Fibra Óptica)** y el **Método de Pago (Cheque Electrónico)** también mostraron una relación positiva con la evasión (ver gráficos de barras apiladas).