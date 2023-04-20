
Time Disributed -> Softmax, CRF, ...

# Auto regresiva

![[Pasted image 20230419153529.png]]

El embedding puede ser entrenable, o pre entrenados. Según la tarea, decisión o otro. Para cosas especificas (medicina por ejemplo, BioBert), preferimos embedding entrenados con corpus específicos. 
En corpus masivos (Wikipedia por ejemplo), conviene que sean entrenables.

dado el carácter \<s\>, que es de inicio, y nos predice la primera palabra (the en el ejemplo). Luego esta se toma como input para predecir la siguiente y así...

En el entrenamiento, tomamos la palabra correcta y no la predicha.

La tarea es **predecir la siguiente palabra**.

# Condicional

![[Pasted image 20230419155006.png]]

la recurrencia se puede reemplazar por transformer
El simbolo en la posicion $j+1$, no solo depende del símbolo $j$, si no que se le agrega un vector de contexto. Que viene de otra red. 

Ese vector de contexto puede ser por ejemplo un tema, idioma. Condicionar con un *prompt*.
Se usa tanto en el entrenamiento y al momento de predecir.

## Encoder - Decoder

Encoder: Genera el vector de contexto
Decoder: Hace la generación auto regresiva

Durante el entrenamiento:
![[Pasted image 20230419155630.png]]

Durante predicción:
Se usa el encoder con el contexto, y luego el decoder con el símbolo de inicio \<s\>

![[Pasted image 20230419160014.png]]

Para traducción:

Es necesario tener corpus paralelo:

Sentencia en idioma de origen y destino.
traduccion

En esta tarea, se deja el texto lo mas natural posible, para que el output sea natural.
