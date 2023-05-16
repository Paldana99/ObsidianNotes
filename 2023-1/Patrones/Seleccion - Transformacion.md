## PCA

## ICA Indeendent Component Analysis

La diferencia con PCA, elimina correlaciones pero ademas dependencias de mayor orden. Es decir que las variables sean independientes.

## PLSR Partial Least Squares Regression

Este considera, la variable $y$.
$$
\begin{align}
X &= TP^{T}+E \\
Y &= UQ^{T} + F 
\end{align}
$$
Las descomposiciones se $X$ e $Y$ se hacen con el fin de maximizar la covarianza entre T y U.

Las matrices $P$ y $Q$ son ortogonales. Las matrices $E$ y $F$ corresponden al error.

La idea e buscar $T$, que es la transformada de X

# Esquema General para Selección de Características:

1. Colección de datos originales
2. Extracción de características
3. Definición de set de datos de Training/Testing
4. Cleaning
5. Normalización
6. Selección de características
7. Diseño del Clasificador con Training
8. Prueba del Clasificador con Testing
9. Medición de desempeño