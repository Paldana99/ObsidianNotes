
Definimos una **PRP** con poder de computación arbitrario pero cantidad fija de pasos.
Buscamos generalizar esta noción a una cantidad *polinomial* de pasos

Necesitamos introducir un parámetro de seguridad.

Un esquema es un triple $(Gen, Enc, Dec)$ de algoritmos aleatorizados donde:

$Gen(1^n)$ genera una llave $k$ tal que $|k| \geq n$

Decimos que un esquema se ve en general como una PRP:

Cuando ningún adversario eficiente puede distinguir la encriptación de una permutación al azar

**Formalmente:**

![[Pasted image 20230411101546.png]]


# AES

En el llamado a propuestas para definir el Advanced Encryption Standard (AES, 2001)

> The security provided by an algorithm is the most important factor... Algorithms will be judged on the following factors:
> 	- The extent to which the algorithm output is indistinguishable from a random permutation...


La idea es que el output sea indistinguible a una permutacion del input. 

AES es un **block cipher**, lo que significa que la encriptacion se define para bloques de largo fijo y luego se extiende a largo arbitrario

AES-128 tiene 10 rondas.

## Key Schedule

Con 10 rondas tenemos que generar 11 sub-llaves

128 bits = 16 bytes
Matriz de 4x4 bytes = 4 columnas de 4 bytes

![[Pasted image 20230411110324.png]]

![[Pasted image 20230411110444.png]]


### RotWord

Rotamos los bytes:
![[Pasted image 20230411110622.png]]

### SubWord

Por cada bytes, se le aplica una S-Box
![[Pasted image 20230411110702.png]]

#### AES S-Box:

si mostramos los bytes en hexadecimal:
Vemos por ejemplo el 4f -> 84
![[Pasted image 20230411110815.png]]

Siempre se usa la misma S-Box
La tabla viene de la multiplicacion de una matriz mas suma de un vector (ver ppt)

### Rcon

Se aplica XOR al primer byte con $rc_{i}$

![[Pasted image 20230411111344.png]]

$rc_{i}$ se define como:

![[Pasted image 20230411111930.png]]
