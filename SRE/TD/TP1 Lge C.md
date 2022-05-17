# Développement en C sous UNIX
## Question 1
```C
#include <stdio.h>

  

int main() {

char carLu ; /* ... */

  

int nbWords = 0;

int nbLines = 0;

  

while ( ( carLu = getchar () ) != EOF)

{

	if (carLu == ' ' || carLu == '\n') nbWords++;
	
	if (carLu == '\n') nbLines++;

}

	printf("nbWords: %i, nbLines: %i", nbWords, nbLines);
		
	return 0;

}
```

## Question 2
```sh
ps -u 1000 | ./ex.exe    
#nbWords: 1470, nbLines: 107
cat /etc/passwd | ./ex.exe    
#nbWords: 64, nbLines: 30
```
## Question 3
```c
#include <stdio.h>

int main() {

char carLu ; /* ... */
int nbWords = 0;
int nbLines = 0;
int isWord = 0; // 0 -> False ; 1 -> True

while ( ( carLu = getchar () ) != EOF)
{
	
	switch (carLu)
	
	{
	
	case '\n':
	
		nbLines++;
		
		break;
	
	case '\t':
	case ' ':
		
		if (isWord)
		
		{
		
			isWord = 0;
			nbWords++;
		}
	
	break;

	default:
	
		isWord = 1;
		break;
	
	}
	
	}
	
	printf("nbLines: %i, nbWords: %i \n", nbLines, nbWords);
	
	return 0;

}
```
## Question 4:
```sh
cat Exo2.c | ./ex.exe  
# nbLines: 38, nbWords: 77
cat Exo2.c | wc
#   38      80     616
```
On peut voir qu'il y a une différence dans le comptage de mot.

## Question 5:
```C
#include <stdio.h>

  

int main() {

char carLu ; /* ... */

  

int nbWords = 0;

int nbLines = 0;

int nbChar = 0;

int nbCharAlpha = 0;

  

int isWord = 0; // 0 -> False ; 1 -> True

  

int nbAlpha[26] = {0}; //On intialise a 0 le tableau de 26.

  

while ( ( carLu = getchar () ) != EOF)

{

nbChar++;

switch (carLu)

{

case '\n':

nbLines++;

break;

case '\t':

case ' ':

if (isWord)

{

isWord = 0;

nbWords++;

}

break;

default:

isWord = 1;

if ((carLu >= 'a') && (carLu <= 'z')) {

nbCharAlpha++;

nbAlpha[carLu - 'a']++;

}

else if ((carLu>= 'A') && carLu && (carLu <= 'Z')) {

nbCharAlpha++;

nbAlpha[carLu - 'A']++;

}

break;

}

}

  

printf("Nombre caracteres..................%i\n", nbChar);

printf("Nombre caractere alphabetiques.....%i\n", nbCharAlpha);

printf("Nombre mots........................%i\n", nbWords);

printf("Nombre lignes......................%i\n", nbLines);

  

printf("+-------+-------+---------+\n");

printf("| Lettre| Nombre|Frequence|\n");

printf("+-------+-------+---------+\n");

for (int i; i < 26; i++) {

printf("| %c | %i | %2.3f%% |\n", i + 'a', nbAlpha[i], 100.0 * nbAlpha[i] / nbCharAlpha);

printf("+-------+-------+---------+\n");

}

  

return 0;

}
```

