# Threads
## Présentation générale
### Question 1:

## Opérations de base
### Question 4: Version 2
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>  
  
#include <pthread.h>  
  
#define DUREE_MAX 5  
#define NBMAX_THREADS 4  
  
#define CHECK_T(status, msg)                        \  
 if (0 != (status))   {                            \  
   fprintf(stderr, "pthread erreur : %s\n", msg);  \  
   exit (EXIT_FAILURE);                            \  
 }  
  
void  *monThread (void * arg);  
void  bye(void);  
pthread_t tid[NBMAX_THREADS];  /* Identifiants de thread    */  
  
int main(int argc, char *argv[])  
{  
  
   atexit(bye);  
   printf("Le processus %d va créer %d threads\n",  
          getpid(), NBMAX_THREADS);  
  
   for (int i = 0; i < NBMAX_THREADS; i++)  
   {  
     CHECK_T(pthread_create (&tid[i], NULL, monThread, NULL),  
           "pthread_create(1)");  
   }  
  
   printf("\tatttente de la terminaison des threads\n");  
  
   for (int i = 0; i < NBMAX_THREADS; i++)  
   {  
     CHECK_T(pthread_join(tid[i], NULL), "pthread_join()");  
   }  
  
   return EXIT_SUCCESS;  
}  
  
void  *monThread (void * arg)  
{  
   pthread_t addressThread = pthread_self();  
   int nThread;  
   for (int i = 0; i < NBMAX_THREADS; i++)  
   {  
     if (pthread_equal(tid[i], addressThread)) nThread = i + 1;  
   }  
   for (int i = 0; i < nThread + 1; i++) printf("  ");  
   printf("Debut du thread n:%d\n", nThread);  
   sleep (rand() % DUREE_MAX + 1);  
   for (int i = 0; i < nThread + 1; i++) printf("  ");  
   printf("Fin du thread n:%d\n", nThread);  
   return NULL;  
}  
  
void bye (void)  
{  
   printf("Fin du processus %d\n", getpid());  
}
```

### Question 5: Version 3
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>  
  
#include <pthread.h>  
  
#define DUREE_MAX 5  
#define NBMAX_THREADS 4  
  
#define CHECK_T(status, msg)                        \  
 if (0 != (status))   {                            \  
   fprintf(stderr, "pthread erreur : %s\n", msg);  \  
   exit (EXIT_FAILURE);                            \  
 }  
  
typedef void * (*pf_t)(void *);  
void  *monThread (long no);  
  
void  bye(void);  
  
int main(int argc, char *argv[])  
{  
   pthread_t tid[NBMAX_THREADS];  /* Identifiants de thread    */  
   atexit(bye);  
   printf("Le processus %d va créer %d threads\n",  
          getpid(), NBMAX_THREADS);  
  
   for (long i = 0; i < NBMAX_THREADS; i++)  
   {  
     CHECK_T(pthread_create (&tid[i], NULL, (pf_t)monThread, (void *) i),  
           "pthread_create(1)");  
   }  
  
   printf("\tatttente de la terminaison des threads\n");  
  
   for (int i = 0; i < NBMAX_THREADS; i++)  
   {  
     CHECK_T(pthread_join(tid[i], NULL), "pthread_join()");  
   }  
  
   return EXIT_SUCCESS;  
}  
  
void  *monThread (long no)  
{  
   int nThread = no + 1;  
   for (int i = 0; i < nThread + 1; i++) printf("  ");  
   printf("Debut du thread n:%d\n", nThread);  
   sleep (rand() % DUREE_MAX + 1);  
   for (int i = 0; i < nThread + 1; i++) printf("  ");  
   printf("Fin du thread n:%d\n", nThread);  
   return NULL;  
}  
  
void bye (void)  
{  
   printf("Fin du processus %d\n", getpid());  
}
```

### Question 6: Version 4
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>  
  
#include <pthread.h>  
  
#define DUREE_MAX 5  
#define NBMAX_THREADS 4  
  
#define CHECK_T(status, msg)                        \  
 if (0 != (status))   {                            \  
   fprintf(stderr, "pthread erreur : %s\n", msg);  \  
   exit (EXIT_FAILURE);                            \  
 }  
  
typedef void * (*pf_t)(void *);  
void  *monThread (long no);  
  
void  bye(void);  
  
int main(int argc, char *argv[])  
{  
   pthread_t tid[NBMAX_THREADS];  /* Identifiants de thread    */  
   long * status;  
  
   atexit(bye);  
   printf("Le processus %d va créer %d threads\n",  
          getpid(), NBMAX_THREADS);  
  
   for (long i = 0; i < NBMAX_THREADS; i++)  
   {  
     CHECK_T(pthread_create (&tid[i], NULL, (pf_t)monThread, (void *) i),  
           "pthread_create(1)");  
   }  
  
   printf("\tatttente de la terminaison des threads\n");  
  
   for (long i = 0; i < NBMAX_THREADS; i++)  
   {  
     CHECK_T(pthread_join(tid[i], (void **) &status), "pthread_join()");  
     printf("-->Fin du thread n%ld avec le code %ld\n", i+1, *status);  
     free(status);  
   }  
   return EXIT_SUCCESS;  
}  
  
void  *monThread (long no)  
{  
   long * nThread = (long *) malloc(sizeof(long));  
   *nThread = no + 1;  
   for (long i = 0; i < no + 1; i++) printf("  ");  
   printf("Debut du thread n:%ld\n", no + 1);  
   sleep (rand() % DUREE_MAX + 1);  
   for (long i = 0; i < no + 1; i++) printf("  ");  
   printf("Fin du thread n:%ld\n", no + 1);  
   pthread_exit((void *) nThread);  
}  
  
void bye (void)  
{  
   printf("Fin du processus %d\n", getpid());  
}
```