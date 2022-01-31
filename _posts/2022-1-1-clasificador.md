---
layout: post
title: Clasificador
published: true
---
## Introducción
Este es un trabajo para el curso de aprendizaje estadístico de la universidad Nacional de Colombia sede Medellín, cuyo objetivo es solucionar el problema de clasificar imágenes utilizando técnicas de aprendizaje estadístico. En el campo de clasificación de imágenes muchas veces es necesario identificar si la persona lleva puestos lentes o si no los lleva, las aplicaciones de estos modelos son de gran importancia,algunos ejemplos son: mecanismos de autenticación en servicios de pagos online, procesos de inicio de sesión, validación de métodos de pago, entre muchas otras.

## Dataset
Para el modelo, los datos fueron obtenidos de un problema existente en kaggle (Bueno, 2021). Los datos ya estaban organizados y separados por el tipo de imagen definiendo dos grupos, si la persona lleva o no lentes puestos. Estos datos son una profundización de un problema generado por (Heaton, 2020).

## Tratamiento de los datos
1.Se cargan las imágenes con una escala de colores gris, puesto que así necesitamos un poco menos de máquina para el procesamiento de los datos, las imágenes inicialmente quedan como muestra la figura 1:

![_config.yml]({{ site.baseurl }}/images/primer_img.jpeg)

2.Luego las imágenes se redimensionan para que queden todas con la misma dimensión de pixeles, en este caso usaremos 150px puesto que con esta dimensión no perdemos la calidad de las imágenes:

![_config.yml]({{ site.baseurl }}/images/segunda_img.jpeg)

3.Una vez se tienen las imágenes procesadas con la escala de grises y con el tamaño de 150px por 150px, las imágenes se verán de la siguiente manera:

- Para alguien con lentes veremos los datos como muestra la figura 3:

![_config.yml]({{ site.baseurl }}/images/tercer_img.jpeg)


- La figura 2 muestra como se verán los datos para las imagenes de personas sin lentes:

![_config.yml]({{ site.baseurl }}/images/cuarta_img.jpeg)


4.Como los datos están organizados por categoría se mezcla de forma aleatoria para así, evitar introducir al modelo cualquier patron de comportamiento.
Para terminar,se normalizan todos los datos excepto la variable de respuesta que toma valores únicamente de 0 y 1.


## Modelos sin datos aumentados

Inicialmente se proponen tres modelos y como es un problema de clasificación de imágenes el mejor método a usar son las redes neuronales convolucionales. Para iniciar haremos tres modelos sin datos aumentados de los cuales 1 es un modelo denso y los otros dos son modelos convolucionales:

### Modelo denso:
Este modelo tiene una capa de entrada que recibe los 22.500 pixeles, luego tiene dos capas densas con 200 neuronas cada una y finalmente la capa de salida, esta última capa debido al problema donde el resultado es si la personas lleva o no lleva lentes puestos tendrá únicamente una neurona de salida y usaremos la función sigmoid. Se usa esta función dado que sus valores de respuesta estan siempre entre 0 y 1.

### Modelo convolucional:
Este modelo tiene tres pares de capas convolucionales los cuales pasaran por 32, 64 y 128 filtros, luego tendrá una capa densa con 150 neuronas y finalmente la capa de salida que cumple con las mismas condiciones que para el modelo denso.



### Gráfico de precisión y perdida:
En la gráfica 1 para el modelo denso y en la grafica 2 para el modelo convolucional, podemos observar que la precision para ambos conjuntos es creciente con cada paso de la red. En la grafica 1 para el modelo denso podemos observar un comportamiento fluctuante tanto en presicion como en perdida, en la precision luego del paso 70 se alcanza el valor de 1 para el conjunto de entrenamiento lo que podria indicar un sobreajuste.

Para el modelo convolusional en la grafica 2, se alcanza identificar que la precision es igual a 1 en muy pocos pasos, lo que podria indicar que la red se esta aprendiendo los datos de memoria y que por ello es que necesita menos pasos para su aprendizaje, tambien, lo podemos confirmar con la perdida dado que para el conjunto de entrenamiento el error tiende a cero a medida que la red da mas pasos pero, el error del conjunto de validacion empieza a ser creciente luego de los 40 pasos.

![_config.yml]({{ site.baseurl }}/images/grafico_1.jpeg)


![_config.yml]({{ site.baseurl }}/images/grafico_2.jpeg)



## Modelos con datos aumentados

Ahora se proponen los mismos dos modelos, pero esta vez con datos aumentados, esto significa que se le realizaran modificaciones a las imágenes del conjunto de entrenamiento, tales como: rotaciones, inclinaciones, acercamientos, desplazamientos verticales y desplazamientos horizontales. 

las imagenes del conjunto de entrenamiento se ven como sigue:

![_config.yml]({{ site.baseurl }}/images/15_img.png)

y quedaran de la siguiente manera:

![_config.yml]({{ site.baseurl }}/images/16_img.png)


Para estos modelos se usaron las mismas reglas que los anteriores y el único cambio fue que se realizaron las modificaciones ya mencionadas sobre el conjunto de entrenamiento.

En la grafica 3 se puede observar que el modelo denso no tiene una mejora en la precisión ni en la perdida, ambas muestran una tendencia constante. En la precisión se puede observar una disminucion en el desempeño del conjunto de entrenamiento.

El comportamiento deseado se obtiene con el modelo convolucional en la grafica 4, donde se tiene que la precision de ambos conjuntos esta creciendo a la par y la perdida esta tendiendo a cero.


![_config.yml]({{ site.baseurl }}/images/grafico_3.jpeg)


![_config.yml]({{ site.baseurl }}/images/grafico_4.jpeg)



## Resultado conjunto de validacion [CMU Face Images Data Set](http://archive.ics.uci.edu/ml/datasets/cmu+face+images)

Teniendo en cuenta los resultados anteriores, se decide evaluar el desempeño de los dos con mejor precisión y menor pérdida, estos son el modelo  denso sin datos aumentados y el modelo convolucional con datos aumentados, teniendo en cuenta el conjunto de imágenes compartidas para realizar la evaluacion del modelo (siendo este un conjunto de validación aparte del de prueba) 
Los resultados se muestran a continuación: 