## Question 6:
### a)
```sh
cat ./Tests/Question\ 6/disparition1.txt | ./ex.exe
```
Le résultat:

	Nombre caracteres..................853  
	Nombre caractere alphabetiques.....634  
	Nombre mots........................133  
	Nombre lignes......................12  
	+-------+-------+---------+  
	| Lettre| Nombre|Frequence|  
	+-------+-------+---------+  
	|   a  |   72  |   11.356%  |  
	+-------+-------+---------+  
	|   b  |   5  |   0.789%  |  
	+-------+-------+---------+  
	|   c  |   17  |   2.681%  |  
	+-------+-------+---------+  
	|   d  |   16  |   2.524%  |  
	+-------+-------+---------+  
	|   e  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   f  |   12  |   1.893%  |  
	+-------+-------+---------+  
	|   g  |   11  |   1.735%  |  
	+-------+-------+---------+  
	|   h  |   1  |   0.158%  |  
	+-------+-------+---------+  
	|   i  |   95  |   14.984%  |  
	+-------+-------+---------+  
	|   j  |   3  |   0.473%  |  
	+-------+-------+---------+  
	|   k  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   l  |   41  |   6.467%  |  
	+-------+-------+---------+  
	|   m  |   9  |   1.420%  |  
	+-------+-------+---------+  
	|   n  |   56  |   8.833%  |  
	+-------+-------+---------+  
	|   o  |   56  |   8.833%  |  
	+-------+-------+---------+  
	|   p  |   16  |   2.524%  |  
	+-------+-------+---------+  
	|   q  |   15  |   2.366%  |  
	+-------+-------+---------+  
	|   r  |   34  |   5.363%  |  
	+-------+-------+---------+  
	|   s  |   41  |   6.467%  |  
	+-------+-------+---------+  
	|   t  |   55  |   8.675%  |  
	+-------+-------+---------+  
	|   u  |   53  |   8.360%  |  
	+-------+-------+---------+  
	|   v  |   15  |   2.366%  |  
	+-------+-------+---------+  
	|   w  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   x  |   4  |   0.631%  |  
	+-------+-------+---------+  
	|   y  |   7  |   1.104%  |  
	+-------+-------+---------+  
	|   z  |   0  |   0.000%  |  
	+-------+-------+---------+

```sh
cat ./Tests/Question\ 6/disparition2.txt | ./ex.exe
```
	Nombre caracteres..................679  
	Nombre caractere alphabetiques.....510  
	Nombre mots........................102  
	Nombre lignes......................15  
	+-------+-------+---------+  
	| Lettre| Nombre|Frequence|  
	+-------+-------+---------+  
	|   a  |   57  |   11.176%  |  
	+-------+-------+---------+  
	|   b  |   8  |   1.569%  |  
	+-------+-------+---------+  
	|   c  |   15  |   2.941%  |  
	+-------+-------+---------+  
	|   d  |   14  |   2.745%  |  
	+-------+-------+---------+  
	|   e  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   f  |   4  |   0.784%  |  
	+-------+-------+---------+  
	|   g  |   9  |   1.765%  |  
	+-------+-------+---------+  
	|   h  |   6  |   1.176%  |  
	+-------+-------+---------+  
	|   i  |   56  |   10.980%  |  
	+-------+-------+---------+  
	|   j  |   1  |   0.196%  |  
	+-------+-------+---------+  
	|   k  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   l  |   26  |   5.098%  |  
	+-------+-------+---------+  
	|   m  |   11  |   2.157%  |  
	+-------+-------+---------+  
	|   n  |   52  |   10.196%  |  
	+-------+-------+---------+  
	|   o  |   54  |   10.588%  |  
	+-------+-------+---------+  
	|   p  |   17  |   3.333%  |  
	+-------+-------+---------+  
	|   q  |   4  |   0.784%  |  
	+-------+-------+---------+  
	|   r  |   34  |   6.667%  |  
	+-------+-------+---------+  
	|   s  |   56  |   10.980%  |  
	+-------+-------+---------+  
	|   t  |   23  |   4.510%  |  
	+-------+-------+---------+  
	|   u  |   53  |   10.392%  |  
	+-------+-------+---------+  
	|   v  |   7  |   1.373%  |  
	+-------+-------+---------+  
	|   w  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   x  |   3  |   0.588%  |  
	+-------+-------+---------+  
	|   y  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   z  |   0  |   0.000%  |  
	+-------+-------+---------+

Dans les deux on peut voir qu'il y a pas de 'e'

