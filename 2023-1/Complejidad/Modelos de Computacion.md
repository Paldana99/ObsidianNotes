$\sum' = \{0, 1\} \quad \text{alfabeto finito.}$
$\sum^{\star} = \text{conjunto de todas las palabras (strings) sobre} \sum'$

$\sum^\star$ siempre contiene a la palabra vacía $\epsilon$

Si $\sum = \{0, 1\} \implies \sum^{\star}= \{\epsilon , 0, 1, 01, 10, 00, 11, \dots\}$ 

> [!note]
> Todas las palabras en $\sum^{\star}$ son finitas

# Lenguaje

$$
\mathcal{L} \subseteq \sum^\star
$$
Cuantos lenguajes existen ?
$$
2^{\mid \sum^{\star\mid}} = 2^{\mid \mathcal{N}\mid} = \mid \mathcal{R}\mid \implies \text{no enumerables}
$$

## Expresiones regulares sobre $\sum$

$$
r, r' = \emptyset \mid \epsilon \mid 0 \mid 1 \mid r \cup r' \mid r \cdot r' 
$$

Cada exp. regular $r$ define un lenguaje $L(r) \subseteq \sum^\star$ 
Se def inductivamente como sigue:
1. $\mathcal{L(\emptyset) = \emptyset}$
2. $\mathcal{L} (\epsilon) = \{\epsilon\}$
3. $\mathcal{L} (0) = \{ 0 \}$
4. $\mathcal{L} (1) = \{ 1 \}$
5. $\mathcal{L} (r \cup r') = \mathcal{L}(r)\cup \mathcal{L}(r')$
6. $\mathcal{L}(r \cdot r') = \{ \bar{u} \bar{v} \mid \bar{u} \in \mathcal{L}(r), \bar{v} \in \mathcal{L}(r') \}$
7. $\mathcal{L}(r^{\star)}= \{ \epsilon \} \cup \bigcup_{i>0}\mathcal{L}(r\cdot r \cdot \dots)_{\text{i veces}} = \{ \epsilon \} \cup \{ \bar{u}_{1}\bar{u}_{2}\bar{u}_{3}\dots \bar{u}_{n}\mid \bar{u}_{1},\bar{u}_{2},\dots \bar{u}_{n}\in\mathcal{L}(r)\}$

| Exp. regular | Leng. regular |
|:------------ | ------------- |
| $\emptyset$  |     $\emptyset$          |
| $\epsilon$   |        $\{ \epsilon \}$       |
|     0         |          $\{ 0 \}$     |
|      1        |              $\{ 1 \}$ |
|       $r \cdot r'$       |            $\{ \bar{u}\bar{v} \mid \bar{u} \in \mathcal{L}(r), \bar{v} \in \mathcal{ L}(r') \}$   |
|        $r \cup r'$      |    $\mathcal{L}(r)\cup \mathcal{L}(r')$           |
|  $r^\star$            | $\{ \epsilon \}\cup \{ \bar{u}_{1}\bar{u}_{2}\dots \bar{u}_{n}\mid \bar{u}_{1},\bar{u}_{2},\dots \bar{u}_{n} \in \mathcal{L}(r)\}$              |

Existen lenguajes no regulares?

$$
\mathcal{L} \subseteq \{ 0, 1 \}^{\star} \quad\text{tq} \quad \mathcal{L} \neq \mathcal{L}(r) \forall \text{toda expr r}
$$

## Automatas

$$
\mathcal{A} = \{ \mathcal{Q}, q_{0}, \mathcal{F}, \delta \}
$$

- $\mathcal{Q}$ conjunto finito de estados
- $q_{0} \in \mathcal{Q}$ estado inicial
- $\mathcal{F} \subseteq \mathcal{Q}$ estados finales
- $\delta : \mathcal{Q} \times \{ 0, 1 \} \to \mathcal{Q}$ es un **funcion parcial** de transicion

El automata recibe una palabra $\bar{w}$ 
Luego realiza la ejecucion de $\mathcal{Q}$ en $\bar{w}$
$\mathcal{Q}$ **acepta** $\bar{w}$, si el estado alcanzado en ultima pos. esta en $\mathcal{F}$.

> [!important]
> El lenguaje def por $\mathcal{A}:$
> 	$\mathcal{L}(\mathcal{A}) = \{ \bar{w} \mid \bar{w} \quad \text{es aceptado por} \mathcal{A}\}$

Ejemplo:

![[Modelos de Computacion 2023-03-19 21.16.02.excalidraw]]

$$\mathcal{L}(\mathcal{A}) = \{ 0^{i}\mid \text{i impar} \} = 0(00)^\star$$

### Automata no determinista

$$
\mathcal{A} = \{ \mathcal{Q}, q_{0}, \mathcal{F}, \delta \}
$$

$\delta$ es una relacion: $\delta\subseteq \left( Q \times \sum \times Q \right)$

> [!abstract] Teorema
> Para todo automata no determinista $\mathcal{A}$, existe un automata determinista $\mathcal{B}$ tal que:
> $\mathcal{L}(\mathcal{A}) = \mathcal{L}(\mathcal{B})$
> $\mathcal{B} = (2^{\mathcal{Q}}, \{ q_{0} \}, \mathcal{F}', \delta')$
> $\mathcal{F}'=\{ A \subseteq Q \mid A \cap F \neq \emptyset \}$

> [!abstract] Teorema
> Para todo expr. regular $r$ existe automata $\mathcal{A}_{r}$ tq:
> $\mathcal{L}(r) = \mathcal{L}(\mathcal{A}_{r})$

> [!abstract] Teorema
> Para todo automata $\mathcal{A}$ existe expr. regular $r$ tq:
> $\mathcal{L}(\mathcal{A}) = \mathcal{L}(r)$

> [!info] Corolario
> Leng. regulares = Leng aceptados automatas


Sea $\mathcal{L} \subseteq \{ 0, 1 \}^{\star}$ un lenguaje
Defina $\bar{u} \equiv_{L} \bar{v} <=> \forall \bar{w}:\bar{u}\bar{w} \in \mathcal{L} <=> \bar{v}\bar{w} \in \mathcal{L}$

> [!abstract] Teorema (Mythill - Nerode)
> Sea $\mathcal{L} \subseteq \sum^\star$ TFAE:
> 1. $\mathcal{L}$ es regular
> 2. $\equiv_{L}$ tiene un numero finito de clases de equivalencia





