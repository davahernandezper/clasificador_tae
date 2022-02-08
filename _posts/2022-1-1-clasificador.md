---
layout: post
title: Clasificador
published: true
---
## Introducción
Este es un trabajo para el curso de aprendizaje estadístico de la universidad Nacional de Colombia sede Medellín, cuyo objetivo es solucionar el problema de clasificar imágenes utilizando técnicas de aprendizaje estadístico. En el campo de clasificación de imágenes muchas veces es necesario identificar si la persona lleva puestos lentes o si no los lleva, las aplicaciones de estos modelos son de gran importancia, algunos ejemplos son: mecanismos de autenticación en servicios de pagos online, procesos de inicio de sesión, validación de métodos de pago, entre muchas otras.

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


- La figura 2 muestra cómo se verán los datos para las imágenes de personas sin lentes:

![_config.yml]({{ site.baseurl }}/images/cuarta_img.jpeg)


4.Como los datos están organizados por categoría se mezcla de forma aleatoria para así, evitar introducir al modelo cualquier patrón de comportamiento.
Para terminar, se normalizan todos los datos excepto la variable de respuesta que toma valores únicamente de 0 y 1.

## Modelos
Como es un problema de clasificación de imágenes el mejor método a usar son las redes neuronales convolucionales, pero de igual manera es una buena idea no solo validar con esta técnica. Para el problema se usaron los siguientes modelos:

-Red neural artificial (ANN) - Modelo denso: Se decide usarla debido a que cada una de sus neuronas se considera como una regresión logística con la capacidad de aprender cualquier función no lineal. Una de las desventajas más grandes que se tiene con este método es que puede aumentar el número de parámetros dependiendo del tamaño de la imagen y que puede llegar a perder características espaciales de una imagen (Pai, 2020).


-Red neuronal convolucional (CNN) - Modelo convolucional: Estos modelos se escogen debido a que tienen la capacidad de aprender filtros automáticamente sin la necesidad de tenerlo que especificar o aclarar y en comparación con las ANN, estos modelos capturan las características espaciales de una imagen por lo que es capaz de crear una relación entre los pixeles de una imagen (Pai, 2020).

Una de las desventajas de este modelo es que requiere muchas entradas de datos para lograr una alta precisión (Meel, 2021).


Para evaluar el desempeño de cada uno de los modelos se usarán los gráficos de precisión y perdida, además se evalúa cada modelo con dos técnicas diferentes para el tratamiento de las imágenes:

### Modelos sin datos aumentados
Para modelos sin datos aumentados se quiere decir que el conjunto de imágenes de entrenamiento no tiene ninguna transformación por lo que se verán como:

![_config.yml]({{ site.baseurl }}/images/15_img.png)

#### Modelo denso:
Este modelo tiene una capa de entrada que recibe los 22.500 pixeles, luego tiene dos capas densas con 200 neuronas cada una y finalmente la capa de salida, esta última capa debido al problema donde el resultado es si la personas lleva o no lleva lentes puestos tendrá únicamente una neurona de salida y usaremos la función Sigmoid. Se usa esta función dado que sus valores de respuesta están siempre entre 0 y 1.

#### Modelo convolucional:
Este modelo tiene tres pares de capas convolucionales los cuales pasaran por 32, 64 y 128 filtros, luego tendrá una capa densa con 150 neuronas y finalmente la capa de salida que cumple con las mismas condiciones que para el modelo denso.


#### Gráfico de precisión y perdida:
En la gráfica 1 para el modelo denso y en la gráfica 2 para el modelo convolucional, podemos observar que la precisión para ambos conjuntos es creciente con cada paso de la red. En la gráfica 1 para el modelo denso podemos observar un comportamiento fluctuante tanto en precisión como en perdida, en la precisión luego del paso 70 se alcanza el valor de 1 para el conjunto de entrenamiento lo que podría indicar un sobreajuste.

Para el modelo convolucional en la gráfica 2, se alcanza identificar que la precisión es igual a 1 en muy pocos pasos, lo que podría indicar que la red se está aprendiendo los datos de memoria y que por ello es que necesita menos pasos para su aprendizaje, también, lo podemos confirmar con la perdida dado que para el conjunto de entrenamiento el error tiende a cero a medida que la red da más pasos pero, el error del conjunto de validación empieza a ser creciente luego de los 40 pasos.

![_config.yml]({{ site.baseurl }}/images/grafico_1.jpeg)

![_config.yml]({{ site.baseurl }}/images/grafico_2.jpeg)




### Modelos con datos aumentados

Ahora se proponen los mismos dos modelos, pero esta vez con datos aumentados, esto significa que se les realizaran modificaciones a las imágenes del conjunto de entrenamiento, tales como: rotaciones, inclinaciones, acercamientos, desplazamientos verticales y desplazamientos horizontales. 

las imágenes del conjunto de entrenamiento se ven como sigue:

