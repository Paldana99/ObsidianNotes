Resolver los siguientes problemas:
- Cada usuario $A$ debe crear una clave publica $P_{A}$ y una clave secreta $S_{A}$
- $P_{A}$ y $S_{A}$ estan relacionadas: $P_{A}$ se usa para cifrar y $S_{A}$ para descifrar
- $P_{A}$ es compartida con todos los otros usuarios
![[Pasted image 20230515194407.png]]


## Cifrado con una clave publica

- $Enc$ y $Dec$ son las familias de funciones de cifrado y descifrado
- **Propiedad fundamental**:
$$
Dec_{S_{B}}(Enc_{P_{B}}(m)) = m
$$

## RSA: Un protocolo criptografico asimetrico

### Claves Publica Privadas

Las claves publicas y privadas de $A$ se construyen como:

1. Genere números primos distintos $P$ y $Q$. Defina: $N := P \cdot Q$
2. Defina $\phi(N):= (P-1)\cdot (Q-1)$
3. Genere un numero $d$ tal que $MCD(d,\phi(N))=1$, es decir primo relativo
4. Construya un numero $e$ tal que $e \cdot d \equiv 1 \mod \phi(N)$
5. Defina $S_{A}=(d,N)$ y $P_{A}=(e,N)$

Los mensajes son números, de largo $m \in \{ 1, \dots, N-1 \}$

### Funciones Cifrado Descifrado

Considere un usuario $A$ con clave publica $P_{A}=(e,N)$ y clave secreta $S_{A}=(d,N)$

Se tiene que:
$$
\begin{align}
Enc_{P_{A}}(m) &= m^{e}\mod N  \\
Dec_{S_{A}}(m) &= c^{d}\mod N
\end{align}
$$
> Ejemplo:
> ![[Pasted image 20230515195302.png]]
> ![[Pasted image 20230515195313.png]]


## Espacios de mensajes, llaves y textos cifrados

Suponiendo que se genera el numero $N$:
- Espacios de mensajes y textos cifrados: $\{ 0, \dots, N-1 \}$
- Espacios de llaves: $d,e \in N$
	- Aunque en gral se asume que $d,e \in \{ 0, \dots, \phi(N)-1 \}$

> [!note] Teorema de Fermat
> Si $p$ es un numero primo, entonces para cada $a \in \{  1, \dots, p-1 \}$, se tiene que $a^{p-1} \mod p = 1$

## Correctitud de RSA

Sean $P_{A}=(e,N)$ y $S_{A}=(d,N)$ generados según el protocolo de RSA

> [!abstract] Teorema
> Para cada $m \in \{ 0, \dots, N-1 \}$, se tiene que $Dec_{S_{A}}(Enc_{P_{A}}(m))=m$



