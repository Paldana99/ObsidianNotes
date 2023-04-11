Función de un espacio de mensajes a un espacio de mensajes de largo fijo :
$$
h : \mathcal{M} \to \mathcal{H}
$$
$\mathcal{M}$ es el espacio de mensajes y $\mathcal{H}$ es el espacio de posibles valores de la funcion de hash
- Por ejemplo, $\mathcal{M} = \{ 0 , 1 \}^\star$ y $\mathcal{H} = \{ 0 ,1 \}^{128}$
- Decimos que h(m) es el hash de un mensaje m

### Una propiedad basica de las funciones de hash

Debe existir un algoritmo eficiente que, dado $m \in\mathcal{M}$, calcula h(m)

No debe existir un algoritmo eficiente que, dado $x \in \mathcal{H}$ encuentre $m \in \mathcal{M}$ tal que h(m) = x

Esta propiedad se denota como **ser resistente a preimagen**.

### Segunda propiedad fundamental de las funciones de hash

No debe existir un algoritmo eficiente que pueda encontrar $m_{1}, m_{2} \in \mathcal{M}$ tales que $m_{1} \neq m_{2}$ y $h(m_{1}) = h(m_{2})$

Esta propiedad se denota como **ser resistente a colisiones**

## Aplicaciones de las funciones de hash

Las funciones de hash (criptograficas) tienen muchas aplicaciones practicas, y nos van a acompañar durante todo el curso

Ejemplos:

- Integridad de un documento
![[Pasted image 20230329214513.png]]

- Lanzar una moneda por telefono
![[Pasted image 20230329214702.png]]

## Definicion formal de funcion de hash

Una función de hash es un par $(Gen, h)$ tal que:
- $Gen$ es un algoritmo aleatorizado de tiempo polinomial. $Gen$ toma como entrada un parámetro de seguridad $1^n$, y genera una llave $s$
- $h$ es algoritmo de tiempo polinomial. $h$ toma como entrada $s$ y un mensaje $m \in \{ 0,1 \}^\star$, y retorna un hash $h^{s}(m)\in \{ 0, 1 \}^{l(n)}$, donde $l$ es un polinomio fijo

Si $m \in \{ 0,1 \}^{l'(n)}$ para un polinomio fijo $l'$ tal que $l'(n) > l(n)$ , entonces $(Gen, h)$ es una funcion de hash de largo fijo

Una función $f : N \to R^{+}_{0}$ es despreciable si:
$$
(\forall \text{polinomio } p: N \to N )(\exists n_{o}\in N)(\forall \geq n_{0})(f(n) < \frac{1}{p(n)})
$$

### Formalizar noción de resistencia a colisiones

Considere una función de hash $(Gen, h)$

Definimos e juego $Hash-Col(n)$:
1. El verificador genera $s = Gen(1^n)$, y se lo entrega al adversario
2. El adversario elige mensajes $m_{1}, m_{2}$ con $m_{1} \neq m_{2}$
3. El adversario gana el juego si $h^{s}(m_{1}) = h^s(m_{2})$, y en caso contrario pierde

Una función de hash $(Gen, h)$ se dice resistente a colisiones si **para todo adversario que funciona como un algoritmo aleatorizado de tiempo polinomial**, existe una función despreciable $f(n)$ tal que:

$$
Pr(\text{Adversario gane Hash-Col(n)})\leq f(n)
$$