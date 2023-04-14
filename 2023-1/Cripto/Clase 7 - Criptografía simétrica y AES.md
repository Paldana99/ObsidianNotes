
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

## AES

![[Pasted image 20230413164958.png]]

Se dice que AES tiene un *estado* de 128 bits, que es lo que se va modificando en cada paso. Este estado se presenta como una martriz de 4x4 bytes

![[Pasted image 20230413165149.png]]

### SubBytes

Se le aplica a cada byte, la **AES S-Box**

### ShiftRows

![[Pasted image 20230413165251.png]]

Se desplazan a la izquiera los bytes n pasos segun la fila.
Fila 1 = 0 
Fila 2 = 1
Fila 3 = 2
Fila 4 = 3

### MixColumns

Se multiplica la matriz segun un operador especial
![[Pasted image 20230413195827.png]]

Donde:

$01= 1$
$02 = x$
$03 = x + 1$

![[Pasted image 20230413195919.png]]

Otra forma de hacer:
1. Pasar todo a binario
2. Se multiplica:
	1. Si es por $01$ -> Queda igual
	2. Si es por $02$ -> Se hace 1 shift a la izquierda $\ll$, si un bit queda fuera entonces se XOR con 0x1B
	3. Si es por $03$ -> Equivalente a $3 \times x = (2 \oplus 1) \times x = (2\times x) \oplus x$
3. Luego se hace XOR, entre los 4 resultados.
4. Se pasa a hexadecimal.

## Decriptar AES

### Invertir MixColumns
Misma multiplicacion pero con la siguiente matriz :
![[Pasted image 20230413200655.png]]

# Modos de Operación

Para extender AES a un largo arbitrario

Suponemos un mensjae que se divide en $l$ bloques.

$m= m_{0}m_{1}\dots m_{l-1}$

Donde cada $m_{i}$ tiene 128 bits. Si $|m|$ no divide a 128, se le agrega un *padding*.

## ECB Electronic Code Book

encriptamos bloque por bloque, esto da un problema que si se cambia un solo bloque, el cifrado solo cambia en esa misma posicion.

![[Pasted image 20230413201259.png]]

## CBC Cipher Block Chaining

Se hace XOR entre los bloques, pero si se manda el mismo mensaje dos veces, el atacante sabe que es el mismo puesto que no cambia.

![[Pasted image 20230413201503.png]]

### Juego

1. El verificador toma $k$ en base a $Gen(1^n)$
2. El adversario puede preguntar lo que quiera a $Enc_{k}(\cdot )$
3. El adversario genera mensajes $m_{0}$ y $m_{1}$ y los envía al verificador
4. El verificador elige $b \in \{ 0, 1 \}$ y envía al adversario $c = Enc_{k}(m_{b})$
5. El adversario puede preguntar lo que quiera a $Enc_{k}(\cdot)$
6. El adversario elige $b' \in \{ 0, 1 \}$ y gana si $b = b'$

La función de encriptación **debe** ser aleatorizada

Un esquema criptográfico es seguro frente a ataques de texto elegido (CPA-secure) si:

Para todo adversario $A$ de tiempo polinomial
$$
|\frac{1}{2}-Pr[\text{A gane el juego}]|
$$
es una función descpreciable en $n$

## CBC (mejorado)

Se incluye un vector de inicialización aleatorio, 128 bits que se comparten cada vez que se encripta un mensaje.

![[Pasted image 20230413202235.png]]

> [!abstract] Teorema
> Si $Enc$ es una PRP, entonces el esquema CBC es CPA-secure
> 


