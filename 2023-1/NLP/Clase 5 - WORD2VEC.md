## Word2vec

Ahora vectorizamos la palabra y no el documento.

![[Pasted image 20230322153625.png]]

El one-hot vector permite hacer un lookup en la matriz de entrada. 
En la salida tenemos palabras, que permite relacionar la palabra de entrada con la de salidas.

### Skip-grams

Se desliza una ventana, la del medio es el input, las otras quedan en la salida. Así se intenta encontrar relaciones semánticas dentro de un texto por proximidad. Skip-grams esta pensado para usarlo en una sentencia, considerando que el punto va a separar ideas, y por lo tanto no tendrían relación.

## Entrenamiento de la red

![[Pasted image 20230322155045.png]]

Negative Sampling:

Muestro palabras que no estan relacionadas, para poder minimizar la relacion entre las dos. Escojo pares no relacionados. Usualmente para cada ventana, escogemos k = 5 palabras negativas.

![[Clase 5 - WORD2VEC 2023-03-22 15.58.28.excalidraw]]

Se puede operar los vectores para ver similitud.

Para ver si uno no hace match con las demas palabras podemos excluir una y ver la que da mayor longitud de la suma de los vectores. Asi sabemos cual esta mas alejada de las demas. 