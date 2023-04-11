
Se calcula el gradiente en X y en Y. Ver el cambio de grises.
Esto nos da dos imágenes $G_{x} \quad G_{y}$

No es invariante a la rotación

![[Pasted image 20230411113850.png]]

Se calcula la magnitud y el angulo, en cada pixel

$R = \sqrt{ G_{x}^{2}+ G_{y}^2 }$
$A = \arctan\left( \frac{G_{y}}{G_{x}} \right)$

Obtenemos dos imagenes

![[Pasted image 20230411114142.png]]

Definimos un histograma en 8 direcciones:

![[Pasted image 20230411114239.png]]

Damos un rango del angulo para cada dirección:

la dirección 1 va entre [-22.5, 22.5] 

Tomamos todos los pixeles que están entre ese rango, y tomamos la suma de la magnitud de todos esos pixeles. 

Se repite para las otras direcciones:

La dirección 2 va entre [22.5, 67.5]
 etc...

Todas las sumas de las magnitudes de cada dirección, se pone en un histograma.
![[Pasted image 20230411114728.png]]

O se puede representar como:
![[Pasted image 20230411115011.png]]


Para utilizarlo, aplicamos en ventanas con traslape en la imagen. 
Asi obtenemos un descriptor, de la silueta de la imagen.
Concatenamos estos descriptores.


Paper original lo utiliza para detectar peatones.

![[Pasted image 20230411120508.png]]

![[Pasted image 20230411120529.png]]