### b)
```sh
cat ./Tests/Question\ 6/revenentes.txt | ./ex.exe
```
	Nombre caracteres..................428  
	Nombre caractere alphabetiques.....306  
	Nombre mots........................60  
	Nombre lignes......................7  
	+-------+-------+---------+  
	| Lettre| Nombre|Frequence|  
	+-------+-------+---------+  
	|   a  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   b  |   1  |   0.327%  |  
	+-------+-------+---------+  
	|   c  |   9  |   2.941%  |  
	+-------+-------+---------+  
	|   d  |   15  |   4.902%  |  
	+-------+-------+---------+  
	|   e  |   93  |   30.392%  |  
	+-------+-------+---------+  
	|   f  |   3  |   0.980%  |  
	+-------+-------+---------+  
	|   g  |   3  |   0.980%  |  
	+-------+-------+---------+  
	|   h  |   4  |   1.307%  |  
	+-------+-------+---------+  
	|   i  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   j  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   k  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   l  |   17  |   5.556%  |  
	+-------+-------+---------+  
	|   m  |   11  |   3.595%  |  
	+-------+-------+---------+  
	|   n  |   21  |   6.863%  |  
	+-------+-------+---------+  
	|   o  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   p  |   10  |   3.268%  |  
	+-------+-------+---------+  
	|   q  |   2  |   0.654%  |  
	+-------+-------+---------+  
	|   r  |   26  |   8.497%  |  
	+-------+-------+---------+  
	|   s  |   50  |   16.340%  |  
	+-------+-------+---------+  
	|   t  |   31  |   10.131%  |  
	+-------+-------+---------+  
	|   u  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   v  |   7  |   2.288%  |  
	+-------+-------+---------+  
	|   w  |   1  |   0.327%  |  
	+-------+-------+---------+  
	|   x  |   1  |   0.327%  |  
	+-------+-------+---------+  
	|   y  |   0  |   0.000%  |  
	+-------+-------+---------+  
	|   z  |   1  |   0.327%  |  
	+-------+-------+---------+
On voit que seulement la voyelle 'e' est utilise.

Un *lipogramme* c'est une figure de style qui consiste a écrire un texte avec l'absence d'une ou plusieurs lettres.

### c)

	Nombre caracteres..................47  
	Nombre caractere alphabetiques.....37  
	Nombre mots........................8  
	Nombre lignes......................1  
	+-------+-------+---------+  
	| Lettre| Nombre|Frequence|  
	+-------+-------+---------+  
	|   a  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   b  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   c  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   d  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   e  |   5  |   13.514%  |  
	+-------+-------+---------+  
	|   f  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   g  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   h  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   i  |   3  |   8.108%  |  
	+-------+-------+---------+  
	|   j  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   k  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   l  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   m  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   n  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   o  |   2  |   5.405%  |  
	+-------+-------+---------+  
	|   p  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   q  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   r  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   s  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   t  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   u  |   5  |   13.514%  |  
	+-------+-------+---------+  
	|   v  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   w  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   x  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   y  |   1  |   2.703%  |  
	+-------+-------+---------+  
	|   z  |   1  |   2.703%  |  
	+-------+-------+---------+
On voit que toutes les lettres son utilisée. C'est a dire c'est un *pangramme*.

## Question 7:
```C
char * aveCesar(const char * *chaine);

char * dyhCesar(const char * *chaine);
```

## Question 8:
```c
#include <string.h>

#include <ctype.h>

#include <stdio.h>

  

char * aveCesar(const char * chaine);

char * dyhCesar(const char * chaine);

  
  

char * aveCesar(const char * chaine) {

  

char * result = strdup(chaine);

  

char *p;

  

for (p = result; *p != '\0'; p++) {

if (isalpha(*p))

{

if (islower(*p)) *p = (((*p - 'a') + 3) % 26) + 'a';

else if (isupper(*p)) *p = (((*p - 'A') + 3) % 26) + 'A';

}

}

return result;

}

  

void test_aveCesar (void)

{

printf ("%s\n", aveCesar (" ABCDEFGHIJKLMNOPQRSTUVWXYZ "));

printf ("%s\n", aveCesar ("TU QUOQUE MI FILI"));

printf ("%s\n", aveCesar ("VENI VIDI VICI"));

printf ("%s\n", aveCesar ("XIBX GXZQX BPQ"));

printf ("%s\n", aveCesar ("PF SFP MXZBJ MXOX YBIIRJ "));

}

  

int main(int argc, char const *argv[])

{

test_aveCesar();

return 0;

}
```
Resultat:

	DEFGHIJKLMNOPQRSTUVWXYZABC    
	WX TXRTXH PL ILOL  
	YHQL YLGL YLFL  
	ALEA JACTA EST  
	SI VIS PACEM PARA BELLUM

