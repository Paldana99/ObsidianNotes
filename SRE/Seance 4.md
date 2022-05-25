# PSY
## Gestion des erreurs
Macro fonction:

```c
#define CHECK(sts, msg) if ((sts) == -1) {perror(msg); exit(-1)};
```

Dans le code:

```c
CHECK(nbCar=read(...), "Erreur de lecture");
```

> [!warning] Parenthèse
> Il faut mettre une parasynthèse dans **(sts)** pour bien faire la comparaison.
> 

## Multitâches - Processus
Un processus est une instance dynamique d'un programme (en cours d’exécution): une tache système. Il est caractérise par un **état** et un **espace mémoire** qui lui son *associes.*

![[Drawing 2022-05-18 11.05.40.excalidraw]]
La table des processus est organise en arbre (père / fils).

![[Drawing 2022-05-18 11.14.14.excalidraw]]
Thread: Un fils d'instructions d'un programme.
Un processus peut être mono-thread ou avoir plusieurs threads. Dans le cas de plusieurs, ils vont partager la mémoire.
![[Pasted image 20220518114728.png]]