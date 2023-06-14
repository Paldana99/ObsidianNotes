
Un grupo de un par $(G, *)$, donde $G$ es un conjunto y $*:G \times G \to G$ es una operación que satisface:

- **Neutro**: Existe $e \in G$ tal que para todo $a \in G$
$$
e * a = a*e=a
$$
- **Inversos**: Para todo $a \in G$ existe $a^{-1}\in G$ tal que $$
a * a^{-1} = a^{-1}*a=e
$$
- **Asociatividad**: Para todos $a,b,c \in G$ se tiene 
$$
(a *b)*c = a*(b*c)
$$
## Ejemplos

$$(Z, +)$$
Neutro: 0
Inverso: Dado $a \in Z$, $-a \in Z$
Asociatividad: Si

$$(Q-\{ 0 \}, \cdot)$$
Neutro: 1
Inverso: Dado $q \in Q$, $\frac{1}{q} \in Z$
Asociatividad: Si

$$
(Z_{n}, + \mod n)
$$
Es el grupo aditivo de los enteros en modulo $n$.

$$
Z_{n}^{*}
$$
Grupo multiplicativo de los enteros modulo $n$

> [!note] GCD y grupo
> Notar que este grupo se define como:
> $Z^*_{N}=\{ a \in \{ 1, \dots, N-1 \}| GCD(a, N)=1 \}$
> Dado que $GCD(a,N)=1$ indica que es invertible.


## $Z_{n}^{*}$ y sus subgrupos

Un subgrupo de $(G, *)$ es un conjunto $H \subseteq G$ tal que $(H, *)$ tambien es un grupo.

### Ejemplo: Subgrupos de $Z_{10}^{*}=(\{ 1,3,7,9 \}, \cdot \mod 10)$
$$
\begin{align}
(\{ 1 \}, \cdot \mod 10 ) \\
(\{ 1,3,7,9 \}, \cdot \mod 10 ) \\
(\{ 1,9 \}, \cdot \mod 10 )
\end{align}
$$
Cantidad de elementos en $G=$ orden del grupo

$Z^*_{11}$ Grupo orden 10, subgrupo orden 1, 2, 5, 10
$Z^*_{7}$ Grupo orden 6, subgrupo orden 1, 2, 3, 6
$Z^*_{5}$ Grupo orden 4, subgrupo orden 1, 2, 4
$Z^*_{17}$ Grupo orden 16, subgrupo orden 1, 2, 4, 8 y 16

Sea $G$ un grupo y $H$ un subgrupo de $G$
Dado $g_{0} \in G - H$

Cuantos elementos tiene $g_{0}H=\{ g_{0}*h|h \in H \}$? A lo mas tiene $|H|$ elementos distintos
Si $g_{0}*h_{1} = g_{0}*h_{2}$ entonces $h_{1}=h_{2}$
Tenemos que $|g_{0}H|=|H|$

## Teorema de Lagrange
Si $G$ es un grupo finito y $H$ es un subgrupo de $G$, entonces $|H|$ divide a $|G|$

## Subgrupos generados

Sea $G$ un grupo y $a \in G$. Usando notacion multiplicativa, definiremos
$$
a^n=a*a*\dots*a\quad\text{ n veces}
$$
Si tomamos la secuencia $\{ 1,a,a^2,a^3,\dots \}$ eventualmente un elemento se tiene que repetir. Sea $a^j=a^{j+k}$ la primera repeticion

Tenemos entonces que $a^j=a^{j}*a^k$ y por lo tanto $a^*$ es el neutro

Implica que $j=0$

Definamos $<a> = \{ a^{j}|0\leq j<k \}$

Es un subgrupo de tamano k, implica que $|<a>| = k$ divide a $|G|$

## Grupos ciclicos

Un grupo $(G, *)$ es ciclico si existe $a \in G$ tal que
$$
<a> = G
$$
![[Pasted image 20230611200934.png]]

Si p es un numero primo, entonces $(Z_{p}^*,\cdot)$ es un grupo ciclico

$(Z_{7}^*,\cdot)$ es ciclico ya que $<5> = \{ 1,2,3,4,5,6 \}$
