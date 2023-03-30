# Co-occurence matrices

Dados una imagen $I$, definimos la matrix $P_{10}$:

![[Pasted image 20230330114656.png]]
La matriz cuenta cuantas veces co occurre los pares de pixeles. Se normaliza por el total de pares de pixeles que pueden existir.

![[Pasted image 20230330114939.png]]

Hay dos pares de pixeles, (0, 0) es la ventana 10. 

Podemos analizar la matriz:

## Contraste:

![[Pasted image 20230330120157.png]]

Dice si en la direccion escogida, hay cambios bruscos. Impide que los numeros de la diagonal sea representativos.

Existen 14 otros... ver ppt


Se utiliza un $d$ pixeles y se extrae la matriz en 4 direcciones:
- -dd
- d0
- dd
- 0d
Y luego se suelen promediar las 4