## Question 9:
```C
char * dyhCesar(const char * chaine) {

char * result = strdup(chaine);

char *p;

for (p = result; *p != '\0'; p++) {

	if (isalpha(*p))
	
		{
	
		if (islower(*p)) *p = (((*p - 'a') - 3 + 26) % 26) + 'a';
		
		else if (isupper(*p)) *p = (((*p - 'A') - 3 + 26) % 26) + 'A';
		
		}

	}
	
	return result;

}
```

	ABCDEFGHIJKLMNOPQRSTUVWXYZ    
	SATOR    
	AREPO    
	TENET    
	OPERA    
	ROTAS    
	DEMO DES MAUX DES MOTS  
	VAE VICTIS

## Question 10:
On perd de la mémoire, car on fait une copie de l'original.

## Question 11:
### a)
```c
char * cesar(const char * chaine, int decalage);
```
### B)
```c
#define ALPHABSZ = 26;
```
### C)
```c
char * cesar(const char * chaine, int decalage) {

char * result = strdup(chaine);

char * p;

  

if (decalage >= 0) {

for (p = result; *p != '\0'; p++) {

if (isalpha(*p))

{

if (islower(*p)) *p = (((*p - 'a') + decalage) % ALPHABSZ) + 'a';

else if (isupper(*p)) *p = (((*p - 'A') + decalage) % ALPHABSZ) + 'A';

}

}

return result;

}

else {

for (p = result; *p != '\0'; p++) {

if (isalpha(*p))

{

if (islower(*p)) *p = (((*p - 'a') + decalage + ALPHABSZ) % ALPHABSZ) + 'a';

else if (isupper(*p)) *p = (((*p - 'A') + decalage + ALPHABSZ) % ALPHABSZ) + 'A';

}

}

return result;

}

  

}
```

### d)
```c
void test_cesar(void) {
printf ("%s\n", cesar (" ABCDEFGHIJKLMNOPQRSTUVWXYZ ", 3));
printf ("%s\n", cesar ("TU QUOQUE MI FILI", 3));
printf ("%s\n", cesar ("VENI VIDI VICI", 3));
printf ("%s\n", cesar ("XIBX GXZQX BPQ", 3));
printf ("%s\n", cesar ("PF SFP MXZBJ MXOX YBIIRJ ", 3));

printf ("%s\n", cesar (" DEFGHIJKLMNOPQRSTUVWXYZABC ", -3));
printf ("%s\n", cesar ("VDWRU \nDUHSR \nWHQHW \nRSHUD \nURWDV ", -3));
printf ("%s\n", cesar ("GHPR GHV PDXA GHV PRWV", -3));
printf ("%s\n", cesar ("YDH YLFWLV ", -3 ));
}
```
### e)
	DEFGHIJKLMNOPQRSTUVWXYZABC    
	WX TXRTXH PL ILOL  
	YHQL YLGL YLFL  
	ALEA JACTA EST  
	SI VIS PACEM PARA BELLUM    
	ABCDEFGHIJKLMNOPQRSTUVWXYZ    
	SATOR    
	AREPO    
	TENET    
	OPERA    
	ROTAS    
	DEMO DES MAUX DES MOTS  
	VAE VICTIS    
	DEFGHIJKLMNOPQRSTUVWXYZABC    
	WX TXRTXH PL ILOL  
	YHQL YLGL YLFL  
	ALEA JACTA EST  
	SI VIS PACEM PARA BELLUM    
	ABCDEFGHIJKLMNOPQRSTUVWXYZ    
	SATOR    
	AREPO    
	TENET    
	OPERA    
	ROTAS    
	DEMO DES MAUX DES MOTS  
	VAE VICTIS

## Question 12:
```c
char * rot13(const char * chaine) {
	return cesar(chaine, 13);
}
```

Reponse:

	C'est son fils.

```c
printf("%s | %s\n", reponse, rot13(rot13(reponse)));
```

