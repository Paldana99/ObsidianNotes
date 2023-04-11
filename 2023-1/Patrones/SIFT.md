Scale Invariant Feature Transform

Se toman keypoints, y para cada uno se saca un descriptor (vector de 128) **SIFT-descriptor**

## SIFT-descriptor
- Scale Invariant
- Rotation invariant
- Illumination Invariant
- Viewpoint Invariant

## Detection of KeyPoints

Por cada imagen detecto sus keypoints.

Se aplica gausiana, y se toma los mayores.

### Descriptor

1. Encontrar un keypoint (x, y , $\sigma'$)
2. Encontrar la orientacion, usando HoG, y encontrar el angulo
3. Tomamos una ventana centrada en el keypoint de talla $1.5\sigma'$
4. Alineamos la imagen en la dirección '1'
5. Separamos en 16 celdas. 
6. A cada una le sacamos el HoG con 8 bin.
7. Concatenamos todos los histogramos, obtenemos en total 16 x 8 = 128
8. Normalizamos el vector



