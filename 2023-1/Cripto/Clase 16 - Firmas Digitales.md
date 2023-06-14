![[Pasted image 20230614164548.png]]

- A firma un mensaje $m$
- $\sigma(S_{A}, m)$ utiliza la clave secrete de A para generar una firma $f$ de $m$, de manera tal que solo $A$ puede firmar
- $T(P_{A},m,f)$ verifica si $f$ es una firma valida del mensaje $m$ por el usuario $A$
- $T(P_{A}, m, f)$ utiliza la clave publica de $A$, de manera que cualquiera puede verificar si $f$ es una firma valida.

## Firmas digitales con RSA

Suponga que $P_{A}= (e, N)$ y $S_{A}=(d,N)$ son las claves publica y privada de un usuario $A$

Para cada $m \in \{ 0, \dots, N - 1 \}$, sabemos que
$$
Dec_{S_{A}}(Enc_{P_{A}}(m)) = m
$$
Pero también tenemos que:

$$
\begin{align}
Enc_{P_{A}}(Dec_{_{S_{A}}}(m)) &= (m^{d}\mod N)^{e}\mod N \\
&= (m^d)^{e}\mod  N \\
&= m^{d \cdot e}\mod  N \\
&= (m^{e}\mod N)^{d}\mod N \\
&= Dec_{S_{A}}(Enc_{P_{A}}(m)) \\
&= m
\end{align}
$$

Definimos entonces la firma del mensaje $m$ por el usuario $A$ como:
$$
f := Dec_{S_{A}}(m)
$$
Solo $A$ puede generar esta firma. Cualquier usuario puede verificar si $A$ firmo un mensaje usando la clave publica $P_{A}$ de $A$

### Problema:
Firmar un mensaje $m$ puede ser lento si $m$ es un mensaje muy largo
Para solucionar este problema, se puede firmar $h(m)$ en lugar de firmar $m$, donde $h$ es una funcion de hash.

## Firmas de Schnorr

Vamos a ver un segundo esquema para firmas digitales que esta basado en el problema del logaritmo discreto

Se puede aplicar en cualquier grupo donde el problema de calcular el logaritmo discreto es difícil.

### Definiciones

Suponemos dado un grupo finito $(G, *)$ y un elemento $g \in G$ tal que $|<g>|=q$
- $G, g, q$ son públicos
- Se debe tener que $|G|$ y $q$ son números grandes

Ademas suponemos dada una función de hash $h$

### Firmar

La clave privada de un usuario $A$ es $x \in \{ 1, \dots, q-1 \}$ y su clave publica es $g^x$

1. Genera al azar $k \in \{  1, \dots, q-1 \}$ y calcular $r=g^k$
2. Calcula $v=h(r\mid\mid m)$ usando $r$ como un string
3. Calcula $s=k+v\cdot x$ interpretando $v$ como un numero natural
4. La firma de $m$ es $(v, s)$

### Verificar

Se puede verificar que $(v,s)$ es una firma de $m$ generada por $A$ de la siguiente forma:

1. Calcule $\alpha = g^{s}= g^{k+v\cdot x}=g^{k}*g^{v\cdot x}=g^k*(g^x)^v$
2. Calcule $\beta=\alpha *(g^x)^{q-v}=\alpha*(g^x)^q*(g^x)^{-v}=\alpha*(g^q)^x*((g^x)^v)^{-1}=g^k*(g^x)^v*e^x*((g^x)^v)^{-1}=g^k$
3. Verificar si $v=h(\beta\mid\mid m)=h(g^k\mid\mid m)$

### Ventajas

Son mas pequeñas que otras firmas digitales
Son faciles de combinar si varios usuarios deben firmar un documento.

## Varios usuarios firman un documento

Suponemos que $A$ y $B$ deben firmar un doc

### Usando Schnorr

- Clave privada de $A$ es $x_{1}$, clave publica $g^{x_{1}}$
- Clave privada de $B$ es $x_{2}$, clave publica $g^{x_{2}}$

Clave publica de ambos usuarios: $g^{x_{1}} * g^{x_{2}} = g^{x_{1} + x_{2}}$

Firman de la siguiente forma:

1. $A$ genera al azar $k_{1} \in \{ 1,\dots,q-1 \}$ y calcula $r_{1}=g^{k_{1}}$
2. $B$ genera al azar $k_{2} \in \{ 1,\dots,q-1 \}$ y calcula $r_{2}=g^{k_{2}}$
3. Ambos calculan $v=h((r_{1}*r_{2})\mid\mid m)$ usando $r_{1}*r_{2}=g^{k_{1}+k_{2}}$ como string
4. A calcula $s_{1}=k_{1}+v\cdot x_{1}$ interpretando $v$ como un numero natural
5. $B$ calcula $s_{2}=k_{2}+v\cdot x_{2}$ interpretando $v$ como un numero natural
6. Ambos calculan $s=s_{1}+s_{2}$, y la firma de $m$ es $(v,s)$