# Introduction
## Seances:
- 1 Shell
- 2  C - lib
- 3 et 5: Prog concurrante
	- POSIX
- 4 et 5: Architecture
	- 2 modeles
	- Ethernet - TCP/IP

## E-learning
#### Linux
- auto evaluation: exam chap (note assiduite)
- evaluation Mid - Final
#### Lge C
- auto evaluation
#### Rezo
- auto evaluation
	- xam definitif chaque chap
	- exam final
- exam pratique
#### PSY
- support
- proc
- sig
- thread
- simphony

#### Derniere seance:
- final sur rezos et PSY

## OS:
**Carte** **mere**:
	memoire cache, processeur, registre
communique avec RAM (Random Access Memory)

Les deux communique a travers de deux BUS:
	BUS @ et BUS DATA
Pour connecter different controleur (interface, graphique, SATA ...) qui seront connecte aux differents periphierique

![[Pasted image 20220504093735.png]]
![[Pasted image 20220504095601.png]]
![[Noyau]]

Modele en couche, si un etage fonctionne pas, il marche plus. 
BIOS ecrite en ROM (pas le cas des nouvelles systemes)
Noyau systemes: Il a tout ce qu'il faut pour gerer, exploiter le microprocesseur (gestion processeur) qui va etre transformer en **Thread**.
Le noyeu est multitache.

**Thread**: En verifie si il y a une interruption, et apres on fait une instruction. Ceci se repete. Si il y a une interruption -> execution du traitement associe. Quand on finit ce traitement, on retourne a l'instruction ou il a ete interrompu.  

Apres noyau il y a bibliotheque qui vont abstraire/masquer le noyau, et ensuite il y a le **SHELL** qui va permettre lancer les autres process.

----

### **SHELL**: 
Interpréteur de commande en ligne, qui va lancer les processus correspondant. Qui vont accéder a travers les bibliothèques. 

	COMMANDE + OPTIONS + ARG(S) 

#### man
/usr/man
 - man1 : cdes user
 - man2: appel systeme
 - man3: biblio C
 - ...
 - man7: TDPO sum les mécanismes systèmes
 - man8: cdes user admin

```sh
man numero_section func
```
Si on ne sait pas ou chercher: permet d'avoir un descriptif des différents manuel qui comporte le mot clé, on peut filtrer les résultat grâce a un pipe **|**  et grep
```sh
man -k key_word | grep key_word2
```
**more** : permet de montrer par pages
```sh
ls -lR | more
```

`CTRL C`
`CTRL D` END (fichier)
`CTRL Z` pause (stopped)
`jobs` avoir les jobs qui ont été stoppe.
`bg %1` background, mettre en arrière plan un job (id 1 dans l'example)
`CTRL S/Q` arrêt/reprise affichage
`CTRL A/E` début/fin ligne