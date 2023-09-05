
# Definiciones:

## Computo Paralelo:
Actividades que se ejecutan de manera no secuencial (Puede realizarse con un solo núcleo, con threads)
Incluye concurrente
## Computo concurrente:
Actividades pueden ejecutar "al mismo tiempo".  Pueden ocurrir situaciones de memoria. 

## Computo Distribuido
Actividades en diversos procesadores, usualmente con memoria separadas/distribuidas.
Incluye paralelo

## Computo Asíncrono:
Permite ejecutar tareas en distintos orden. 

![[Clase 3 2023-09-05 12.37.28.excalidraw]]

# Arquitectura
![[Pasted image 20230905124042.png]]

## SISD
CPU tradicional
## SIMD
- Utilizado en computación vectorial. 
- Instrucciones vectoriales.
- GPU (SIMT) 
- Clock compartido, todas avanzan al mismo tiempo.
## MISD
Util para algoritmos críticos, necesitas que varias maquinas verifiquen un proceso.
## MIDM
Clásico para computo paralelo.
### SPMD
Solo un proceso, pero varios datos


