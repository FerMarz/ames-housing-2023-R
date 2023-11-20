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

### Distribución de precio de venta

![distribucion_precio_venta](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/88eee6fe-f4cc-413e-aea9-44260275dd6a)

Se realizó una gráfica de barras para observar la tendencia de los precios de las casas disponibles en el mercado.

### Gráfica de dispersión del área del garage vs. precio de venta

![precio_venta_area_garage](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/913a2787-f6ed-48b2-b455-b0c7783fafc7)

Se realizó una gráfica de dispersión entre el precio de venta y el área del garage. Se observaron muchas propiedades con un valor 0 en el área de garage al no disponer del mismo.

### Gráfica de dispersión del área de vivienda vs. el precio de venta y su regresión lineal

![SalePrice_Gr Liv Area](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/419ef8bc-650a-4e39-9af8-b5ee8d151ece)

Se hizo una gráfica para comparar el precio de las viviendas con el área total de cada una. Se observó una relación positiva entre ambos factores y un evidente aumento del precio en relación al tamaño de la propiedad.

### Matriz de correlación

![matriz_correlacion_procesado](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/e425871f-49fe-4cbe-8fd0-fcfbff46b0ab)

Se realizó una matriz de correlación con todas las columnas para identificar aquellas con una relación fuerte con el precio de venta.

### Matriz de correlación de variables con coeficientes mayores a 0.5 y menores a -0.5

![matriz_correlacion_alta](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/3a851e3a-0571-4124-a4a5-56d35938bb40)

Se realizó una matriz de correlación usando un filtro para solo observar aquellas relaciones con un valor mayor a 0.5 y menor a -0.5. Estas variables son buenos predictores para nuestro modelo.

### Matriz de correlación de las variables con coeficientes altos en relación al precio de venta

![matriz_correlacion_procesado2](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/58d15914-8e05-418c-b9de-4c3e3be4ad6e)

A partir de la primer matriz de correlación, se eligieron las características más importantes para realizar una tercera matriz de correlación y así identificar aquellas con coeficientes de Pearson altos relacionados al precio de venta.

## Preprocesamiento de datos
Este paso es crucial para preparar la base de datos para el análisis y modelado. Incluye la limpieza de datos, donde corregimos o eliminamos registros erróneos o irrelevantes; la imputación, donde reemplazamos los datos faltantes con valores sustitutos; la codificación de variables categóricas para convertirlas en formatos numéricos que los modelos puedan interpretar; la normalización o estandarización de rangos de datos para que tengan una escala común, facilitando así la convergencia en algoritmos de aprendizaje automático. Todos los procesos mejoran la eficiencia computacional y la interpretación de los resultados.

![Datos_faltantes_por_columna](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/c5397dbb-192f-4293-84ce-5001264a3423)

Se contó el número de datos faltantes en cada una de las columnas de la base de datos y se realizó una gráfica de barras para identificar aquellas columnas con la mayor información faltante.

## Creación de conjuntos de entrenamiento y prueba
Este proceso implica la división de la base de datos en dos segmentos distintos: un conjunto de entrenamiento y un conjunto de prueba. Hemos asignado el 70% de los datos al conjunto de entrenamiento, que se utilizará para construir y afinar nuestros modelos de aprendizaje automático. El restante 30% constituye el conjunto de prueba, que emplearemos para evaluar el rendimiento y la generalización de los modelos en datos no vistos anteriormente. Esta división estratégica es esencial para evitar el sobreajuste y asegurar que los modelos tengan una capacidad predictiva robusta en condiciones reales.

