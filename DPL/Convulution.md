# Convolution

## I: Les Filtres
**But:** 
- reduire le "bruit" du signal
- Mettre en evidence des particularites

**Outils:**
- Utilisation judicieux des moyennes.
- Utilisation de fenetres glissantes

## II: Convolution
C'est la generalisation de la notion de filtre. Puisque l'on va a utiliser de moyennes *pondérées*. Ce qui implique l'utilisation du noyau.

Formellement , on a l'utilisation de la convolution:
				- $f$ : La donnée d’entrée
				- $g$ : Le noyau

 $$\forall(x,y)\in Z, (f*g)(x,y)=\sum^{+\inf}_{i=-inf}\sum^{+\inf}_{j=-inf}f(i,j)g(x-i,y-j)$$

## III: Interets:
Le détection de structure de la première application concerne la détection de contour.
Quelque exemple de noyau: (Wikipedia) 3x3 
	- identité:	$$\begin{bmatrix}
0 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}$$
	- contour:		$$
\begin{bmatrix}
1 & 0 & -1 \\
0 & 0 & 0 \\
-1 & 0 & 1 \\
\end{bmatrix} \quad

\begin{bmatrix}
0 & 1 & 0 \\
1 & -4 & 1 \\
0 & 1 & 0 \\
\end{bmatrix} \quad

\begin{bmatrix}
1 & 1 & 1 \\
1 & 8 & 1 \\
1 & 1 & 1 \\
\end{bmatrix}
$$
		- netteté: $$\begin{bmatrix}
0 & -1 & 0 \\
-1 & 5 & -1 \\
0 & -1 & 0 \\
\end{bmatrix}$$


## IV: Aspect Mathématiques:
Soit A une matrice que représente l’entrée du **RdN**.

a) **Pooling**: Le pooling consiste a transformer une matrice dans une matrice plus petite (en essai de garder les caractéristiques) 

![[Pasted image 20220608142408.png]]

On peut croiser:
- Le **Max-Pooling** ou le matrice $A'$ hérite des coefficients les + élevés de chaque zone.
- Le **Pooling en moyenne de taille k**, est le fait de calculer la moyenne pour chaque zone de taille $k*k$ de $A$ pour obtenir un coef de $A'$.