## Question 13:
```c
int main(int argc, char const *argv[])

{

	int decalage = 3;
	char ligne[MAX_LEN + 1] = "";
	
	switch (argc)
	{
		case 3:
			printf("%s\n", cesar(argv[2], atoi(argv[1])));
			return 0;

		case 2:		
			// See if is an integer
			int test = atoi(argv[1]);
			if (test == 0) { // if atoi fail -> return 0, alors c'est le texte.
				printf("%s\n", cesar(argv[1], 3));
				return 0;
			} else {
				decalage = atoi(argv[1]);
			}
			break;
		
		case 1:
			break;
		
		default:
			// Cas erreur.
			printf("Mauvais usage\n");
			return 1;
	
	}
	
	while (fgets(ligne, sizeof(ligne) - 1, stdin) != NULL)
	{
		printf("%s", cesar(ligne, decalage));	
	}

	return 0;

}
```

```sh
./exo3.exe 12 "AAbb AA"

./exo3.exe 12 "AA b" "Un mauvais usage"

./exo3.exe "Change"

./exo3.exe 18

./exo3.exe
```

```sh
for i in {1..25}
do
echo "$i: "
	./exo3.exe $i "SV PKED ZBOXNBO K MOCKB DYED MO AES XO VES KZZKBDSOXD ZKC. - Zkev OVEKBN OD Kxnbo LBODYX -"
done
```
## Question 14:
```sh
whereis stdio.h
# stdio.h: /usr/include/stdio.h
```
## Question 15:
```sh
gcc test1.c -E > test1.i
```
Tout les commentaires on été supprimes. 
Les lignes de include ont été remplace par les codes sources des librairies.
`int titi = MAx` a pris la valeur de max : `int titi = 15`.

## Question 16:
```sh
gcc test1.c -S > test1.s
```
.data définit les variables globales.
.rodata read_only data.
.texte instructions du programme.

.size c'est la taille en octet d'une variable.
.align permet d'indiquer que la variable sera sauvegardée dans un espace mémoire de 4octects. 

```asm
tete:
	.long	0
	.long	1072955392
```
Dans la calculatrice 1.25 nous donne la représentation:  3FF4000000000000
C'est little indian.

Le point d’entrée c'est main. 

## Question 17:
```sh
gcc test1.c -c
# Produit test1.o
```
```sh
nm test1.0
```
```
0000000000000000 T main
                 U Msg
                 U printf
0000000000000000 D tata
0000000000000008 R tete
0000000000000000 R tutu
```
 On voit que:
 main  est dans le text code section
 Msg est undefined
 printf est undefined
 tata est donne initialize
 tete et tutu sont read only.

