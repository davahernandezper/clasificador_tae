---
layout: post
title: Clasificador
published: true
---
## Introducción
Este es un trabajo para el curso de aprendizaje estadistico de la universidad Nacional de Colombia sede Medellín, cuyo objetivo es solucionar el problema de clasificar imágenes utilizando técnicas de aprendizaje estadístico. En el campo de clasificación de imagenes muchas veces es necesario identificar si la persona lleva apuestos lentes o si no los lleva, las aplicaciones que tiene lograr un modelo de estos son inmensas tales como: mecanismos de autenticación en servicios de pagos online, procesos de inicio de sesión, validacion de metodos de pago, entre muchas otras.

## Dataset
Para el modelo los datos fueron basados en 
[https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images](https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images), que a su vez estan basados en [https://www.kaggle.com/jeffheaton/glasses-or-no-glasses](https://www.kaggle.com/jeffheaton/glasses-or-no-glasses). Inicialmente los datos ya estaban organizados y separados por el tipo de imagen, que era si la persona lleva o no lleva lentes puestos.

## Tratamiento de los datos
1.Se cargan las imagenes con una escala de colores gris, puesto que así necesitamos un poco menos de maquina para el procesamiento de los datos, las imagenes inicialmente quedan de la siguiente manera:

![_config.yml]({{ site.baseurl }}/images/primer_img.png)

2.Luego las imagenes se redimensionan para que queden todas con la misma dimension de pixeles, en este caso usaremos 150px puesto que con esta dimension no perdemos la calidad de las imagenes:

![_config.yml]({{ site.baseurl }}/images/segunda_img.png)

3.Una vez se tienen las imagenes procesadas con la escala de grises y con el tamaño de 150px por 150px, los imagenes se veran de la siguiente manera:

- Para alguien con lentes:

![_config.yml]({{ site.baseurl }}/images/tercer_img.png)

Computacionalmente lo datos de la imagen anterior se veran como sigue, recordando que es una composicion de pixeles que van de 0 a 255:

![_config.yml]({{ site.baseurl }}/images/cuarta_img.png)


- Para alguien sin lentes:

![_config.yml]({{ site.baseurl }}/images/5_img.png)


Y computacionalmente:

![_config.yml]({{ site.baseurl }}/images/6_img.png)

4.Como los datos estan organizados por categoria, lo que se hace ahora es que queden de forma aleatoria y así el modelo no aprendera que la mitad de los datos son de personas llevando lentes y la otra mitad no lleva lentes.

![_config.yml]({{ site.baseurl }}/images/7_img.png)

5.Para terminar lo que hacemos es que normalizamos todos los datos excepto la variable de respuesta que ya la tenemos unicamente como 0 y 1.

![_config.yml]({{ site.baseurl }}/images/8_img.png)

![_config.yml]({{ site.baseurl }}/images/9_img.png)


## Modelos sin datos aumentados

Inicialmente se proponen tres modelos y como es un problema de clasificacion de imagenes el mejor metodo a usar son las redes neuronales convolucionales. Para iniciar haremos tres modelos sin datos aumentados de los cuales 1 es un modelo denso y los otros dos son modelos convolucionales:

### Modelo denso:
Este modelo tiene una capa de entrada que recibe los 22.500 pixeles, luego tiene dos capas densas con 200 neuronas cada una y finalmente la capa de salida, esta ultima capa debido al problema donde el resultado es si la personas lleva o no lleva lentes puestos tendra unicamente una neurona de salida y usaremos la funcion sigmoid.

![_config.yml]({{ site.baseurl }}/images/10_img.png)


### Modelo convolucional:
Este modelo tiene tres pares de capas convolucionales los cuales pasaran por 32, 64 y 128 filtros, luego tendra una capa densa con 150 neuronas y finalmente la capa de salida que cumple con las mismas condiciones que para el modelo denso.

![_config.yml]({{ site.baseurl }}/images/11_img.png)


### Modelo convolucional 2:
Este modelo tiene tres pares de capas convolucionales los cuales pasaran por 32, 64 y 128 filtros, luego tendra un dropout cuya función es la de regularizar para reducir el sobreajuste de la red neuronal, continua con una capa densa con 150 neuronas y finalmente la capa de salida que cumple con las mismas condiciones que para los modelos anteriores.

![_config.yml]({{ site.baseurl }}/images/12_img.png)


### Grafico de precisión y perdida:
