# Rezo Informatique

## Historique:
- IBM, 1970, propose SNA (système network arch) a la normalisation et deploiement  de token ring.
	- non normalise
- ISO propose norme **système (Open systeme inter connexion).**
	- fait tjs référence
- 1975 modèle **InterNet** (Inter Connexion of Networks)
	- Modèle qui vient de OSI, mais plus simple.
	- Plus industriel, intervention de **IEEE** (mise en place de Standard)

Les trois modèle propose une pile de **protocoles**, principe de modèle en couche, si un étage marche pas, on continue pas.

## OSI et Internet
![[OSI - Internet]]
- 1 Couche (i) rend service a la couche (i+1) en s'appuyant sur les services (i-1).
- Chaque couche fonctionne selon un protocole.
- Modèle applicatif **Client / Server**. Requête a initiative du Client.

### Encapsulation
Chaque couche rajoute une encapsulation (enveloppe) et seulement la même couche peut "ouvrir" la couche qui lui correspond. 
Chaque couche gère un **PDU** (Protocol Data Unit).
PDU = PDU de couche superieur + ICL (Info controleur)

### Multiplexage
![[Multiplexage]]

### Couches OSI:
1. Convertir Signal numérique vers physique ou inversement. Début et fin transmission.
2. Dire sur un groupe d'information reçu, acces CTRL permet de dire voici un trame. Et permet de donne le paque a la couche superieur.
3. -

### Couches Internet:
1. Ethernet

Routage entre les différents rezos en forme de étoile. 