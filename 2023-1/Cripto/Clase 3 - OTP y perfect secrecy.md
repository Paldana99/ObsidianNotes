
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

Dados $a, n \in Z$ , existe un unico par de elementos $(q, r) \in Z^2$ tal que:

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

Para enviar un mensaje de largo l -> necesitamos una llave de largo l
![[Pasted image 20230309111513.png]]
Para decriptar:
![[Pasted image 20230309111934.png]]





