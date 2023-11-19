# Home Pricer AI

![HomePricerLogo](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/62c8f4dc-5355-4c22-b315-c41d97edaeaf)

# Estudio de base de datos Ames Housing 2023 usando R 
Este repositorio se centra en el análisis y desarrollo de modelos de Machine Learning utilizando XGBoost para predecir los precios de la vivienda en Ames, Iowa. Predecir los precios de bienes raíces es crucial en el mercado de la vivienda, y el objetivo principal de esta investigación es explorar y refinar modelos de aprendizaje automático para mejorar la precisión de estas predicciones.

El estudio se realizó usando herramientas del lenguaje R.

# Introducción

## Contexto y Relevancia del Conjunto de Datos
El conjunto de datos de Ames Housing, derivado de las ventas de viviendas en Ames, Iowa, en 2011, ofrece una rica oportunidad para explorar las características del mercado inmobiliario. Proporciona una amplia gama de atributos (más de 70) que afectan al precio de venta de las viviendas, desde características físicas hasta consideraciones ambientales y de localización.

## Objetivo del Análisis
Nuestro proyecto apunta a utilizar XGBoost, un algoritmo de aprendizaje automático basado en árboles de decisión potenciado con gradient boosting, para predecir los precios de las viviendas en Ames, Iowa. Buscamos no solo realizar predicciones precisas sino también entender qué factores tienen mayor influencia en los precios de las viviendas.

## Metodología de XGBoost
XGBoost es conocido por su eficiencia, rendimiento y capacidad para manejar una gran variedad de tipos de datos. En nuestro análisis, aprovecharemos estas características para manejar el amplio espectro de variables del conjunto de datos de Ames Housing. Además, exploraremos cómo la optimización de hiperparámetros y la ingeniería de características pueden mejorar aún más la precisión del modelo.

## Aplicaciones y Beneficios Potenciales
Los resultados de este análisis pueden ser útiles para compradores y vendedores de viviendas, agentes inmobiliarios y urbanistas en Ames, proporcionando una herramienta para entender mejor los factores que influyen en los precios de las viviendas. Además, las metodologías desarrolladas podrían aplicarse a otros conjuntos de datos inmobiliarios, extendiendo su utilidad más allá del contexto específico de Ames, Iowa.

# Metodología del estudio
Nuestro estudio sigue el siguiente proceso:

1. Análisis de la base de datos original [AmesHousing_raw_data](https://github.com/FerMarz/ames-housing-2023/tree/main/data).
2. Preprocesamiento de datos.
3. Creación de conjuntos de entrenamiento y prueba.
4. Busqueda de hiperparámetros usando "grid search" con validación cruzada para el modelo xgboost.
5. Entrenamiento final del modelo.
6. Resultados y conclusiones.
7. Creación de la idea del producto y marca.

A continuación se describe cada proceso.

## Análisis de la base de datos original
Este proceso nos ayudará a examinar las estadísticas descriptivas para comprender la distribución de los datos, explorar las relaciones entre las variables, identificar si hay datos faltantes que requieran imputación, y determinar si es necesario reescalar los datos para técnicas de modelado específicas.

## Preprocesamiento de datos
Este paso es crucial para preparar la base de datos para el análisis y modelado. Incluye la limpieza de datos, donde corregimos o eliminamos registros erróneos o irrelevantes; la imputación, donde reemplazamos los datos faltantes con valores sustitutos; la codificación de variables categóricas para convertirlas en formatos numéricos que los modelos puedan interpretar; la normalización o estandarización de rangos de datos para que tengan una escala común, facilitando así la convergencia en algoritmos de aprendizaje automático. Todos los procesos mejoran la eficiencia computacional y la interpretación de los resultados.

## Creación de conjuntos de entrenamiento y prueba
Este proceso implica la división de la base de datos en dos segmentos distintos: un conjunto de entrenamiento y un conjunto de prueba. Hemos asignado el 70% de los datos al conjunto de entrenamiento, que se utilizará para construir y afinar nuestros modelos de aprendizaje automático. El restante 30% constituye el conjunto de prueba, que emplearemos para evaluar el rendimiento y la generalización de los modelos en datos no vistos anteriormente. Esta división estratégica es esencial para evitar el sobreajuste y asegurar que los modelos tengan una capacidad predictiva robusta en condiciones reales.

## Busqueda de hiperparámetros usando "grid search" con validación cruzada para el modelo xgboost
Este paso es fundamental para optimizar el rendimiento del modelo XGBoost. Consiste en emplear la técnica de "Grid Search", que explora sistemáticamente una gama de valores de hiperparámetros para determinar la combinación óptima que produce el mejor resultado de predicción. Combinamos esto con la validación cruzada, un método que divide repetidamente el conjunto de datos en grupos de entrenamiento y validación para evaluar la estabilidad y la fiabilidad del modelo. Esta estrategia no solo mejora la precisión del modelo sino que también contribuye a prevenir el sobreajuste, asegurando que el modelo generalice bien a nuevos datos. La selección del tamaño de pliegues o "folds" es de 5.

### 

![Paso 1](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/1b56e40b-4372-461c-83df-733351bde7da)
![Paso 2](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/f2fee1c8-d393-47b1-8b90-0261d6e7bb17)
![Paso 3](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/a4f09048-ef12-4e32-8111-0d8a0eb2f308)
![Paso 4](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/ab0bf22e-e9a0-4eac-b4ad-5baea5b94765)
![Paso 5](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/eb8b6658-1c9b-4229-8d70-48e2c19f4b20)

## Entrenamiento final del modelo


    learning_rate=0.02
    max_depth=4
    min_child_weight=3
    subsample=0.7
    colsample_bytree=0.3
    reg_alpha=1000
    reg_lambda=1



## Resultados y conclusiones


## Creación de la idea del producto y marca