Los conjuntos que hemos creado se encuentran en [Train test](https://github.com/FerMarz/ames-housing-2023/blob/main/data/AmesHousing_train_set.csv) y 
[Test Set](https://github.com/FerMarz/ames-housing-2023/blob/main/data/AmesHousing_test_set.csv) ubicados en nuestro repositorio de Github.

## Busqueda de hiperparámetros usando "grid search" con validación cruzada para el modelo xgboost
Este paso es fundamental para optimizar el rendimiento del modelo XGBoost. Consiste en emplear la técnica de "Grid Search", que explora sistemáticamente una gama de valores de hiperparámetros para determinar la combinación óptima que produce el mejor resultado de predicción. Combinamos esto con la validación cruzada, un método que divide repetidamente el conjunto de datos en grupos de entrenamiento y validación para evaluar la estabilidad y la fiabilidad del modelo. Esta estrategia no solo mejora la precisión del modelo sino que también contribuye a prevenir el sobreajuste, asegurando que el modelo generalice bien a nuevos datos. La selección del tamaño de pliegues o "folds" es de 5.

La métrica del error es la Raíz del Error Cuadrático Medio o (RECM). En las siguientes imágenes, los mejores valores de los hiperparámetros estan de color naranja.

### Paso 1: búsqueda del mejor valor para `learning_rate` o tasa de aprendizaje
![Paso 1](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/1b56e40b-4372-461c-83df-733351bde7da)

### Paso 2: búsqueda del mejor valor para parámetros individuales de los árboles
![Paso 2](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/f2fee1c8-d393-47b1-8b90-0261d6e7bb17)

### Paso 3: búsqueda de los valores de hyperparámetros de estocasticidad
![Paso 3](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/a4f09048-ef12-4e32-8111-0d8a0eb2f308)

### Paso 4: búsqueda de hyperparámetros de regularización
![Paso 4](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/ab0bf22e-e9a0-4eac-b4ad-5baea5b94765)

### Paso 5: volver a hacer una búsqueda de la tasa de aprendizaje
![Paso 5](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/eb8b6658-1c9b-4229-8d70-48e2c19f4b20)

## Entrenamiento final del modelo
Después de la búsqueda exhaustiva de hiperparámetros, los valores que minimizan el error RECM (Raíz del Error Cuadrático Medio) son los siguientes:

    learning_rate=0.02
    max_depth=4
    min_child_weight=3
    subsample=0.7
    colsample_bytree=0.3
    reg_alpha=1000
    reg_lambda=1

El modelo XGBoost fue entrenado utilizando un total de `15,000` estimadores. La mejor generalización se logró en el estimador número `2,658`, donde el valor mínimo del RMSE (Raíz del Error Cuadrado Medio) para el conjunto de prueba fue aproximadamente `$23,482.77`, aproximadamente. Eso quiere decir que las predicciones de los precios de venta tienen un error promedio de 23 mil dólares. Esto es un error pequeño para un promedio de `$180,796.00`.

![GraficaDeRECM](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/26eea143-ecae-4c3e-a8ac-62d93a835e22)

La grafica muestra que existe sobreentrenamiento, sin embargo, podemos ver que no explota, sino que el modelo xgboost mantiene decentemente los valores de error para el conjunto de validación. COn una parada temprana, el modelo puede generalizar muy bien en los `2,658` estimadores.

## Resultados y conclusiones

En una gráfica de importancia con XGBoost utilizando ganancia y cover, la ganancia evalúa cuánto mejora la precisión al dividir los datos según una característica, indicando su importancia. Por otro lado, el cover mide cuántos datos afecta una característica al realizar una división. Una gráfica de importancia de características basada en la frecuencia en XGBoost ilustra la relevancia relativa de cada característica según la frecuencia con que se emplean para tomar decisiones durante el entrenamiento del modelo. Características con una alta frecuencia de uso se presentan como destacadas en la visualización.

### Gráfica de importancia según el valor `gain`.
![matriz_importancia1](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/21a42e44-05a5-4214-8a5f-19f1167010df)

La gráfica ilustra la importancia relativa de cada característica, representando en el eje X las características y en el eje Y la ganancia o el valor de gain.

### Gráfica de importancia según el valor `cover`.

![matriz_importancia2](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/fd3b39fb-85c3-4672-b7ff-3e878a1bcfd4)

La gráfica ilustra la importancia relativa de cada característica, representando en el eje X las características y en el eje Y la ganancia o el cover.

### Gráfica de importancia según el valor `frecuencia`.

![matriz_importancia3](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/ab57ead7-4787-4b6f-83ab-3658545dda22)

La gráfica ilustra la importancia relativa de cada característica, representando en el eje X las características y en el eje Y la ganancia o el frecuencia.

### Afirmación de nuestra hipótesis inicial

La hipótesis inicial planteada sostenía que las variables `Ground Living Area` y `Garage Area` representaban los predictores más significativos en el modelo, basándose en los resultados obtenidos de la matriz de correlación. Tras la fase de entrenamiento con XGBoost y el consecuente análisis de la importancia de las características, los datos respaldaron dicha hipótesis. Las métricas de importancia, incluyendo frecuencia, cover y gain, indicaron consistentemente que "Ground Living Area" y "Garage Area" eran las características preponderantes en la realización de divisiones dentro de los árboles de decisión. Estos hallazgos no solo validan nuestra hipótesis sino que también reafirman el valor predictivo de estas variables en el modelo, subrayando su capacidad para mejorar la generalización y optimizar la precisión de las predicciones del modelo.

## Creación de la idea del producto y marca

Nuestra idea del producto se puede ver en la siguiente liga de nuestra presentación: [enlace público de la presentación del producto](https://www.canva.com/design/DAF0lFDI_78/irClYSgIi2-MPTbXKeqJQA/view?utm_content=DAF0lFDI_78&utm_campaign=designshare&utm_medium=link&utm_source=editor)

![HomePricerLogo](https://github.com/FerMarz/ames-housing-2023-R/assets/84693158/62c8f4dc-5355-4c22-b315-c41d97edaeaf)

## Información de contacto

Fermín Martínez: fer.marz.py@gmail.com
Gustavo Lino: glino092@gmail.com
Sergio Saavedra: checonidas92@gmail.com
