# Processus
Pablo Aldana

# Introduction
## Question 1:
a)
```sh
head /proc/sys/kernel/pid_max
```
`4194304`

b)
```sh
head /proc/sys/kernel/threads-max
```
`62529`
c)
```sh
ps -o pid,user,etime,status,command  -p 1
```
d)
elle se situe dans `/sbin/init`. C'est la premiere commande a etre lance.

## Question 2:
```sh
size testStat
```
```
text    data     bss     dec     hex filename  
5389     672       8    6069    17b5 testStat
```
```sh
size testStat_ic
```
```
text    data     bss     dec     hex filename  
746816   23440   23016  793272   c1ab8 testStat_ic
```

## Question 3:
a) 
>Since Linux 2.6.23, the default scheduler is CFS, the "Completely Fair Scheduler".  The CFS scheduler re‐placed the earlier "O(1)" scheduler.

b)
Le *nice value* c'est une valeur donnee  a un thread, sur posix tout les threads d'un process on le meme, sur linux c'est pas le cas.
Les valeurs vont de -20 (le plus prioritaire) au +19 (moin prioritaire)

c)
>getpriority(2)  
             Return  the  nice  value  of a thread, a process group, or the set of threads owned by a specified  
             user.

d)
Avec la commande :
>nice(2)  
             Set a new nice value for the calling thread, and return the new nice value.

On peut lancer une commande avec une valeur donne de *nice*.
e)
Si on fait:
```sh
nice -n 18 echo hello
```
On voit bien que la commande s'execute

Mais si on fait:
```sh
nice -n -19 echo hello
```
On recoit:
`nice: cannot set niceness: Permission denied`
Si on veut reduire la valeur, il nous faut acces root.

# Création de processus
## Question 4:
a)
```c
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

#define CHECK(sts, msg) \
	if (-1 == (sts)) { \
		perror(msg); \
		exit(EXIT_FAILURE); \
	}

int main(int argc, char const *argv[] {
	int pid, ppid;
	CHECK(pid = (getpid()), "getpdi()");
	CHECK(ppid = (getppid()), "getppid()");
	printf("Je suis le processus..........n: %d\n", pid);
	printf("Mon pere est le processus.....n: %d\n", ppid);
	return 0;
}
```
b)
Si on exécute en ligne de commande on retrouve:
```
Je suis le processus..........n: 13731
Mon pere est le processus.....n: 13042
```
Le père est le pid de la ligne de commande actuelle.
```sh
ps -n 13042
```
On obtient:
```
   PID TTY      STAT   TIME COMMAND  
 13042 pts/1    Ss+    0:00 /usr/bin/zsh
```
Dans mon cas j'utilise zsh et pas bash.
c)
Si on execute plusieurs fois, le pid il change.

# Applications et compléments
## Question 5:
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <errno.h>

#define CHECK(sts, msg) \
	if (-1 == (sts)) { \
		perror(msg); \
		exit(EXIT_FAILURE); \
	}

void showID();

void showID() {
int pid, ppid;
	CHECK(pid = (getpid()), "getpdi()");
	CHECK(ppid = (getppid()), "getppid()");
	printf("Je suis le processus..........n: %d\n", pid);
	printf("Mon pere est le processus.....n: %d\n", ppid);
	return;
}


int main(void) {

	pid_t pidFils;
	pidFils = fork();
	switch (pidFils)
	{
		case -1:
			perror("Echec de la creation d'un processus fils");
			exit (pidFils);
		case 0:
			// Code du fils
			showID();
			exit(0);
		default:
			// Code du pere
			printf("Je suis le pere du processus..n: %d\n", pidFils);
			showID();
			break;
	}
	return 0;
}
```

## Question 6:
Si on compile le programme on voit qu'il compile au total 8.
```
Je suis le processus .............. n°15434
Mon père est le processus ......... n°15261
Je suis le processus .............. n°15436
Mon père est le processus ......... n°15434
Je suis le processus .............. n°15439
Je suis le processus .............. n°15435
Mon père est le processus ......... n°15436
Mon père est le processus ......... n°15434
Je suis le processus .............. n°15438
Mon père est le processus ......... n°15434
Je suis le processus .............. n°15441                           
Mon père est le processus ......... n°15437
Je suis le processus .............. n°15440
Mon père est le processus ......... n°15435
Je suis le processus .............. n°15437
Mon père est le processus ......... n°15435
```
## Question 7:
a)
```sh
man 3 sleep
```
C'est dans la page 3, donc c'est pas un appel systeme.

b) 
>sleep() causes the calling thread to sleep either until the number of real-time seconds specified in sec‐  
      onds have elapsed or until a signal arrives which is not ignored.

```c
sleep(10)
```
va faire que le processus va être dans un état endormi pendant 10 seconde, ou jusqu’à une signal externe fait un appel.

## Question 8:
```sh
./q5 & ; ps -l
```

```
[1] 15856  
Je suis le pere du processus..n: 15858  
Je suis le processus..........n: 15856  
Mon pere est le processus.....n: 9574  
Je suis le processus..........n: 15858  
Mon pere est le processus.....n: 15856  

F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD  
0 S  1000    9574    9560  0  80   0 -  2966 -      pts/2    00:00:01 zsh  
0 S  1000   15856    9574  0  85   5 -   659 -      pts/2    00:00:00 g5  
4 R  1000   15857    9574  0  80   0 -  2547 -      pts/2    00:00:00 ps  
1 Z  1000   15858   15856  0  85   5 -     0 -      pts/2    00:00:00 g5 <defunct>
```

On voit que le processus de pid 15858, qui est le fils crée par le fork, est dans un état **Z**. Ce état "Zombie", est a cause que le fils a finit l’exécution, et il doit attendre que le processus parent fini l’exécution (en sleep de 10s). 

## Question 9:
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <errno.h>

#define CHECK(sts, msg) \
if (-1 == (sts)) { \
perror(msg); \
exit(EXIT_FAILURE); \
}


void showID();
void proccesChild();


void showID() {
	int pid, ppid;
	CHECK(pid = (getpid()), "getpdi()");
	CHECK(ppid = (getppid()), "getppid()");
	printf("Je suis le processus..........n: %d\n", pid);
	printf("Mon pere est le processus.....n: %d\n", ppid);
	return;
}

void proccesChild(){
	char *argv [11] = {NULL};
	char *comm = "./testExecve";
	for (int i = 0; i < 10; i++)
	{
		argv[i] = (char *) malloc(3 * sizeof(char));
		int ran = rand() % 21;
		sprintf(argv[i], "%d", ran);
	}
	showID();
	CHECK(execv(comm, argv), "execve()");
}

int main(void) {
	pid_t pidFils;
	int wstatus, return_value;
	pidFils = fork();
	switch (pidFils)
	{
		case -1:
			perror("Echec de la creation d'un processus fils");
			exit (pidFils);
		case 0:
			// Code du fils
			proccesChild();
			exit(0);
		default:
			// Code du pere
			printf("Je suis le pere du processus..n: %d\n", pidFils);
			showID();
			break;
	}
	waitpid(pidFils, &wstatus, 0);
	return_value = WEXITSTATUS(wstatus);
	printf("Code de terminaison du processus...n: %d = %d\n", pidFils, return_value);
	return 0;
}
```