# <h1 align=center><span style="color:blue"> **MACHINE LEARNING** </span></h1>

## **Introducción**

En el presente proyecto nos propusimos crear un modelo, o modelos, de Machine Learning. Este tiene como objetivo poder predecir la categoría a la que pertenece un conjunto de inmuebles, según su precio. Las categorías iniciales son tres; low, high y medium. De aquí solo nos interesa saber que propiedades tienen un valor low y cuales no. Las métricas a utilizar para medir el desempeño de nuestro modelo son dos, *accuracy* y *recall*. 
<p>Para comenzar, contamos con dos datasets, uno de entrenamiento con algo más de 346.000 registros y otro de testeo con 38500, todos datos extraídos de una empresa inmoviliaria líder de los Estados Unidos. Para construir un modelo fiable fue necesario realizar tanto un trabajo de análisis exploratorio de datos, como un trabajo de transformación de estos.     
   
</p>
<hr>

**IMPORTANTE:** Los datasets del trabajo no se encuentran en el github del proyecto debido a su tamaño. Al final de este README compartimos el enlace desde donde pueden descargarse.

<hr>  

## **Desarrollo del proyecto**

### **EDA-ETL**

Luego de cargar nuestro set de entrenamiento, el primer paso fue realizar el análisis exploratorio de datos con el que intercalamos el proceso de ETL. A continuación listamos las herramientas utilizadas en esta etapa:

- Jupyter Notebook, como entorno de desarrollo
- Python, como lenguaje de programación
- Pandas, librería para carga, tratamiento general y guardado de datos
- Seaborn para análisis exploratorio y gráficas descriptivas
- Matplotlib para el ploteo de los gráficos
- Geopandas para análisis exploratorio de puntos geográficos
- Scipy, para el tratamiento de valores atípicos
- Sklearn, para binarizar columnas categóricas

Durante el proceso de análisis observamos estas anomalías: datos faltantes en algunos campos, distribución sesgada de los datos, presencia de valores atípicos, puntos geográficos que no pertenecían al territorio estadounidense.

En cuanto al tratamiento de valores faltantes tomamos uno de dos caminos, o bien eliminar las columnas, en los casos en que aquellos superaran el 20 % del total de registros, o bien eliminar las filas en los casos de una cantidad de valores nulos que no fuera representativo de la muestra. 

La presencia de valores atípicos fue abordada con el método de winsorización. En este mismo paso, quedó corregido el sesgo de la  distribución para cada uno de los campos tratados.

Por su parte, el tratamiento de puntos geográficos hechos con datos erróneos, aunque solo representaban un 0,07 % de los datos, constituía un buen desafío, por lo que tratamos la mayoría de ellos. Se puede encontrar una explicación del procedimiento utilizado en la notebook del proyecto, bajo el apartado "Puntos geográficos".

Lo siguiente que realizamos fue moldear la forma de nuestro data frame para que incluyera los campos que creíamos más relevantes. Aquí también fue importante el EDA dado que analizamos la correlación entre los distintos campos. Si bien esta vez solo dos campos mostraban una alta correlación (0,89 con Índice de Pearson), este paso es fundamental para evitar la introducción de ruido al modelo de ML. Eliminamos una de estas columnas, así como también columnas con datos descriptivos o categóricos. Además quitamos la columna de precios, ya que no se hallaba presente en el set de testeo.

La única columna categórica que no eliminamos fue la contenía los tipos de inmuebles, dado que decidimos realizar el método de One-hot Encoding sobre esta, de manera de tener un conjunto de campos numéricos que pudieran ser analizados por nuestro modelo.

Los pasos seguidos en el set de datos de testeo fueron prácticamente los mismos, a excepción de algunos puntos como el tratamiento y eliminación de la columna de precios, porque no existe tal columna en este dataset. Tampoco pudimos eliminar ningún registro, dado que el largo del dataset de testeo no podía ser modificado, es decir que todos los valores nulos o incorrectos fueron tratados.

### Creación de los modelos de Machine Learning

Una vez que tuvimos los dos dataframes con la misma estructura procedimos a crear un modelo de Regresión Logística, primero y un modelo de Random Forest, después, los entranamos y predijimos las categorías objetivos de un tercer dataset con datos reales. El segundo obtuvo mejores métricas(0.758 en recall, 0,782 en accuracy ), por lo que optamos quedarnos con este. 

Para esta etapa utilizamos:

- Sklearn, para la la creación, entrenamiento de los modelos y gráfica de curva de aprendizaje del modelo Random Forest

- Numpy para especificar los parámetros de los tamaños de las muestras de entrenamiento utilizados en la gráfica de curva de aprendizaje

##
<hr>

## **Puntos a mejorar**

Los siguientes son algunos puntos pensados para mejorar el proyecto a futuro:

1) Utilizar alguna libería como nltk para el tratamiento de texto del campo 'description'

2) Realizar un pipeline de Machine Learning



## **Sitios relacionados con el proyecto**

__Datasets__
-https://drive.google.com/drive/folders/1kLa8WhT0ZEgLY0gxemxaeWhbsuUw17f8?usp=sharing

__Repositorio Github__

- https://github.com/Diemale/Datathon
