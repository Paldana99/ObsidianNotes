
Analizar la opinión de un texto (Opinion Mining). Puede dar como resultado:
- Positivo
- Negativo
- Neutro en ciertos casos


Dos approachs posibles:
- Machine Learning -> Supervisado o No supervisado
- Lexicon-Based -> Conozco una lista de palabras que tienen una carga positiva/negativa

![[Pasted image 20230316153624.png]]

La ironía es complicada ya que juega con vocabulario positivo, pero por contexto se entiende como algo negativo. Hay que hilar mas fino.

## Sentiment analysis

Se utilizan tres parámetros:
- valence (the pleasantness of a stimulus)
- arousal (the intensity of emotion provoked by a stimulus)
- dominance (the degree of control exerted by a stimulus) Palabras que hacen que ejerca una reaccion

Mediante esto se crea un léxico : **Affective Norms for English Words (ANEW)**

![[Pasted image 20230316154353.png]]

Se toman palabras del corpus y se revisa si existe en el lexicon. Se recuperan los puntos, y promedian. Luego con un árbol de decisión, se decide si el corpus es neutro, negativo, positivo.

Limitaciones:
Si hay palabras que no están en el léxico, entonces no lo toma en cuenta. E igual no toma en contexto las palabras. 
