
Geometric Features:
- location
- orientation
- shape
- size

Intensity Features:
- Grayvalues

# Geometric Features

![[Pasted image 20230321114110.png]]
Area = numero de pixeles grises
Perimetro = numero de pixeles blancos

altura = $i_{max} - i_{m\in} + 1$
ancho = $j_{max}-j_{min}+1$

Roundness:

$R = \frac{4\cdot A\cdot \pi}{L^2}$

Centro de masa: $(i_{m}, j_{m})$


**Momentos:**

$m_{rs} = \sum_{i,j\in\mathcal{R}} \quad \text{for} \quad r,s \in \mathcal{N}$

$\bar{i} = \frac{m_{10}}{m_{00}} \quad \bar{j}=\frac{m_{01}}{m_{00}}$

$u_{rs}=\sum_{i,j \in \mathcal{R}}(i-\bar{i})^r(j-\bar{j})^{s}\quad \text{for} \quad r,s \in \mathcal{N}$

### Momentos de Hu

Estos son invariantes al tamaño, rotación y ubicación

![[Pasted image 20230321120603.png]]

## Descriptores de Furier

![[Caracteristicas Geometricas 2023-03-23 11.37.16.excalidraw]]

![[Caracteristicas Geometricas 2023-03-23 11.39.06.excalidraw]]

Le aplicamos la **transformada de Fourier DFT**

$$
F_{m} = \sum_{k=0}^{L-1}f_{k}e^{\frac{-i2\pi mk}{L}}
$$
$$
f_{k}=x_{k}+iy_{k}
$$

Para un circulo perfecto:
$F_{0} = 0$
$F_{1} = \text{valor alto}$
$F_{2}=0\dots$
$F_{i}=0$

Si movemos el circulo, y no lo centramos en 0, entonces el $F_{0}\neq 0$, pero los otros quedan iguales. Por lo tanto es invariante a la posicion.

Si al circulo le agregamos frecuencia en el borde, entonces los otros valores de F van a describir este contorno. 

![[Caracteristicas Geometricas 2023-03-23 11.49.06.excalidraw]]

Es variante al tamaño
