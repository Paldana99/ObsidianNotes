
Tres pasos:
1. Coding
2. Mapping
3. Histogram

El histograma LBP de imágenes parecidas, son parecidos.
Varia con la rotación en la forma básica
Es invariante a la escala y a la iluminación

### Coding

Se pone cada pixel con una escala de gris del 1-10. Luego se hace una ventana de 3x3 y comparo el pixel centro con los demás. 
![[Pasted image 20230323123707.png]]

Luego a lo resultado se convierte el byte por una representación decimal
![[Pasted image 20230323123758.png]]

### Mapping

Mapeamos la ventana de bits, a unos patrones según cuantos cambios encontramos de 0 a 1 y de 1 a 0.
![[Pasted image 20230323124107.png]]
![[Pasted image 20230323124122.png]]

Los U = 0 y U = 2  son patrones uniformes, los 4, 6, y 8 son uniformes (ruido)
![[Pasted image 20230323124233.png]]
Los ruidos se mapean a 58 para todo tipo de patrón.


### Histogram
![[Pasted image 20230323124253.png]]
Se ponen todos los pixeles según su numero de patrón, y este puede servir para comparar con otras imágenes.

