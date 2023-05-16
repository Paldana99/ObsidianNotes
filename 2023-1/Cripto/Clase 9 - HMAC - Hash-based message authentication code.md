
Construir un MAC en base a una función de hash $h$.

Que pasa si definimos $Mac_{k}=h(k\mid \mid m)$

La funcion de hash nos devolvera un $M$ que es la llave, mensaje mas el padding necesario.

Ahora podemos crear un mensaje $m' = m\mid\mid P'$ el cual podemos calcular su tag, dado que es el hash de $M$ con $P'$.

![[Pasted image 20230425105032.png]]

y si hacemos $Mac_{k}(m) = h(m\mid\mid k)$, no se puede realizar *lenght extension attacks*, ya que el padding queda entre el mensaje y la llave.

Pero puede traer problema si se encuentran colisiones en la función de hash.

Si se encuentra colisión para $m \mid \mid P$ y $m' \mid \mid P'$ tal que son del mismo largo, entonces al agregar el $k$ queda en el mismo tag.

## Solución

$$
Mac_{k}(m)=h(k_{1}\mid\mid h(k_{2}\mid\mid m))
$$
Donde $k_{1}$ y $k_{2}$ ocupan exactamente un bloque, distintas y se derivan de forma determinista a partir de k y no se pueden obtener sin k

Se define de la siguiente forma:

$$
k' = \begin{cases}
h(k) & k\text{ usa mas de un bloque} \\
k & e.o.c
\end{cases}
$$
$$
k_{1}=k'\oplus 36 \dots 36 \quad k_{2} =k' \oplus 5c \dots 5c
$$
$$
5c = 01011100 \quad 36 = 00110110
$$

$$
HMac_{k}(m)=h(k_{2}\mid\mid h(k_{1}\mid\mid m))
$$
![[Pasted image 20230425110538.png]]