![_config.yml]({{ site.baseurl }}/images/15_img.png)

y quedaran de la siguiente manera:

![_config.yml]({{ site.baseurl }}/images/16_img.png)


Para estos modelos se usaron las mismas reglas que los anteriores y el único cambio fue que se realizaron las modificaciones ya mencionadas sobre el conjunto de entrenamiento.

En la gráfica 3 se puede observar que el modelo denso no tiene una mejora en la precisión ni en la perdida, ambas muestran una tendencia constante. En la precisión se puede observar una disminución en el desempeño del conjunto de entrenamiento.

El comportamiento deseado se obtiene con el modelo convolucional en la gráfica 4, donde se tiene que la precisión de ambos conjuntos está creciendo a la par y la perdida está tendiendo a cero.


![_config.yml]({{ site.baseurl }}/images/grafico_3.jpeg)


![_config.yml]({{ site.baseurl }}/images/grafico_4.jpeg)




## Resultado conjunto de validación [CMU Face Images Data Set](http://archive.ics.uci.edu/ml/datasets/cmu+face+images)

Teniendo en cuenta los resultados anteriores, se decide evaluar el desempeño de los dos con mejor precisión y menor pérdida, estos son el modelo denso sin datos aumentados y el modelo convolucional con datos aumentados, teniendo en cuenta el conjunto de imágenes compartidas para realizar la evaluación del modelo (siendo este un conjunto de validación aparte del de prueba) 
Los resultados se muestran a continuación: 

- El modelo denso presento una precisión del 37%.
- El modelo convolucional con datos aumentos presenta una precisión del 78%.

De esta manera el modelo seleccionado es el convolucional con datos aumentados pues este presenta un mejor desempeño en el conjunto de validación. De igual manera, en el mundo del reconocimiento facial un 22% puede hacer gran diferencia en procesos de seguridad de la información. La pérdida de precisión puede deberse a que en el conjunto de validación (a diferencia del conjunto de entrenamiento y prueba) las imágenes no deben tener una reducción de dimensiones, sino que más bien deben ser aumentadas. Otra gran diferencia es que el conjunto de validación ya viene en una escala de grises, mientras que el conjunto de entrenamiento debe ser transformado en su escala de colores a gris.



## Bibliografía

-Bueno, J. (2021, enero). data-cleaning-glasses-no-glasses. Kaggle. Recuperado 25 de diciembre de 2021, de [https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images](https://www.kaggle.com/jorgebuenoperez/datacleaningglassesnoglasses?select=Images).

-Heaton, J. (2020, 18 abril). Glasses or No Glasses. Kaggle. Recuperado 25 de diciembre de 2021, de [https://www.kaggle.com/jeffheaton/glasses-or-no-glasses](https://www.kaggle.com/jeffheaton/glasses-or-no-glasses).

-Foro de GitHub. (2016, 3 octubre). flow_from_directory seems to find no images · Issue #3946 · keras-team/keras. GitHub. Recuperado 24 de diciembre de 2021, de [https://github.com/keras-team/keras/issues/3946](https://github.com/keras-team/keras/issues/3946).

-Chaturvedi, S. (2019, 5 junio). Research gate. Research gate. Recuperado 1 de enero de 2022, de [https://www.researchgate.net/post](https://www.researchgate.net/post/When_can_Validation_Accuracy_be_greater_than_Training_Accuracy_for_Deep_Learning_Models)

-Zhang, K. (2020, 26 julio). Redes-Neuronales. GitHub. Recuperado 2 de enero de 2022, de [https://github.com/Codificados/Redes-Neuronales/blob/master/GenerarDatos.py](https://github.com/Codificados/Redes-Neuronales/blob/master/GenerarDatos.py).

-Introduction to deep learning. (s. f.). pythonprogramming.net. Recuperado 2 de enero de 2022, de [https://pythonprogramming.net/introduction-deep-learning-python-tensorflow-keras/](https://pythonprogramming.net/introduction-deep-learning-python-tensorflow-keras/).

-Pai, A. (2020, 17 febrero). ANN vs CNN vs RNN | Types of Neural Networks. Analytics Vidhya. Recuperado 7 de febrero de 2022, de [https://www.analyticsvidhya.com/blog/2020/02/cnn-vs-rnn-vs-mlp-analyzing-3-types-of-neural-networks-in-deep-learning/](https://www.analyticsvidhya.com/blog/2020/02/cnn-vs-rnn-vs-mlp-analyzing-3-types-of-neural-networks-in-deep-learning/).

-Meel, V. (2021, 1 febrero). ANN and CNN: Analyzing Differences and Similarities. Viso.Ai. Recuperado 7 de febrero de 2022, de [https://viso.ai/deep-learning/ann-and-cnn-analyzing-differences-and-similarities/](https://viso.ai/deep-learning/ann-and-cnn-analyzing-differences-and-similarities/).
