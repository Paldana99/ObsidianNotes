
# POS tagging

Etiquetar cada termino de acuerdo a la funcion que este cumple en el texto.

Util para tareas de deteccion de estilo, parsing, deteccion de colocaciones.
Tarea importante en NLP.

![[Pasted image 20230405153710.png]]

Se puede usar `NLTK` o `SPICY`

O usar `HMM` Hidden Markov Model (modelo clasico)

Buscamos la probabilidad de una palabra, dado una cadena de tags.
$$
P(t | x_{1}, x_{2}, \dots, x_{t+1}) = P(t | x_{t+1})
$$

![[Pasted image 20230405154504.png]]

Hoy dia se utilizan redes neuronales 
