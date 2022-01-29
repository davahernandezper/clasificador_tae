---
layout: post
title: Clasificador
published: true
---
## Introducción
Este es un trabajo para el curso de aprendizaje estadístico de la universidad Nacional de Colombia sede Medellín, cuyo objetivo es solucionar el problema de clasificar imágenes utilizando técnicas de aprendizaje estadístico. En el campo de clasificación de imágenes muchas veces es necesario identificar si la persona lleva apuestos lentes o si no los lleva, las aplicaciones que tiene lograr un modelo de estos son inmensas tales como: mecanismos de autenticación en servicios de pagos online, procesos de inicio de sesión, validación de métodos de pago, entre muchas otras.

## Dataset
Para el modelo los datos fueron basados en 
[https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images](https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images), que a su vez están basados en [https://www.kaggle.com/jeffheaton/glasses-or-no-glasses](https://www.kaggle.com/jeffheaton/glasses-or-no-glasses). Inicialmente los datos ya estaban organizados y separados por el tipo de imagen, que era si la persona lleva o no lleva lentes puestos.

## Tratamiento de los datos
1.Se cargan las imágenes con una escala de colores gris, puesto que así necesitamos un poco menos de máquina para el procesamiento de los datos, las imágenes inicialmente quedan de la siguiente manera:

> _Figura 1_

figura1![_config.yml]({{ site.baseurl }}/images/primer_img.png)

2.Luego las imágenes se redimensionan para que queden todas con la misma dimensión de pixeles, en este caso usaremos 150px puesto que con esta dimensión no perdemos la calidad de las imágenes:

![_config.yml]({{ site.baseurl }}/images/segunda_img.png)

3.Una vez se tienen las imágenes procesadas con la escala de grises y con el tamaño de 150px por 150px, las imágenes se verán de la siguiente manera:

- Para alguien con lentes:

![_config.yml]({{ site.baseurl }}/images/tercer_img.png)

Computacionalmente lo datos de la imagen anterior se verán como sigue, recordando que es una composición de pixeles que van de 0 a 255:

![_config.yml]({{ site.baseurl }}/images/cuarta_img.png)


- Para alguien sin lentes:

![_config.yml]({{ site.baseurl }}/images/5_img.png)


Y computacionalmente:

![_config.yml]({{ site.baseurl }}/images/6_img.png)

4.Como los datos están organizados por categoría, lo que se hace ahora es que queden de forma aleatoria y así el modelo no aprenderá que la mitad de los datos son de personas llevando lentes y la otra mitad no lleva lentes.

![_config.yml]({{ site.baseurl }}/images/7_img.png)

5.Para terminar lo que hacemos es que normalizamos todos los datos excepto la variable de respuesta que ya la tenemos únicamente como 0 y 1.

![_config.yml]({{ site.baseurl }}/images/8_img.png)

![_config.yml]({{ site.baseurl }}/images/9_img.png)


## Modelos sin datos aumentados

Inicialmente se proponen tres modelos y como es un problema de clasificación de imágenes el mejor método a usar son las redes neuronales convolucionales. Para iniciar haremos tres modelos sin datos aumentados de los cuales 1 es un modelo denso y los otros dos son modelos convolucionales:

### Modelo denso:
Este modelo tiene una capa de entrada que recibe los 22.500 pixeles, luego tiene dos capas densas con 200 neuronas cada una y finalmente la capa de salida, esta última capa debido al problema donde el resultado es si la personas lleva o no lleva lentes puestos tendrá únicamente una neurona de salida y usaremos la función sigmoid.

![_config.yml]({{ site.baseurl }}/images/10_img.png)


### Modelo convolucional:
Este modelo tiene tres pares de capas convolucionales los cuales pasaran por 32, 64 y 128 filtros, luego tendrá una capa densa con 150 neuronas y finalmente la capa de salida que cumple con las mismas condiciones que para el modelo denso.

![_config.yml]({{ site.baseurl }}/images/11_img.png)


### Modelo convolucional 2:
Este modelo tiene tres pares de capas convolucionales los cuales pasaran por 32, 64 y 128 filtros, luego tendrá un dropout cuya función es la de regularizar para reducir el sobreajuste de la red neuronal, continua con una capa densa con 150 neuronas y finalmente la capa de salida que cumple con las mismas condiciones que para los modelos anteriores.

![_config.yml]({{ site.baseurl }}/images/12_img.png)


### Grafico de precisión y perdida:
Para cada uno de los modelos anteriores podemos observar en la precisión que los datos de entrenamiento están creciendo demasiado rápido y llegando al valor 1, lo cual indica que estos modelos no son capaces de generalizar y que se aprenden los datos de memoria, esto se comprueba con la precisión de los datos de validación que en lugar de crecer antes están con tendencia hacia el 0.

Al mirar los gráficos de loss podemos observar que los datos de validación están creciendo en lugar de tener una tendencia hacia el cero, esto último nos comprueba que estos modelos no son capaces de generalizar y por lo tanto no son útiles en este ejercicio. Esto a pesar de que los datos de validación 'mejoraron' para los modelos convolucionales.

- Modelo denso

![_config.yml]({{ site.baseurl }}/images/denso.png)

- Modelo convolucional:

![_config.yml]({{ site.baseurl }}/images/cnn.png)

- Modelo convolucional 2:

![_config.yml]({{ site.baseurl }}/images/cnn2.png)


## Modelos con datos aumentados

Ahora se proponen los mismos tres modelos, pero esta vez con datos aumentados, esto significa que se le realizaran modificaciones a las imágenes del conjunto de entrenamiento, tales como: rotaciones, inclinaciones, acercamientos, desplazamientos verticales y desplazamientos horizontales. Para esto usamos el siguiente código:

![_config.yml]({{ site.baseurl }}/images/13_img.png)

![_config.yml]({{ site.baseurl }}/images/14_img.png)

las imagenes del conjunto de entrenamiento se ven como sigue:

![_config.yml]({{ site.baseurl }}/images/15_img.png)

y quedaran de la siguiente manera:

![_config.yml]({{ site.baseurl }}/images/16_img.png)


Para estos modelos se usaron las mismas reglas que los modelos anteriores y el único cambio fue que se realizaron las modificaciones ya mencionadas sobre el conjunto de entrenamiento, los resultados obtenidos son los siguientes:


- Modelo denso con datos aumentados:

![_config.yml]({{ site.baseurl }}/images/denso_AD.png)

- Modelo convolucional con datos aumentados:

![_config.yml]({{ site.baseurl }}/images/cnn_AD.png)

- Modelo convolucional 2 con datos aumentados:

![_config.yml]({{ site.baseurl }}/images/cnn2_AD.png)

Observando los gráficos anteriores podemos ver que el modelo denso continua siendo el menos indicado para el clasificador de imágenes dado que no es capaz de generalizar y con el aumento de datos pareciera que hasta en el conjunto de entrenamiento tiene dificultades para el aprendizaje. En cambio, en los modelos convolucionales si se obtienen resultados interesantes, ahora si se observa que la precisión de los conjuntos de validación está creciendo y que la perdida está bajando, aun así, no lo hacen de la misma manera que lo que el conjunto de entrenamiento y posiblemente esto se pueda mejorar.


## Modelos con datos aumentados, pero con muestra de validación diferente

Ahora se usa una técnica diferente, es posible que los resultados anteriores se deba a que el conjunto de validación usado es demasiado diferente al conjunto de entrenamiento que se usa, por ejemplo, el conjunto de entrenamiento solo tiene una fotografía para cada persona mientras que el conjunto de validación tiene diferentes tomas de la misma persona en diferentes ángulos o con diferentes lentes, es probable que esto este confundiendo al modelo y por eso su dificultad al generalizar, por lo que se opta por usar el 20% de los datos de entrenamiento como conjunto de validación:
