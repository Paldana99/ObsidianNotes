## Que algoritmos eficientes necesitamos para ejecutar RSA
- Generación aleatoria de números primos
- Operaciones básicas
- Máximo común divisor
- Generación de un primo relativo
- Algoritmo extendido de Euclides
- Exponenciación rápida

Se encripta en Base 64, los primeros 4 bytes, indica el largo de lo siguiente y asi...

## Generar un numero primo

Sea $\pi(n)$ la cantidad de números primos menores o iguales a $n$
- Por ejemplo $\pi(10) = 4$ y $\pi(19) = 8$

> [!abstract] Teorema
> $\lim_{ n \to \infty } \frac{\pi(n)}{\frac{n}{ln(n)}}=1$

Por lo tanto: $$\pi(n) \approx \frac{n}{ln(n)}$$
Probabilidad de obtener un numero primo al azar?
$$
Pr_{x \sim U(1,n)}(x \text{ sea primo}) = \frac{1}{ln(n)}
$$

Por ejemplo para generar un numero primo de 400 dígitos:
$$
Pr_{x \sim U(10^{399},10^{400}-1)}= \frac{\frac{10^{400}-1}{ln(10^{400}-1)} - \frac{10^{399}-1}{ln(10^{399}-1)}}{10^{400}-10^{399}}
$$
Aprox: $0.001085$ -> Se necesitan 922 intentos para obtener un numero primo, lo cual es rapido. Pero falta saber como tener un test de primalidad rapido.

### Generar un primo relativo al azar

Queremos generar un primo relativo $a$ de un numero dado $n$

Sea $\phi(n)$ la cardinalidad del conjunto
$$
\{ a \in \{ 0,\dots ,n-1 \} \mid MCD(a,n) = 1 \}
$$
> [!abstract] Teorema
> $\phi(n)$ es $\Omega\left( \frac{n}{log(log(n))} \right)$

Podemos entonces generar un primo relativo a n usando el mismo argumento que para los primos
- Generamos números al azar $a \in \{  0, \dots, n-1 \}$ y verificamos si $MCD(a,n) = 1$

