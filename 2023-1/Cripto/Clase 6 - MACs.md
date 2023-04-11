MAC -> Message Authentication Codes

# Autentificación de mensajes

Como autentificar mensajes?

![[Pasted image 20230409224736.png]]


## Formalización

$\mathcal{K}$ -> Espacio de llaves
$\mathcal{M}$ -> Mensajes
$\mathcal{T}$ -> Tags

Un esquema de autentificación de mensajes es una tupla $(Gen,Mac,Verify)$ tal que:

- $Gen$ es un algoritmo aleatorizado tal que, dado $1^n$, genera una llave en $\mathcal{K}$ de largo $\geq n$
- $Mac$ es una familia de funciones $Mac_{k}:\mathcal{M} \to \mathcal{T}$
- $Verify$ es una familia de algoritmos $Verify_{k}:\mathcal{T} \times \mathcal{M} \to \{ 0, 1 \}$

### Que esperamos:

Para todo $k \in \mathcal{K}$ y $m \in \mathcal{M}$, se cumple que

$$
Verify_{k}(Mac_{k}(m),m) = 1
$$

## A Jugar... Forge

Definimos el juego $Forge_{MAC}(n)$:

1. El verificador invoca $Gen(1^n)$ para generar $k$
2. El adversario envia $m_{0}\in\mathcal{M}$
3. El verificador responde $Mac_{k}(m_{0})$
4. Los pasos 2 y 3 se repiten tantas veces como quera el adversario
5. El adversario envia $(m,t)$ siendo $m$ un mensaje que no habia enviado antes

El adversario **gana** si $Verify_{k}(t, m) = 1$

### Esquema de autentificacion de mensajes seguro

Todo adversario que juega en tiempo polinomial (en $n$) tiene una probabilidad despreciable (en $n$) de ganar el **juego**.
En general se usa: *seguro = unforgeable*

