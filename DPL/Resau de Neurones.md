# Les réseaux de neurones
## Les réseaux de neurones
Une neurone permet de séparer un ensemble en 2 parties.
- 1 neurone sépare l'ensemble avec une fonction linaire.

**Question:** Comment faire quand la frontière n'est pas linaire?

a) Couche de Neurones:

![[Drawing 2022-05-23 10.39.32.excalidraw]]

Ce réseau possède 2 couches cachées (interne ou externe qui ne sont pas "d’entrée ou sortie")
De même, on peut associe a un réseau de neurones une fonction:
$$ F: \mathbb{R}^n\to\mathbb{R}$$
$$x \to y=F (x_1...x_n)$$

De même générale, un réseau possède **n** entrée et **p** sorties:

$$F:\mathbb{R}^n\to\mathbb{R}^p$$
```ad-info
title: Remarque
- Dans une couche de neurone donnees, il n'y a qu'une seule fonction d'activation.
- Un reseau de neurones completement connecte sera dit **dense**.

```
---
**Example:** On considere un reseau de neurones a 3 neurones:

![[Drawing 2022-05-23 11.00.19.excalidraw]]
On commence par regarder la valeur théorique de chaque neurone:
Pour H1:
$$H(-x_1+3x_2)$$
Pour H2:
$$H(2x_1+x_2)$$
Pour H:
$$H(\alpha_1+\alpha_2-2)$$
On en déduit que:
$$-x_1+3x_2\geq0 \text{  et  } 2x_1+x_2\geq0$$


## La théorie:
a. Le "ou exclusif".

C'est impossible de le representer avec 1 seule neurone!
mais avec plusieurs? -> Oui, et même c'est facile!.

![[Drawing 2022-05-23 11.13.58.excalidraw]]

### Definition:
Un ensemble $A$ se dit realisable par un reseau de neurones s'il existe $R$ un reseau de neurones (d'unique fonction d'activation $H$) tq.
$$F: \mathbb{R}^2 \rightarrow \mathbb{R} \text{ associee a R verifie:}$$


Remarque:
- Aucune valeur n'est imposee sur la frontiere de $A (Fr(A))$.
- On sait deja que l'on peut realiser:
	- demi plans
	- secteurs angulaires
	- triangles
