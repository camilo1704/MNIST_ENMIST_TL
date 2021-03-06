# MNIST_ENMIST_TL

Transfer Learning **MNIST** with **EMNIST** features

Se entreno una red neuronal convolucional con la arquitectura mostrada [CNN](model.png) con la base de datos de EMNIST, se transfirieron posteriormente las características aprendidas de las capas convolucionales para posteriormente reentrenar las últimas capas (full conected layers) con la base de datos de [MNIST](http://yann.lecun.com/exdb/mnist/).<br />

<p align="center"> 
<img height=400 src="https://github.com/camilo1704/MNIST_EMNIST_TL/blob/master/model.png" />
</p>

I used Keras with tensorflow as backend, the EMNIST dataset is a .mat file downloaded from the [official repository of NIST]( https://www.nist.gov/itl/iad/image-group/emnist-dataset).<br />
Se usó keras con Tensorflow como backend en un ambiente virtual creado con Anaconda para lsa versiones  tensorflow=1.8.0 and keras=2.1.6. (estas versiones arreglan el problema de la compatibilidad de la lista de parámetros de las capas sofmax).<br/> 
Los datos vienen separadados previamente en un archivo .mat [download](https://www.nist.gov/itl/iad/image-group/emnist-dataset), donde el set de entrenamiento tiene la dirección "file['dataset'][0,0][0][0][0][0]", las categorías están en file['dataset'][0,0][0][0][0][1], y el set de testeo está en "file['dataset'][0,0][1][0][0][0]" con las categorías "file['dataset'][0,0][1][0][0][1]".<br />
Las categorías en el archivo son de 1 a 26, y como necesitan empezar por 0 se sustrajo 1 como se observa en el codigo.<br />
<p align="center"> 
<img height=400 src="https://github.com/camilo1704/MNIST_EMNIST_TL/blob/master/MNIST.png" />
  </p>

En la [figura](MNIST.png) se muestran los resultados del entrenamiento de la red con la base de datos de MNIST y EMNIST, tanto del entrenamiento completo de todos los parámetros, como aplicando transferencia de aprendizaje. Para los datos llamados *transfer de conv* se congelaron solo los pesos de las capas convolucionales y para los datos llamados *transfer de conv+densa* se congelaron además los pesos de la anteúltima capa densa. Se observa que para este último caso, la precisión obtenida es mucho menor que para el reentrenamiento de ambas capas densas, por lo que la transferencia es más eficiente si se congelan solo los pesos de las capas convolucionales y se reentrenan las capas de clasificación. Se obseva además que con la transferencia de aprendizaje se obtuvo una precisión similar a la obtenida entrenando por completo la red; incluso para el caso de transferencia de EMNIST a MNIST la precisión obtenida es ligeramente mayor.
