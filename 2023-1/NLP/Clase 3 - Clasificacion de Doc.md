
## BOW

Una palabra por entrada , para el vector de caract.
Como output $y : \text{Topico}$ por ejemplo.

![[Pasted image 20230315153212.png]]
$d \to \text{Bow} \to \vec{d}$
$W_{i,j} = T_{f}$

Existe igual:
- Multiclase : $\mid y\mid > 2$
- Multilabel : $\mid y_{j} > 1$

Para problemas de detección por ejemplo *hate speech* puede ser un problema de clasificación binaria. 
![[Pasted image 20230315153804.png]]
$max \quad f_{l,j}$ es la frecuencia máxima del termino mas frecuente.
La corrección del $T_{f}$ permite evitar el problema de Zipf, para que las palabras muy frecuentes pesen menos.

### Naive Bayes
![[Pasted image 20230315154532.png]]

Se considera que los documentos son independientes entre si (por esto es naive), pero existe una dependencia la relación entre el documento y su clase. 

Por detrás hay un proceso generativo, que es capaz de generar datos. 

```
for Instance i in {1, 2, ..., N} do:
	Draw the label y_i ~ Categorical(u);
	Draw the word counts x_i | y_i ~ Multinomial(phi(y_i))
```

u  y phi son parametros del modelo, que si los obtenemos entonces podemos generar texto.

![[Pasted image 20230315155237.png]]

por simplicidad $x_{j}=f_{j}$

Se asume una independencia entre los términos del documento. 
El $B(x)$ permite hacer que quede una funcion probabilistica.

## LIME

Busca ver que tan importante es una palabra para un documento. Causando errores al eliminar una palabra, y dándole un peso.