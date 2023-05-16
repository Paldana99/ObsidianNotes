
**Como construir una función de hash**

Los pasos de la construcción:

- Se define una función de hash para mensajes de largo fijo, la cual es llamada **función de compresión**
- Se define un método que permite utilizar de manera **iterativa** la función de compresión para construir una función de hash para mensajes de largo arbitrario

# Función de compresión

Una primera versión, queremos construir una función de hash de largo fijo:

$h: \{ 0, 1 \}^{2n} \to \{ 0,1 \}^n$

Para construirla suponemos que tenemos:
$(Gen, Enc, Dec)$ en los espacios:

$\mathcal{M} = \mathcal{K} = \mathcal{C}=\{ 0,1 \}^n$

- Tenemos que $Enc_{k}:\{ 0,1 \}^{n}\to \{ 0,1 \}^n$ para cada $k \in \{ 0,1 \}^n$

## Primer intento

Dado $u,v \in \{ 0,1 \}^n$, definimos $h(u\mid \mid v) = Enc_{u}(v)$

- $u\mid\mid v$ es la concatenación de $u$ con $v$

Ejemplo con $n=128$ y AES

```python
from Crypto.Cipher import AES

def compresion(m: str) -> str:
	l = m[0:16]
	r = m[16:32]
	
	h = AES.new(l, AES.MODE_ECB)
	
	return h.encrypt(r)

m1 = b'Texto de prueba para compresion.'
m2 = b'TeXto de prueba para compresion.'
m3 = b'Texto de prueba para compresion?'

h1 = compresion(m1)
h2 = compresion(m2)
h3 = compresion(m3)

print(h1.hex())
print(h2.hex())
print(h3.hex())
```

```
a4eb875d9a9e589d7dfaec66bb710441
98b1b377d5915e6a80a4db533fa416c7
bbb4aafcb004f5a4a5ede95da4f84395
```

Hay un problema:

Existe un algoritmo eficiente, en terminos del parametro de seguridad $1^n$, para construir preimagenes
- No solo para el caso de AES, sino que para cualquier esquema criptografico sobre los espacios: $\mathcal{M} = \mathcal{K} = \mathcal{C}=\{ 0,1 \}^n$

## La relación entre $Enc$ y $Dec$

Si fijamos una llave $k$, y definimos las siguientes funciones

$$
f(x) = Enc_{k}(x)
$$
$$
g(x) = Dec_{k}(x)
$$
Tenemos que:
$$
\forall x \in \{ 0,1 \}^n:g(f(x))=x
$$
Tenemos que:
$$
\forall x \in \{ 0,1 \}^{n}: f(g(x)) = x
$$
Podemos concluir que:
$$
\forall k \in \mathcal{K} \forall m \in \mathcal{M} : Enc_{k}(Dec_{k}(m)) = m
$$


### Así podemos demostrar que el primer intento no es resistente a pre imagen:

Dados $u,v \in \{ 0,1 \}^n$, sea $x = h(u\mid\mid v)=Enc_u(v)$
Consideramos $u'\in \{ 0,1 \}^n$ arbitrario, y definimos $v'=Dec_{u'}(x)$

Tenemos que:
$$
h(u'\mid\mid v') = Enc_{u'}(v')=Enc_{u'}(Dec_{u'}(x)) = x
$$
#### En codigo:

```python
m = b'Texto de prueba para compresion.'
h = compresion(m)
k = b'1111111111111111'
alg = AES.new(k, AES.MODE_ECB)
c = alg.decrypt(h)
p = k + c

print(m.hex())
print(h.hex())
print(p.hex())
print(compresion(p).hex())
```

```
546578746f20646520707275656261207061726120636f6d70726573696f6e2e
a4eb875d9a9e589d7dfaec66bb710441
3131313131313131313131313131313117894bb10a97cd21175266d33b1c25b4
a4eb875d9a9e589d7dfaec66bb710441
```

## Segundo Intento: Construcción de Davies-Meyer

$$
h(u\mid\mid v) = Enc_{u}(v) \oplus v
$$

Supones un esquema criptográfico $(Gen, Enc, Dec)$ sobre $\mathcal{M}=\mathcal{K}=\mathcal{C}=\{ 0,1 \}^*$

