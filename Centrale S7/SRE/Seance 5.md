![[Drawing 2022-05-20 15.46.16.excalidraw]]

1 NIC Ethernet fait de:
- L'Ethernet V2.  `multiplex par lui meme`
- et du 802.3 `passe par 1 LLC pour multiplexer (802.28.802.1)`

Les RL ont été standardises par le STD IEEE 802...

Le fonctionnement d'1 NIC Eth, est découple  du processus: on émet  / reçoit sans CPU (même quand l'ordi est hors service.)

Un nic Ethernet implémente le protocole CSMA/CD (Carrier Sensitive Multiple Acces / Collision Direct)

## TOPO Physique des RL
- Rezo point a point. Machine -> <- Machine.
- Token Ring (IBM) : **Anneali**
	- Utilise 1 jeton pour accéder au rezo -> acces déterministe

![[Drawing 2022-05-20 16.05.32.excalidraw]]

- 73' Ethernet (Digital / Intel / Xerox) : **BUS**
	- V1 DIX protocole ALHOA
![[Drawing 2022-05-20 16.11.28.excalidraw]]
	 - V2 CSMA/CD
		 - Eth Cable gros.


## Format d'1 Trame:
Permet de transporter des donnes a la couche 3

![[Drawing 2022-05-20 16.30.58.excalidraw]]

## Protocole CSMA / CD
- écoute permanente:
	- Savoir si le temps silence > 9.6 us (TC) -> Alors droit a l'emmission.
	- Détection de collision en mode emmision.
- Sur la réception d'une trame:
	-  si l'@MAC-DST n'est pas la mienne alors je ne consomme pas. 
	- Si l'@MAC-DST est mienne, alors stockage en mémoire de la trame.
		- $<$ 32 oct : Bruit
		- 32 $=<$  $<$ 64 oct : Collision
		- $>=$ 64 oct : **Trame utile** 

### RTT : Round Trip Time
Temps moyen pour 1 bit pour faire 1 aller/retour.