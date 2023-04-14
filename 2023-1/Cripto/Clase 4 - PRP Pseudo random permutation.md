
Definimos un escenario:

Consideramos un largo n fijo:
- Llaves $\mathcal{K}= \{ 0,1 \}^n$
- Mensajes: $\mathcal{M}=\{ 0,1 \}^n$
- Textos cifrados: $\mathcal{C}= \{ 0,1 \}^n$

Esquema criptografico: $(Gen, Enc, Dec)$

**Juego para definir una pseudo-random permutation**

1. **Verificador** elige $b \in \{ 0,1 \}$ con distribución uniforme (tira una moneda)
	1. si b = 0 entonces elige una clave $k \in \mathcal{K}$ según la distribución $Gen$ y define $f(x) = Enc_{k}(x)$
	2. Si b = 1, entonces elige una permutación $\pi$ con distribución uniforme y define $f(x)=\pi(x)$
2. El **adversario** elige una palabra $y \in \{  0, 1 \}^n$, el verificador responde con $f(y)$
3. El paso 2. es repetido $q$ veces
4. El **adversario** indica si $b = 0$ o $b=1$, y gana si su elección es correcta

La probabilidad de que el adversario gane depende de la cantidad de rondas $q$, si en el paso 4 tira una moneda, entonces su probabilidad de ganar es 1/2

# Pseudo-random permutation (PRP)

Decimos que $(Gen, Enc, Dec)$ es una pseudo-random permutation si no existe un adversario que pueda ganar el juego con una probabilidad significativamente mayor a 1/2


### Ejemplo
![[Pasted image 20230321225325.png]]
Ver ppt...

Se llega que en OTP el adversario con tan solo 2 rondas, va a tener una probabilidad mayor a 1/2 de poder ganar el juego.