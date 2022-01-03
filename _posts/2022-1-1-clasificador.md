---
layout: post
title: Clasificador
published: true
---
## Introducción
Este es un trabajo para el curso de aprendizaje estadistico de la universidad Nacional de Colombia sede Medellín, cuyo objetivo es solucionar el problema de clasificar imágenes utilizando técnicas de aprendizaje estadístico. En el campo de clasificación de imagenes muchas veces es necesario identificar si la persona lleva apuestos lentes o si no los lleva, las aplicaciones que tiene lograr un modelo de estos son inmensas tales como: mecanismos de autenticación en servicios de pagos online, procesos de inicio de sesión, validacion de metodos de pago, entre muchas otras.

## Dataset
Para el modelo los datos fueron basados en https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images, que a su vez estan basados en https://www.kaggle.com/jeffheaton/glasses-or-no-glasses. Inicialmente los datos ya estaban organizados y separados por el tipo de imagen, que era si la persona lleva o no lleva lentes puestos.

## Tratamiento de los datos
Se cargan las imagenes con una escala de colores gris, puesto que así necesitamos un poco menos de maquina para el procesamiento de los datos, las imagenes inicialmente quedan de la siguiente manera:

![_config.yml]({{ site.baseurl }}/images/primer_img.png)


Luego las imagenes se redimensionan para que queden todas con la misma dimension de pixeles, en este caso usaremos 150px puesto que con esta dimension no perdemos la calidad de las imagenes:

![_config.yml]({{ site.baseurl }}/images/segunda_img.png)

Una vez se tienen las imagenes procesadas con la escala de grises y con el tamaño de 150px por 150px, los imagenes se veran de la siguiente manera:

- Para alguien con lentes:

![_config.yml]({{ site.baseurl }}/images/tercer_img.png)

Computacionalmente lo datos de la imagen anterior se veran como sigue, recordando que es una composicion de pixeles que van de 0 a 255:

![_config.yml]({{ site.baseurl }}/images/cuarta_img.png)


- Para alguien sin lentes:

![_config.yml]({{ site.baseurl }}/images/5_img.png)


Y computacionalmente:

![_config.yml]({{ site.baseurl }}/images/6_img.png)


