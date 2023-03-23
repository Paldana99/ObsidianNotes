
Cifrado (simétrico) -> nos referimos antes de los 70'

![[Pasted image 20230309104914.png]]

## Cifrado del César

Se hace un shift de n letras:
	n = 3: A -> X ; B -> X
	HOLA MUNDO -> EMIX JRKAM

La llave podría ser el shift. Hay muy pocas posibilidades -> 27 diferentes existentes.

Para mejorarlo, podemos hacer permutación de las letras. aumentamos el espacio de llaves a $27!$ 

Aun así es malo, ya que podemos encontrar mediante distribución de letras ver cuales son según esto. La letra E en ingles aparece el 13%. 

> [!important]
> Un espacio de llaves grandes es necesario, no suficiente

## ONE-TIME PAD (OTP)

### Operación módulo

Dados $a, n \in Z$ , existe un único par de elementos $(q, r) \in Z^2$ tal que:

$$0 <= r < |n|$$
$$a = q * n + r$$
	Decimos entonces que $a \mod n = r$    y que  $a \equiv r \mod n$ 

Esperamos que:
```python
n * (a / n) + a % n = a
```

Donde / es la división entera.

### OTP

se parte enumerando las letras:
![[Pasted image 20230309111453.png]]

Para enviar un mensaje de largo $l$ -> necesitamos una llave de largo $l$
Se aplica la suma según la coordenada de cada letra en nuestro alfabeto y luego se aplica el modulo del largo de nuestro alfabeto. 
Puesto que usamos la definición del modulo positiva, tendremos un valor entre $[0, 27]$.
![[Pasted image 20230309111513.png]]
Para decriptar:
Mismo proceso, pero aplicando la resta.
![[Pasted image 20230309111934.png]]

Definimos como el mensaje : $a$ y el mensaje traducido en numeros como: $\bar a$ 
Asi podemos ver que: 
$$\bar{\bar a} = a$$
Con esto definimos:
$$Enc_k(m)=(m+k) \mod 27$$
$$Dec_k(c)=(c-k) \mod 27$$
$$Dec_k(Enc_k(m))=((m+k) \mod 27 - k) \mod 27 = (m + k - k) \mod 27 = m \mod 27 = m$$

> [!important] Revisar
> Dado que: $(m + k) \mod 27 = m + k$ ya que un numero es siempre congruente consigo mismo.

> [!info] Aritmetica modular
> Division:
> $$a \mid b \leftrightarrow \exists q \in \mathcal{Z} \quad a \cdot q = b  $$
> Congruencia:
> $$a \equiv b \mod m \leftrightarrow  m \mid (a-b)$$
> Proposicion:
> $$\forall m > 0 \text{ si } a\equiv b \mod m \quad \land c \equiv d \mod m$$
> $$
\begin{align}
a + c  & \equiv  &  (b + d )\mod m \\
a \cdot c  & \equiv & b \cdot d \mod m
\end{align}$$


### Esquema criptográfico



**K, M, C**

K -> espacio de llaves
M -> mensajes
C -> textos cifrados

Un esquema es un triple ($Gen, Enc, Dec$)

**$Gen$** es una distribución de probabilidades sobre $K$.

![[Pasted image 20230314103259.png]]



$Enc = {Enc_k | k \in K}$ es una familia de algoritmo para decriptar para cada $k \in K$, se tiene que $Dec_k: C -> M$

Esperamos que para un esquema cript. se cumpla:

$$\forall k \in K \forall m \in M: Dec_k(Enc_k(m)) = m$$
> [!info] Formalizar
> Es importante para la cripto moderna, la formalizacion de los conceptos para las demostracions. Importante valor


**En este caso diremos que el esquema es perfectamente correcto.**

#### Perfect Secrecy

Cuando el atacante ve un mensaje cifrado, no gana ninguna información. 

![[Pasted image 20230314104626.png]]


La idea es que la probabilidad de la llave, es casi que haberla elegido al azar. 

![[Pasted image 20230314110151.png]]

Si el atacante tiene información previa, es decir puede conocer


$$\sum_{k \in K: Enc(m_{0}=c_{o})}Gen(k)$$

![[Pasted image 20230320225140.png]]


> [!abstract] Teorema
> Sean $\mathcal{M},\mathcal{K},\mathcal{C}$ espacios de mensajes, llaves y textos cifrados, respectivamente
> Si $\mid \mathcal{K}\mid < \mid \mathcal{M}\mid$, entonces no existe un esquema (Gen, Enc, Dec) que sea perfectamente secreto.


