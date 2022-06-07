# Signaux
Pablo Aldana

----
# Présentation Générale
## Question 1:
```sh
kill -l
```

```
HUP INT QUIT ILL TRAP IOT BUS FPE KILL USR1 SEGV USR2 PIPE ALRM TERM STKFLT CHLD CONT STOP TSTP TTIN TTOU URG XCPU  
XFSZ VTALRM PROF WINCH POLL PWR SYS
```

## Question 2:
1
```sh
kill -l SIGTSTP
```
```
20
```

2

```sh
kill -l 10
```
```
USR1
```

## Question 3:
1. **SIGINT** permet interrompre l’exécution depuis le clavier. On tape **CTRL+C**.
2. **SIGCHLD** est destine a un processus père, lorsque le processus fils termine son exécution.
3. **SIGTSTP** C'est le signal termine par terminal, pour mettre stop a un processus, il peut être lance par l'utilisateur si il tape **CTRL+Z**

# Traitement des signaux
## Question 4:
On compile notre programme et on l’exécute en arrière plan:
```sh
gcc infini.c -o infini
./infini &
```
On peut voir les processus:
```sh
ps -l
```
```
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD  
0 S  1000    1974    1960  0  80   0 -  2974 -      pts/1    00:00:00 zsh  
0 R  1000    3271    1974 99  85   5 -   629 -      pts/1    00:04:39 infini  
4 R  1000    3483    1974  0  80   0 -  2555 -      pts/1    00:00:00 ps
```
On voit bien que infini est en arriere plan, avec pid 3271. 

Si on fait:
```sh
kill -INT 3271
ps -l
```

```
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD  
0 S  1000    3672    3658  1  80   0 -  2758 -      pts/1    00:00:00 zsh  
4 R  1000    3728    3672  0  80   0 -  2555 -      pts/1    00:00:00 ps
```

On voit qu'il a ete interrompu. Si on envoie:
```sh
kill -INT 3271
```
le processus ignore le signal et continue l'execution.
```sh
kill -USR1 3271
```
Interrompe l’exécution

```sh
kill -FPE 3271
```
Renvoie l'erreur:
`[1]  + 3829 floating point exception (core dumped)  ./infini`

## Question 5:
a) 
```sh
man 2 kill
```
b)
Selon le man:

>CONFORMING TO  
      POSIX.1-2001, POSIX.1-2008, SVr4, 4.3BSD.

c)
On peut envoyer le signal a plusieurs processus, selon le groupe, ou le parametter.
d)
Si on envoie:
```c
int resultat = kill(1234, 0)
```
Il envoie aucun signal, mais on peut verifier l'existance du PID 1234.

## Question 6:
```sh
man 2 alarm
```
On peut mettre en place une alarme, pour delivrer une signal dans temps fixe. 

## Question 7:
```sh
man 2 pause
```
Fait que le processus actuel se met en pause, jusqu’à qu'il reçoit un signal.

## Question 8:
```c
#include <unistd.h>  
  
int main(void) {  
       alarm(10);  
       pause();  
       return 0;  
}
```

On effectue `alarm(10);` qui va renvoyer un signal dans les prochains 10 secondes au meme processus. Puis on effectue `pause()` qui va a mettre en pause le process, jusqu'a qu'il recoit un signal.
Apres 10 secondes, il reçoit le signal de alarme qui par defaut va faire un arret d'execution:
`[1]    4465 alarm      ./infini_v2`

## Question 9:
```sh
whereis signal.h
```
```
signal.h: /usr/include/signal.h /usr/share/man/man0p/signal.h.0p.gz
```

Les librairies son appeller dans /usr/include

## Question 10:
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <signal.h>  
#include <unistd.h>  
  
#define TIMEOUT 10  
  
#define CHECK(sts, msg)             \  
   if (-1 == (sts)) {              \  
       perror(msg);                \  
   exit(EXIT_FAILURE);         \  
       }  
  
int main (int argc , char *argv[])  
{  
   sigset_t newMask, oldMask;  
   struct sigaction newAction;  
   int timeout = 0;  
  
   if (argc > 1) {  
       timeout = atoi(argv[1]);  
   }  
   if (timeout == 0)  
       timeout = TIMEOUT;  
  
   printf("Programme qui inhibe le Ctrl-C et s'arrête dans %d s\n",  
          timeout);  
  
   /* Initialisation du masque des signaux à ajouter                       */  
   newAction.sa_handler = SIG_IGN;  
   CHECK(sigemptyset(&newAction.sa_mask), "sigemptyset()");  
   newAction.sa_flags = 0;  
  
   CHECK(sigaction(SIGINT, &newAction, NULL), "sigaction()");  
  
   CHECK(alarm(timeout), "alarm()");  
   CHECK(pause(), "pause()");  
   exit(EXIT_SUCCESS);  
}
```

## Question 11:
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <signal.h>  
#include <unistd.h>  
  
#define TIMEOUT 10  
  
#define CHECK(sts, msg)             \  
   if (-1 == (sts)) {              \  
       perror(msg);                \  
   exit(EXIT_FAILURE);         \  
       }  
  
static void signalHandler(int numSig);  
  
int main (int argc , char *argv[])  
{  
   sigset_t newMask, oldMask;  
   struct sigaction newAction;  
   int timeout = 0;  
  
   if (argc > 1) {  
       timeout = atoi(argv[1]);  
   }  
   if (timeout == 0)  
       timeout = TIMEOUT;  
  
   printf("Programme qui inhibe le Ctrl-C et s'arrête dans %d s\n",  
          timeout);  
  
   /* Initialisation du masque des signaux à ajouter                       */  
   newAction.sa_handler = signalHandler;  
   CHECK(sigemptyset(&newAction.sa_mask), "sigemptyset()");  
   newAction.sa_flags = 0;  
  
   CHECK(sigaction(SIGINT, &newAction, NULL), "sigaction()");  
  
   CHECK(alarm(timeout), "alarm()");  
   CHECK(pause(), "pause()");  
   exit(EXIT_SUCCESS);  
}  
  
static void signalHandler(int numSig)  
{  
   switch (numSig)  
   {  
   case SIGINT:  
       printf("Le CTRL+C est desactive\n");  
       break;  
  
   default:  
       printf("Signal %d non traite\n", numSig);  
       break;  
   }  
}
```
## Question 12:
a)
On constate que le message est affiche, mais le programme est interrompu comme meme. 
`pause(): Interrupted system call`
b)
La cause est que la fonction pause se voit affecte par le traitement du signal:
>pause() returns only when a signal was caught and the signal-catching function returned.  In  this  case,  
      pause() returns -1, and errno is set to EINTR.

Alors il faut traiter que pause soit différent a -1 et voir l'erreur.
