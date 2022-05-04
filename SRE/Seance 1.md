# Introduction
## Seances:
- 1 Shell
- 2 C - lib
- 3 et 5: Prog concurrante
	- POSIX
- 4 et 5: Architecture
	- 2 modeles
	- Ethernet - TCP/IP

## OS:
**Carte** **mere**:
	memoire cache, processeur, registre
communique avec RAM (Random Access Memory)

Les deux communique a travers de deux BUS:
	BUS @ et BUS DATA
Pour connecter different controleur (interface, graphique, SATA ...) qui seront connecte aux differents periphierique

![[Pasted image 20220504093735.png]]
![[Pasted image 20220504095601.png]]

[[Noyau]]

Modele en couche, si un etage fonctionne pas, il marche plus. 
BIOS ecrite en ROM (pas le cas des nouvelles systemes)
Noyau systemes: Il a tout ce qu'il faut pour gerer, exploiter le microprocesseur (gestion processeur) qui va etre transformer en **Thread**.
Le noyeu est multitache.

**Thread**: En verifie si il y a une interruption, et apres on fait une instruction. Ceci se repete. Si il y a une interruption -> execution du traitement associe. Quand on finit ce traitement, on retourne a l'instruction ou il a ete interrompu.  

Apres noyau il y a bibliotheque qui vont abstraire/masquer le noyau, et ensuite il y a le **SHELL** qui va permettre lancer les autres process.

### **SHELL**: 
Interpreteur de commande en ligne, qui va lancer les processus correspodant. Qui vont acceder a traver les bibliotheques. 

#### man
/usr/man
 - man1 : cdes user
 - man2: appel systeme
 - man3: biblio C
 - ...
 - man7: TDPO sum les mecanismes systemes
 - man8: cdes user admin

