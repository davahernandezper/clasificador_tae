---
layout: post
title: Clasificador
published: true
---
## Introducción
Este es un trabajo para el curso de aprendizaje estadistico de la universidad Nacional de Colombia sede Medellín, cuyo objetivo es solucionar el problema de clasificar imágenes utilizando técnicas de aprendizaje estadístico. En el campo de clasificación de imagenes muchas veces es necesario identificar si la persona lleva apuestos lentes o si no los lleva, las aplicaciones que tiene lograr un modelo de estos son inmensas tales como: mecanismos de autenticación en servicios de pagos online, procesos de inicio de sesión, validacion de metodos de pago, entre muchas otras.

## Dataset
Para el modelo los datos fueron basados en https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images, que a su vez estan basado en https://www.kaggle.com/jeffheaton/glasses-or-no-glasses. Inicialmente los datos ya estaban organizados y separados por el tipo de imagen, que era si la persona lleva o no lleva lentes puestos.

## Tratamiento de los datos
1. Se cargan las imagenes con una escala de colores gris, puesto que así necesitamos un poco menos de maquina para el procesamiento de los datos, las imagenes inicialmente quedan de la siguiente manera:

![_config.yml]({{ site.baseurl }}/images/primer_img.png)

2. Luego las imagenes se redimensionan para que queden todas con la misma dimension de pixeles, en este caso usaremos 150px puesto que con esta dimension no perdemos la calidad de las imagenes:

![_config.yml]({{ site.baseurl }}/images/segunda_img.png)


