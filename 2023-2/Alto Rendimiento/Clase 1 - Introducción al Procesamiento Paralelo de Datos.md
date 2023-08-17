
# Componentes de Von Neumann:

- CPU
- Memoria
- I/O - E/S
- Se conectan a traves de buses

Tenemos un flujo de datos y flujo de instrucciones. Con una sola CPU, debemos hacer una instruction a la vez. 
Con varias podemos separar estas instrucciones, esto se conoce como **paralelismo de instrucciones**. Al hacerlo debemos mantener coherencia. Por ejemplo:

```
b = 5
r1 = 1 + b
r2 = r1 + 2
```

La instruccion 3, depende directamente de la dos por lo que podria crear un problema.

Otro ejemplo (**Paralelismo de Datos**), si tenemos n datos. **SIMD** (Single Instruction Multiple Data)
```
a[0] = b[0] + c[0]
a[1] = b[1] + c[1]
...
```

Un ciclo:

Fetch Instruc -> Acceso Memoria
Decode -> CPU
Fetch Data -> Acceso Memoria
Ejecucion -> CPU
Store -> Acceso Memoria

Hay un cuello de botella con el acceso de memoria (es mas lento), para eso utilizamos cache.

Ejecución **Out-of-order** podemos ejecutar instrucciones en orden random, para optimizar. Se pueden realizar operaciones mientras se espera que el dato se cargue desde la memoria (siempre que se mantenga consistencia)

## Pipelining

![[Pasted image 20230810125854.png]]

## Branch-prediction
intentar adivinar el resultado de una operación para adelantar el bloque siguiente. En caso de error de la predicción, se resuelve de nuevo con el valor correcto y se usa el tiempo normal estimado.

## Prefetching
pre cargar en cache los datos que se van a utilizar previamente.
Esto se aprovecha si se utiliza localidad de memoria:
- Temporal: Guardo en cache los datos que use recientemente. (Asumiendo que las volveré a usar)
- Espacial: Guardo en memoria fisica cercana, por ejemplo arrays.

## Floating Point Unit
Operaciones complejas, varios ciclos de un CPU. Se mide FLOP/s.
El tiempo de computo $Tiempo(n): L * n * t$
- $L:$ numero de etapas (stages)
- $t :$ *clock cycle time*
- $n:$ numero de operaciones

Tasa de operaciones : $\frac{T(n)}{n} = \frac{1}{l*t}$

Usando Pipelining, el tiempo de pipeling: $l * t + (n-1)$
Asi la tasa de operaciones con pipelining:
$$
\frac{n}{l*t + (n-1)} \to_{n \to \inf} \frac{1}{s-1}
$$


**ILP**: Instruction Level Parallelism


Cantidad de FPU (Floating Point Unit) -> Influye en FLOP/s

## Peak Performance
Rendimiento teórico máximo (se mide en **Flop/s**)

Peak performance: clockspeed × \#FPUs

- clock speed
- \#FPUs
- Velocidad de buses / Ancho de banda -> Latencia
- Tamaño de cache
- Canales

## Real Performance
Se corren operaciones reales  (se mide en **Flop/s**), benchmark y se analiza el resultado

Por ejemplo:
- LINPACK -> Algebra lineal
- HPCE -> Patrones de paralelismo

TOP500  -> Mejores computadores segun rendimiento operaciones
GREEN500 -> Mejores computadores según rendimiento energetico

## Caché
![[Pasted image 20230817124443.png]]


- Registros se acceden por instrucciones de assembler 
- Movimientos de cache-memoria se hace por hardware
- Es compartido entre varios cores, gasto en coherencia -> penalización de velocidad

### Cache Miss
- Compulsory miss (obligatoria), busco pero no habia nada.
- Capacity miss, cuando esta lleno y tengo que ver cual sobrescribir
- Conflict miss, ambos datos se quieren usar pero se quieren almacenar en el mismo lugar.
- Invalidation miss (en multicore), el valor se actualiza por otro núcleo.