Si on fait
```sh
gcc test1.c -o test1.exe
```
On obtient: 
```
/usr/bin/ld: /tmp/ccuiyouM.o: warning: relocation against `Msg' in read-only section `.text'
/usr/bin/ld: /tmp/ccuiyouM.o: in function `main':
test1.c:(.text+0x40): undefined reference to `Msg'
/usr/bin/ld: warning: creating DT_TEXTREL in a PIE
collect2: error: ld returned 1 exit status
```
 
Il trouve bien le printf dans les librairies, pourtant il n'est plus undefined. Mais pour **Msg** il trouve pas, est c'est la cause de l'erreur.

## Question 18:
On retire tout les références du symbole **Msg**. Si on effectue:
```sh
gcc test1.c -o test1.exe
```
On réussi bien a compiler notre fichier. Sauf que quand on exécute le fichier on retrouve:
```
[1]    5150 segmentation fault (core dumped)  ./test1.exe
```
2.
A l'aide de **-g**:
3. Grace a file on peut retrouver que le fichier est du type ELF x86-64.
4.  la commande:
```sh
objdump -T ./test1.exe
```
Donne le detaille des liens symboliques du fichier.
>Print the dynamic symbol table entries of the file.  This is only meaningful for dynamic objects, such   as certain types of shared libraries.

5. On utilise:
```sh
objdump -T /lib/libc.so.6
```
## Question 19:
## Question 20:
a)
L'erreur est cause car la fonction **srqt** n'est pas défini, et elle est utilise dans les fichiers: *std.c testBasique.c*.
b)
Si on voit le mannuelle de sqrt, ça nous dit que on peut faire le lien avec:
> Link with -lm.

c)
On effectue alors:
```sh
gcc *.c -lm -o testStat
```
On obtient bien un fichier testStat, que si on exécute on obtient:
```
Min = 0.001125479582697
Max = 0.999993570614606
Avg = 0.508125469784718
Std = 0.283832849108248
```
d)
Si on donne comme paramètre: **1000000**, on obtient:
```
Min = 0.000000563450158
Max = 0.999998311046511
Avg = 0.500006609820427
Std = 0.288619577803438
```
## Question 21
```
/usr/lib/libm.so  
/usr/lib/libm.a
```
Il existe deux fichier, un pour la lib dynamique (.so) et l'autre statique (.a)

## Question 22
On peut voir sur le code qu'il y a des 
```c
#ifdef _TEST_BASIQUE
```
Alors on peut faire appel, en définissant différent paramètres pour afficher les résultats que on veut.
- gcc *.c -lm -D_TEST_BASIQUE -o testStat
- gcc *.c -lm -D_TEST_BASIQUE -DNBMAX=25 -o testStat
- gcc *.c -lm -D_TEST_BASIQUE -DNBMAX=25 -D_DEBUG -o testStat

## Question 23:
Le défaut majeur est que chaque fois il fait une compilation complète du programme pour afficher les différents résultat.

## Question 24
1.
Quand on utilise make testStat le makefile va compiler le programme pour avoir le fichier testStat.
```
gcc  -Wall -Werror -std=c99 -pedantic -c testStat.c -o testStat.o
gcc  -Wall -Werror -std=c99 -pedantic -c min.c -o min.o
gcc  -Wall -Werror -std=c99 -pedantic -c max.c -o max.o
gcc  -Wall -Werror -std=c99 -pedantic -c avg.c -o avg.o
gcc  -Wall -Werror -std=c99 -pedantic -c std.c -o std.o
gcc  -Wall -Werror -std=c99 -pedantic -c testBasique.c -o testBasique.o
gcc testStat.o min.o max.o avg.o std.o testBasique.o -o testStat -lm
```

2.
Si on fait de nouveau la commande, on retrouve un autre résultat:
```
make: 'testStat' is up to date.
```
Le make reconnait qu'il y a pas besoin de re compiler le programme car il existe déjà.

3.
La règle touch all va faire un touch a tous les fichiers **.c**.
Si on exécute:
```sh
make touchAll
make testStat
```
On retrouve:
```
gcc  -Wall -Werror -std=c99 -pedantic -c testStat.c -o testStat.o
gcc  -Wall -Werror -std=c99 -pedantic -c min.c -o min.o
gcc  -Wall -Werror -std=c99 -pedantic -c max.c -o max.o
gcc  -Wall -Werror -std=c99 -pedantic -c avg.c -o avg.o
gcc  -Wall -Werror -std=c99 -pedantic -c std.c -o std.o
gcc  -Wall -Werror -std=c99 -pedantic -c testBasique.c -o testBasique.o
gcc testStat.o min.o max.o avg.o std.o testBasique.o -o testStat -lm
```
C'est a dire que comme il a change le timestamp de tout les fichiers .c, le compilateur pense qu'ils ont change et pour tant, le fichier exécutable avant, ne correspond plus a la dernière version possible.

4.
Permet d'afficher les dépendances des fichiers **.c**
```
gcc  -MM min.c max.c avg.c std.c testStat.c testBasique.c
min.o: min.c
max.o: max.c
avg.o: avg.c
std.o: std.c avg.h
testStat.o: testStat.c stat.h min.h max.h avg.h std.h
testBasique.o: testBasique.c stat.h min.h max.h avg.h std.h
```

5.
La règle **realclean**, va supprimer tous les fichier de librairies, ou exécutables dans le répertoire.

## Question 25
1.
Si on exécute: 
```sh
make testStat TEST_BASIQUE=on NBMAX=125
```
On peut voir par ce qui affiche la commande:
```
gcc -D_TEST_BASIQUE -DNBMAX=125 -Wall -Werror -std=c99 -pedantic -c testStat.c -o testStat.o
gcc -D_TEST_BASIQUE -DNBMAX=125 -Wall -Werror -std=c99 -pedantic -c min.c -o min.o
gcc -D_TEST_BASIQUE -DNBMAX=125 -Wall -Werror -std=c99 -pedantic -c max.c -o max.o
gcc -D_TEST_BASIQUE -DNBMAX=125 -Wall -Werror -std=c99 -pedantic -c avg.c -o avg.o
gcc -D_TEST_BASIQUE -DNBMAX=125 -Wall -Werror -std=c99 -pedantic -c std.c -o std.o
gcc -D_TEST_BASIQUE -DNBMAX=125 -Wall -Werror -std=c99 -pedantic -c testBasique.c -o testBasique.o
gcc testStat.o min.o max.o avg.o std.o testBasique.o -o testStat -lm
```
Qu'il a été bien en prise en compte la variable car il existe **-D_TEST_BASIQUE -DNBMAX=125**

2. On peut utiliser soit @ soit -s

## Question 26:
1. Si on fait:
```sh
ls -l *._ic
```
On obtient:
```
-rwxr-xr-x 1 pablo pablo 866168 17 mai   18:31 test2Stat_ic
-rwxr-xr-x 1 pablo pablo 866168 17 mai   18:31 testStat_ic
```
On peut voir que les deux ont la même taille. C'est normal car les deux ont les librairies dans leurs codes.

2. Si on fait:
```sh
ls -la | grep "Stat$"
```
On obtient:
```
-rwxr-xr-x 1 pablo pablo  16752 17 mai   18:31 test2Stat
-rwxr-xr-x 1 pablo pablo  16840 17 mai   18:23 testStat
```
On peut voir que les deux sont considérablement plus petits que les autres. Car il comporte seulement des liaisons vers les librairies, et pour tant pas le code dans le fichier.

Egalement on peut voir que *test2Stat* est un peu plus petit que l'autre

## Question 27:
1.
```sh
file testStat
```
```
testStat: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=70d4d20cd7a44896e88df3038c074250be4d59c4, for GNU/Linux 4.4.0, not stripped
```

2.
```sh
file testStat_ic
```
```
testStat_ic: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, BuildID[sha1]=043f8a5b65c05d6972cc48c4dc9c9f28042a4326, for GNU/Linux 4.4.0, not stripped
```

On peut voir que les deux sont de fichiers exécutable (ELF 64-bits). Mais le premier dit bien qu'il est **dynamically linked**.

## Question 28:
`nm` permet de lister les symboles d'un fichier.

1.
```sh
nm testStat | grep ' T '
```

```
00000000000014b2 T avg
0000000000001bdc T _fini
0000000000001000 T _init
00000000000011c9 T main
000000000000142b T max
00000000000013a4 T min
0000000000001318 T newRandomTable
00000000000010d0 T _start
000000000000151f T std
00000000000015e6 T testBasique
```

>"T" The symbol is in the text (code) section.

2.
```sh
nm testStat | grep ' t '
```

```
0000000000001100 t deregister_tm_clones
0000000000001170 t __do_global_dtors_aux
00000000000011c0 t frame_dummy
0000000000001130 t register_tm_clones
0000000000001b15 t Std
0000000000001621 t testBasique1
0000000000001868 t testBasique2
```
Les fonctions statiques

3.
```sh
nm testStat | grep ' U '
```

```
                 U atoi@GLIBC_2.2.5
                 U exit@GLIBC_2.2.5
                 U free@GLIBC_2.2.5
                 U __libc_start_main@GLIBC_2.34
                 U malloc@GLIBC_2.2.5
                 U perror@GLIBC_2.2.5
                 U printf@GLIBC_2.2.5
                 U puts@GLIBC_2.2.5
                 U rand@GLIBC_2.2.5
                 U sqrt@GLIBC_2.2.5
                 U __stack_chk_fail@GLIBC_2.4
```

C'est les symboles non définis. On peut voir qu'ils appartenaient aux librairies de linux.

4.

>If lowercase, the symbol is usually local; if uppercase, the symbol is global (external)
>"T" "t" The symbol is in the text (code) section.
>"U" The symbol is undefined.
## Question 29:

1. Dans mon cas ils se trouvent dans: `/usr/lib/`
2. Windows utilise les librairies comme `DLL`
3.  On peut utiliser également:
```sh
find /usr/lib/ -name libc.a
``` 
Elle se trouve:
```
/usr/lib/libc.a
```
