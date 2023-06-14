**One-way function**: operaciones que son difíciles para volver atrás, por ejemplo multiplicar dos números primos, $x^{e} \mod N$

Para ciertos grupos, en particular subgrupos de $Z_{p}^*$, creemos que es difícil calcular el logaritmo discreto.

Dado $g \in G$ y el valor $y=g^x$, si $\mid<g>\mid$ es grande, es difícil calcular $x$

Siendo $g \in G$ un elemento que genera un subgrupo grande, la función $f(x)=g^x$ es una *one-way function*

Queremos usar elementos de orden primo en $Z_{p}^*$, ya que el orden puede ser una descomposicion del orden, pero al ser primo solo puede ser 1, o el numero mismo.

## Diffie-Hellman (y Merkle)
Protocolo para intercambiar una llave secreta (simetrica) en un canal inseguro

![[Pasted image 20230611201607.png]]

La llave compartida es $S = g^{x \cdot y}$

## El Gamal

Se basa en usar Diffie-Hellman, donde quien envía el mensaje genera una llave efímera

Se acuerda un grupo $<g>$ de orden $q$
Alice genera $x \in \{ 1, \dots, q \}$ esa es su llave secreta.
Alice publica $g^x$ que sera su llave publica

Bob genera $y \in \{ 1, \dots, q \}$ (llave efimera)
Le envia a Alice el par $(m * g^{xy}, g^y)$


Alice para recuperar $m$ debe buscar el inverso de $g^{xy}$

$$
g^{xy}*g^{y(q-x)} = g^{xy+yq-xy}=g^{yq}
$$
Como $yq$ es multiplo del orden del grupo, $g^{yq}=e$. 
$g^{y(q-x)}$ es el inverso de $g^{xy}$
