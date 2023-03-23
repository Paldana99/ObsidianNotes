
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