Definimos una función de hash $(Gen', h')$:
- $Gen'(1^n)=n$ para un parámetro de seguridad $1^n$
- $(h')^n:\{ 0,1 \}^{2n}\to \{ 0,1 \}^n$ tal que para cada $u,v \in \{ 0,1 \}^n$
$$
(h')^n(u\mid\mid v)=Enc_{u}(v)\oplus v
$$

### Propiedad fundamental de la construcción de Davies-Meyer

Si $(Gen, Enc, Dec)$ es un esquema criptografico *ideal*, entonces $(Gen', h')$ es resistente a colisiones

$(Gen', h')$ es una buena alternativa para una función de compresión

## Extensión a un largo arbitrario

Supones que tenemos una función de compresión $h' : \{ 0,1 \}^{256} \to \{ 0,1 \}^{128}$

![[Pasted image 20230418104852.png]]

$h(m)$ seria el hash final.

Queremos demostrar que si $h'$ es resistente a colisiones **y** no se conoce una preimagen de $H_{0}$, entonces $h$ es resistente a colisiones

Pensemos considerando solo mensajes que son divisibles por 128.

Si encontramos una colision: $m \neq m' : h(m) = h(m')$ Pero sabemos que $h'$ es resistente a colisiones, por lo tanto todo debe ser igual, a excepcion por el $H$. Por lo tanto se llega a una contradicción, dado que los mensajes son iguales. 

### Pre Imagen $H_{0}$

Para estar **seguros** que nadie conoce una preimagen de $H_{0}$, podemos usar *nothing-up-my-sleeve number*. 
Por ejemplo: Los primeros 128 bits de la representación de $\pi$ en binario.

### Largo arbitrario

Debemos hacer un padding, hasta tener un mensaje de largo tal que sea divisible por 128.

Podemos agregar $0's$ al final, pero no es buena forma ya que es facil de encontrar colisiones $h(m) = h(m_{0})$ si $|m|$ no es divisible por 128.

#### Funcion de padding

Considere una funcion $Pad(\cdot)$ para bloques de largo $n$
- En el ejemplo $n  = 128$

Dado un mensaje $m\in \{ 0,1 \}^*$, se debe obtener que $|Pad(m)| \geq n$ y $|Pad(m)|$ es divisible por n

##### Axiomas fundamentales
- m es un prefijo de $Pad(m)$
- si $|m_{1}|=|m_{2}|$, entonces $|Pad(m_{1})|=|Pad(m_{2})|$
- si $|m_{1}|\neq|m_{2}|$, entonces el ultimo bloque de $Pad(m_{1})$ es distinto del ultimo bloque de $Pad(m_{2})$

> [!note] Función Inyectiva
> $Pad$ es una función inyectiva si satisface los axiomas fundamentales

Supones que $m_{1} \neq m_{2}$:
- Si $|m_{1}| \neq|m_{2}|$, entonces $Pad(m_{1})\neq Pad(m_{2})$ ya que el ultimo bloque de $Pad(m_{1})$ es distinto del ultimo bloque de $Pad(m_{2})$
- Si $|m_{1}|=|m_{2}|$, entonces $Pad(m_{1})\neq Pad(m_{2})$ ya que $m_{1}$ es prefijo de $Pad(m_{1})$ y $m_{2}$ es prefijo de $Pad(m_{2})$

# Construccion de Merkle-Damgard

Suponga dados:
- La función de compresión $(Gen', h')$ de *Davies-Meyer*
- Para cada $n \in N$, una función de padding $Pad_{n}$ que considera bloques con $n$ elementos y satisface los axiomas fundamentales

Vamos a definir una funcion de hash $Gen, h$ para mensajes de largo arbitrario

Consideramos un parametro de seguridad $1^n$

Tenemos que $Gen(1^{n})=s$ y
$$
h^{s}: \{ 0, 1 \}^{*}\to \{ 0,1 \}^n
$$
El valor del vector de inicialización $H_{0}$ esta contenido en $s$
- $s$ puede ser definido como $(n, H_{0})$

Dado $m \in \{ 0, 1 \}^*$, calculamos $h^s(m)$ de la siguiente forma:

1. Suponga que $Pad_{n}(m)=m_{1}m_{2}\dots m_{l}$, donde el largo de cada bloque $m_{i}$ es $n$
2. Para cada $i \in \{ 1, \dots, l \}:$
	$$
H_{i}:= (h')^n(m_{i}\mid\mid H_{i-1})
$$
3. $h_{s}(m):=H_{l}$ 

La construcción es resistente a colisiones

### Comentarios

- Se puede reemplazar la construccion de Davies-Meyer por cualquier funcion de compresion resistente a colisiones
- Podemos considerar funciones de compresion de la forma $h':\{ 0,1 \}^{p(n)}\to \{ 0,1 \}^n$ con $p(n)$ un polinomio tal que $p(n)>n$

## Que funcion de padding

![[Pasted image 20230420164434.png]]

Satisface los **dos primeros** axiomas fundamentales, pero pueden existir mensajes $m_{1}$ y $m_{2}$ tal que: $|m_{1}|\neq |m_{2}|$ y los ultimos bloques de $m_{1}$ y $m_{2}$ son iguales

Se debe tener que: $|m_{1}|\equiv |m_{2}| \mod 2$
- Si $|m_{1}|< |m_{2}|$ entonces $|m_{2}|> 2^n$

Si $n = 128$, entonces $|m| > 2^{128}$, $m$ debe tener al menos $10^{38}$ digitos, lo cuales es imposible de escribir.

# SHA-2

**Secure Hash Algorithm 2** es una familia de funciones de hash
- Se definen utilizando la construccion de *Merkle-Damgard*
- Las funciones de compresion son definidas utilizando la construccion de Davies-Meyer sobre un block cipher propio (no AES)

## SHA-256

Función de $\{ 0,1 \}^{*}$ en $\{ 0,1 \}^{256}$
Es el resultado de instanciar el parametro de seguridad en el valor 256. Tambien existe SHA-224, SHA-384, SHA-512

SHA-256 es utilizada en Bitcoin

### Bloques y estados internos

SHA-256 considera bloques de 512 bits, y sus estados internos $H_{i}$ son de 256 bits

La funcion de compresion es de la forma
$$
h': \{ 0,1 \}^{512} \times \{ 0,1 \}^{256} \to \{ 0,1 \}^{256}
$$

### Padding

Se define utilizando las ideas anteriores, pero reservando los últimos 64 bits para el largo del mensaje $m$

1. Se agrega un simbolo 1
2. Se agregan $l$ simbolos 0, donde $l$ es el menos numero natural tal que $|m|+1 + l \equiv 448 \mod 512$
3. se agrega $|m| \mod 2^{64}$

## Vector de inicialización

$H_{0}$ se define como $H_{0}^{1}H_{0}^{2}H_{0}^{3}H_{0}^{5}H_{0}^{6}H_{0}^{7}H_{0}^{8}$ donde
- $H_{0}^{i}$ tiene los primeros 32 bits de la parte decimal de la raíz cuadrada del $i$-esimo numero primo
Por ejemplo, $H_{0}^{1}$ tiene los primeros 32 bits de la parte decimal de $\sqrt{ 2 }$:
$$
H_{0}^{1} = 01101010000010011110011001100111
$$