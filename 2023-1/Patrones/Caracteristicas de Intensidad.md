![[Pasted image 20230418114134.png]]
Average: en la región
$$
G = \frac{1}{A}\sum_{i,j\in \mathcal{R}}x'[i,j]
$$
Mean gradiente: En el contorno
$$
C = \frac{1}{L} \sum_{i,j \in l}x'[i,j]
$$
Mean segunda gradiente: En la región
$$
D = \frac{1}{A}\sum_{i,j \in \mathcal{R}}x''[i,j]
$$
Si es mas claro que el fondo, la segunda derivada sera negativa.
## Contrast Features

![[Pasted image 20230418114807.png]]

No hay pixeles en comun, entre la region y la region de entorno.

$$
G = \frac{1}{A}\sum_{i,j \in R}x[i,j]
$$
$$
G_{l}=\frac{1}{A}\sum_{i,j \in R_{l}}x[i,j]
$$
$$
K_{1} = \frac{G-G_{l}}{Gl}
$$
$$
K_{2} = \frac{G-G_{l}}{G+Gl}
$$
$$
K_{3}  = ln\left( \frac{G}{G_{l}} \right)
$$
