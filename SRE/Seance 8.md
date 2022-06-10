# Threads

## Threads vs Process
- Thread + performant a cause du tps noyau (commutation de contexte): tps commutation entre processus > tps commutation entre 1 threads d'1 m processus
- Les threads partagent un espace de données commun.

## Check Threads
Les threads donne **0 si le résultat est positif**

```c
# define CHECK_T ( sts , msg) \
	if ( (sts) != 0 ) { perror(msg); exit(-1); }
```

## Attributs
En vue d'adapter le comportement d'1 thread -> `pthread_attr_t`
On utilisera `NULL`

- Etat de détachement
- héritage de l'ordonnancement
- politique ordonnancement / priorité
- @ / taille mémoire

## Création d'un thread:
```c
int pthread_create (pthread_t * tid, pthread_attr_t * attr, void * (*fct_thread) (void *), void * arg)
```

| Argument                        | Description                                     |    
| ------------------------------- | ----------------------------------------------- | 
| `pthread_t *`                   | renseigne le thread cree                        |
| `pthread_attr_t *`              | determine les attributs du thread a la creation | 
| `void * (*fct_thread) (void *)` | fct / traitement execute par le thread          |  
| `void **`                       | @ de l'arg                                      |  

## Atach Thread
Pour recevoir le return d'un thread.

```c
int pthread_join(pthread_t tid, void ** res)
```

| Argument  | Description        |
| --------- | ------------------ |
| `pthread_t` | thread attendu     |
| `void **`   | résultat du thread | 
