
**Como construir una función de hash**

Los pasos de la construcción:

- Se define una función de hash para mensajes de largo fijo, la cual es llamada **funcion de compresion**
- Se define un método que permite utilizar de manera **iterativa** la función de compresión para construir una función de hash para mensajes de largo arbitrario

# Función de compresión

Queremos construir una funcion de hash de largo fijo:

$h: \{ 0, 1 \}^{2n} \to \{ 0,1 \}^n$

Para construirla suponemos que tenemos:
$(Gen, Enc, Dec)$ en los espacios:

$\mathcal{M} = \mathcal{K} = \mathcal{C}=\{ 0,1 \}^n$

- Tenemos que $Enc_{k}:\{ 0,1 \}^{n}\to \{ 0,1 \}^n$ para cada $k \in \{ 0,1 \}^n$

## Primer intento

Dado $u,v \in \{ 0,1 \}^n$, definimos $h(u\mid \mid v) = Enc_{u}(v)$

- $u\mid\mid v$ es la concatenacion de u con v

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