# Speedup

$T_p$: Tiempo de ejecución c/p unidades de cómputos
$T_{1}$: Tiempo base o secuencial

Speedup: $\frac{T_{1}}{T_{2}}$


$T_{1}=60 \text{sec}; T_{2}=30\text{sec}\implies \text{Speedup}=2$

![[Clase  2 - Estrategias 2023-08-31 12.57.31.excalidraw]]

No llegamos al ideal debido a las limitaciones del cache.

# Eficiencia

$E_{ff_{p}}=\frac{\text{Speedup}_{p}}{p}$

![[Clase  2 - Metricas 2023-08-31 13.05.45.excalidraw]]

![[Clase  2 - Metricas 2023-08-31 13.08.35.excalidraw]]

La parte paralelizable la puedo reducir infinitamente, pero la secuencial va a dominar

$F_{p} + F_{s} = 1$

Asi el tiempo total se ve:
$$
T_{p} = T_{1}\left( F_{s} + \frac{F_{p}}{p} \right)
$$
Si tendemos al inifinito los procesadores obtenemos:
$$
Tp = T_{1}(F_{s} + 1)
$$
## Ley de Amdahl

Si p tiende al infinito :

$$
\frac{T_{1}}{F_{s}T_{1}} = \frac{1}{F_{s}}
$$
$$
\text{Speedup}\to \frac{1}{0.9}=1.1
$$
El speedup, esta limitado por la eficiencia secuencial, y la eficiencia decae en una relacion $\frac{1}{p}$
