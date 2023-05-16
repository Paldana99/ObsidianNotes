## Recordatorio

### Operación módulo

Dados $a, n \in Z$ , existe un único par de elementos $(q, r) \in Z^2$ tal que:

$$0 <= r < |n|$$
$$a = q * n + r$$
	Decimos entonces que $a \mod n = r$    y que  $a \equiv r \mod n$ 

Ademas, $a \equiv b \mod n$ si y solo si $n|(b-a)$
o es equivalente
$$
a \mod n = b \mod n
$$

**Propiedad fundamental:**
Si $a\equiv b \mod n$ y $c \equiv d \mod n$ entonces
$$
(a+c)\equiv (b+d) \mod n
$$
$$
(a \cdot c) \equiv (b \cdot d) \mod n
$$
## Objetivo inicial

Vamos a estudiar algunos algoritmos en teoría de números
- Los cuales son fundamentales para los protocolos criptográficos de la clave pública

## Máximo común divisor

Sean $a,b \in N$ con $a >b$. Para calcular $MCD(a,b)$ utilizamos la siguiente recurrencia:
$$
MCD(a,b) = \begin{cases}
a  & \text{si } b = 0 \\
MCD(b,a\mod b) & \text{si } b> 0
\end{cases}
$$
#### Nota sobre complejidad

En protocolos de criptografia de llave publica podemos usar numeros con 800 digitos. Si $n$ tiene 800 digitos, no vamos a poder ejecutar un algoritmo de tiempo polinomial en $n$
- No podemos realizar $n, n^{2}, n^3$ operaciones, puesto que $n\geq 10^{799}$
Vamos a utilizar algoritmos de tiempo polinomial en el **largo de $n$**
- Vale decir, de tiempo polinomial en el **largo de la entrada**
Esto significa que vamos a utilizar algoritmos de tiempo polinomial en **$log(n)$**

### Algoritmo extendido de Euclides

Dados numeros $a,b \in N$ tales que $a>b$, existen numeros $s,t \in Z$ tales que:
$$
MCD(a,b)= s \cdot a + t \cdot b
$$
Por ejemplo: $MCD(180, 63)= 9$ y $9= (-1)\cdot 180 + 3 \cdot 63$

Dados numeros $a$ y $b$, el algoritmo extendido de Euclides calcula $MCD(a,b)$ y los numeros $s,t$

Defina una secuencia $r_{0}, r_{1}, \dots$ tal que:
$$
\begin{align}
r_{0} =& a&  \\
r_{1} =& b&  \\
r_{i+1} =& r_{i-1} \mod r_{i}& \text{ para } i\geq 1
\end{align}
$$

Si $r_{k} = 0$, entonces $MCD(a,b) = r_{k-1}$ y el algoritmo se puede detener

Ademas, vamos a mantener secuencias de numeros $s_{0},s_{1},\dots$ y $t_{0},t_{1},\dots$ tales que:
$$
r_{i} = s_{i} \cdot a + t_{i} \cdot b
$$
Si $r_{k}=0$, entonces $MCD(a,b)= r_{k-1}=s_{k-1} \cdot a + t_{k-1} \cdot b$ y el algortimo retorna $MCD(a,b), s_{k-1}, t_{k-1}$

Tenemos que:
$$
\begin{align}
r_{0} = & 1 \cdot a + 0 \cdot b \\
r_{1} = & 0 \cdot a + 1 \cdot b  \\
r_{i+1} = & \left( s_{i-1} - \lfloor \frac{r_{i-1}}{r_{i}} \rfloor \cdot s_{i} \right)\cdot a + \left( t_{i-1} - \lfloor \frac{r_{i-1}}{r_{i}} \rfloor \cdot t_{i} \right)\cdot b
\end{align}
$$
### Inverso Modular

$b$ es inverso de $a$ en modulo $n$ si:
$$
a \cdot b \equiv 1 \mod n
$$
Por ejemplo, 4 es inverso de 2 en modulo 7:
$$
2 \cdot 4 \equiv 1 \mod 7
$$

> [!note] Teorema
> Un numero $a$ es invertible en modulo $n$ si y solo si $MCD(a,n)=1$

- Vale decir, si $a$ y $n$ son primos relativos

#### Algoritmo

Dado numero $a$ y $n$:
1. Verifique se $MCD(a,n)=1$
2. Si el paso 1 se cumple, use el algoritmo extendido de Euclides para construir $s,t \in Z$: $1 = MCD(a,n)=s \cdot a + t \cdot n$
3. Retorne $s$
