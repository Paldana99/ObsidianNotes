Desde ahora suponemos que $n$ es un numero **impar**
$$
W_{n} = \{ a \in \{ 1,\dots,n-1 \}\mid a^{n-1}\equiv 1 \mod n \}
$$
El teorema de fermat nos dice que si $p$ es primo entonces:
$$
\mid W_{p} \mid = p-1
$$
## Caso que n es compuesto
Si $n$ es un numero compuesto, entonces (no es cierto para todos)
$$
\mid W_{n}\mid\leq \frac{n-1}{2}
$$

## Test de primalidad v.1

Dados $n$ y $k$:
1. Elija $a_{1},\dots,a_{k}$ en $\{ 1, \dots, n-1 \}$ con distribución uniforme y de manera independiente
2. Calcule $b_{i} = a_{i}^{n-1} \mod n$ para cada $i \in \{ 1, \dots, k \}$
3. Si $b_{i} \neq 1$ para algun $i \in \{ 1, \dots, k \}$ entonces return **false**, caso contrarion return **true**.

### Pero...

Existe cantidad infinita de números compuestos $n$ tales que:
$$
\mid W_{n}\mid> \frac{n-1}{2}
$$
## Nocion de testigo

Consideramos testigos de la forma:
$$
a^{\frac{n-1}{2}} \mod n
$$
Estos están bien definidos dado que $n$ es impar

Si $p$ es un numero primo impar, y $a \in \{  1 , \dots p-1 \}$ entonces
$$
\begin{align}
a^{\frac{p-1}{2}} &\equiv 1 &\mod p & \quad \text{o} \\
a^{\frac{p-1}{2}}&\equiv -1 &\mod p 
\end{align}
$$
Sea:
$$
\begin{align}
W^{+}_{n} &= \{  a \in \{ 1, \dots, n-1 \} \mid a^{\frac{n-1}{2}}\equiv 1 \mod n \} \\
W^{-}_{n} &= \{  a \in \{ 1, \dots, n-1 \} \mid a^{\frac{n-1}{2}}\equiv -1 \mod n \} 
\end{align}
$$
### Teorema

Si $p$ es un numero primo impar, entonces
$$
\mid W^{+}_{p} \mid = \mid W^{-}_{p} \mid  = \frac{p-1}{ 2}
$$
### Teorema
Si $p$ es un numero primo y $r(x)$ es un polinomio de grado $k$, entonces $r(x)$ tiene a lo mas $k$ raíces en modulo $p$
