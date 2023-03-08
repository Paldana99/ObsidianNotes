
NLP es una área que cruza IA, ML y DL, ademas con computación lingüística.
Con nlp buscamos hacer traducción de maquina, análisis de sentimiento, extracción de información, interacción humano computador.

El enfoque clasico se parece al de DL, solo que se usa volumenes grandes de texto como input.
![[Pasted image 20230308155255.png]]

Hay un proceso de aprendizaje (supervisado o no).

## Leyes del texto

- La mayoría de las palabras se usan muy poco, y una minoría mucho. 
Existe una "ley" constante entre la frequencia de una palabra, y su ranking de la palabra.

### Ley de Zipf:

![[Pasted image 20230308155851.png]]

![[Pasted image 20230308155836.png]]

$\theta \in [ 1.0 , 1.6 ]$

Se encuentran tres categorías de palabras:
- stopwords
- keywords
- outliers
Entre los stopwords y keyword están las palabras interesantes a estudiar ya que nos dan mas información.

![[Pasted image 20230308160304.png]]

### Ley de Heaps

Mide el crecimiento del vocabulario, en proporción con el tamaño del texto (numero de tokens)
![[Pasted image 20230308160507.png]]

Esta ley va depender igualmente del tipo de texto al analizar, con textos mas específicos (científicos por ejemplo) el vocabulario es mas extenso, no pasa en cambio con por ejemplo en redes sociales.
-> Por eso hay tres curvas según el tipo de texto.

Esta ley es útil ya que nos permite predecir de antemano de cuanto vocabulario va a existir en un texto. 

$\beta$ va a indicar un crecimiento sublineal -> es decir que $\beta < 1$ . Normalmente entre: $0.3 <= \beta <= 0.6$ cuanto mas chico, mas básico el tipo de texto.  
k indica la verbosidad del lenguaje

## Procesamiento basico

- Token : String delimitado que aparece en el texto
- Termino: Token con algún significado según el corpus

### **Lematizacion** 
indica reducir formas infleccionales a su raíz, por ejemplo poner todo al infinitivo
	ejemplo: be = {are, is, ...}

De esta forma reducimos a un vocabulario mas compacto.
	Para esto se usa WordNet, que permite una enorme red de palabras, que están organizadas en forma semantica.

![[Pasted image 20230308161624.png]]

- hipernimo: synset cuyo significado es mas general
- hiponimo: synset mas especifico que el otro
- meronimo: synset relacionados entre ellos, pero uno hace parte del otro