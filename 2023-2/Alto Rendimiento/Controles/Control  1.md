Pablo Aldana

1. ¿Qué es un FLOP y por qué se utiliza como medida de rendimiento en sistemas de supercómputo en lugar de otros parámetros como la velocidad del procesador? ¿qué criterios se usan para efectuar rankings como el Top500 ? Ejemplifique los criterios con 2 sistema de súpercómputo de la última lista Top500.

FLOP hace referencia a *floating point operation*. Se utiliza la medida de rendimiento FLOPS, es decir *floating point operation per second*. La cual mide la cantidad de operaciones de punto flotantes que puede realizar un computador por segundo. En los procesadores modernos, nos encontramos que cuentan con varios FPU (Floating Point Unit), quienes están optimizados para realizar este tipo de operaciones y son aprovechados por distintas estrategias tales como pipelining. Es por esto que medir solo la velocidad del procesador, no nos da una imagen real al momento real de realizar operaciones aritméticas. Ademas que el rendimiento se ve limitados por otras características como el *bandwidth*.
Para efectuar el ranking Top500 se mide el rendimiento en *FLOPS* de cada super computador, siguiendo el *Linpack Benchmark*. Obteniendo así el resultado luego de computar un problema denso de algebra lineal. Igualmente se cuenta con la información de la cantidad de *Cores*, la eficiencia maxima **Rmax** alcanzada en PFlop/s, la eficiencia teórica **Rpeak** en PFlop/s y la eficiencia energética (kW).

Tomando el ranking de Junio 2023:
![[Pasted image 20230903170123.png]]
![[Pasted image 20230903170108.png]]
Podemos observar que el puesto 2 le gana en solo ~100 PFlop/s, siendo que tiene mas del triple de Cores y una gasto energético mayor. Por eso la importancia de medir con Flop.

2. El reemplazo de entradas de caché puede usar estrategias de reemplazado como LRU o cómo FIFO. Ejemplifique un caso (seudocódigo) en que una estrategia LRU da mejor resultado que una estrategia FIFO. (Hint: mostrar el patrón de acceso a datos). ¿Qué tipo de cache miss es éste?

Por ejemplo en la situacion siguiente (suponemos que tenemos un cache de 2 datos maximo):
```
a = 10
b = [1, 2, 3, 4, 5]
c = [10, 20, 30, 40, 50]
for (i=1; i<5;i++) {
	 total = a + b[i] + c[i]
}
```

Notamos que por cada operación, debemos de traer 3 datos pero siempre traemos al a. Por lo que en FIFO siempre al traer el tercer dato eliminara el primero en ser puesto (que en este caso sera el a).
En cambio con LRU, mantendrá el dato a dado que se utiliza frecuentemente.
Se conoce como **Capacity Cache Miss**, dado que se queda sin espacio el cache y debe aplicar una estrategia para reemplazar.

3. ¿Cuál es el objetivo de una TLB y en qué se diferencia de los cachés tradicionales (L1, L2, L3, etc)? ¿En qué aspectos puede afectar al rendimiento de una aplicación

Una TLB permite conocer rápidamente donde se encuentra una pagina de memoria en la memoria física. Usualmente utilizando una estrategia LRU, recordara las direcciones físicas de las paginas mas utilizadas. De esta forma cuando se deba de cargar una nueva pagina, se consulta a TLB donde se encuentra de forma mas optima. Si no se encuentra, se conoce como *TLB miss*, y se debera de buscar en las tablas de paginas que son mas lentas de consultar. Se diferencia que esta no guarda datos tal como lo hacen los demas cachés, si no la dirección de una pagina. Puede afectar al rendimiento de una aplicacion, si esta requiere de nuevas paginas aleatorias constantemente, provocando varios miss y haciendo mas lento la ejecución.

4. ¿En qué consiste el fenómeno de false sharing? ¿Hay alguna manera de evitarlo o reducirlo?

False sharing se produce cuando varios threads o procesadores acceden a la misma linea de cache para distinto datos. Cada uno actualizara su dato sin tocar aquel del otro, pero al momento de registrarlo, se rechazara alguno de los dos dado que el otro dato no esta actualizado correctamente, forzando una actualización.
Para evitarlo o reducirlo podemos re-ordenar las variables de forma que no compartan lineas de cache no deseadas, o utilizar un padding de forma que se separen de linea. [Fuente](https://en.wikipedia.org/wiki/False_sharing)

5. ¿En qué afecta el uso de diferentes tamaños de stride para acceder a datos en caché?
Por ejemplo cuando tenemos datos ordenados en un array. Usualmente estos datos serán ordenados en las lineas de cache de forma continua. Por lo que si accedemos a los primeros $n$ elementos siendo $n<N$ donde $N$ es el tamaño de una linea de cache. Solo deberemos de cargar una linea de cache. Pero si utilizamos un *stride*, por ejemplo de $N$ y queremos carga los primeros 5 datos. Nos vemos forzados a cargar por tanto $5$ lineas de cache.

6. ¿En qué consiste el uso de loop tiling para acceder a datos? ¿Por qué esto puede mejorar el rendimiento?

Loop tiling, consiste en romper un loop en varios loop concatenados entre si de forma que se acceda a los datos de forma optima. Es decir que por cada iteración, vamos a aprovechar de usar todos las datos cargados en caché, tomando en consideración el tamaño de los bloques.
Esto permite mejorar el rendimiento dado que tendremos menos miss caché y deberemos de realizar menos ciclos cargando los datos en memoria. Como se muestra en la imagen, iteramos de forma que aprovechamos la memoria ya cargada.
![[Pasted image 20230903181125.png]]
