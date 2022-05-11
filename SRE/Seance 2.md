# Langage C
---
Pour tout langage:
- Structure Donee elementaires (DATA)
- SC elementaires (Alog)
- Syntaxe (grammaire)
	- Le compilateur aide a corriger la syntaxe

Étapes de compilation
![[Compilation]]
---
## Structure données Simple
- Entier

| int          | 4   | -2^15 .. 2^15-1 |
| ------------ | --- | --------------- |
| unsigned int | 4   | 0 .. 2^16-1     |
| byte         | 1   | 0 ... 255       |
| Char         | 1   | ASCII           |
| short        | 2   |                 |
| long         | 8   |                 |

- Réel: 
	- float
	- double

### Constructeur Simple:
- tableau `[dimension]`
> [!attention]
> Tableau indice de 0 a dimension - 1
> 

Example:
```c
int i;
int n = 100;
char c = 'a';
int tabEntier[100];
```
```ad-info
**;** Séparateur d'instructions.

```

Autres constructeur:
- n-uplet
- struct (enregistrement, record, tuple)

```c
struct point {
	float x;
	float y;
};

struct point tabPts[100];
struct point pt, pt2;

pt.x = ...;
pt.y = ...;
pt2 = pt;
```

Langage C est sensible a la casse (UNIX aussi).

### Conventions:
- Constante: MAJUSCULES
- vars / structure / fonctions : minuscules

Si le nom est composé:
- CST : _
- autres: Initiales du mot en maj (**camelCase**)

```c
#define TAILLE_TABLEAU 100

int tabEntiers[TAILLE];
```
---
## SC: Structures de CTRL
### Simples:
- Séquence: **;**
- Conditionnelle
	```c
	if (expr_condition) instruction_vrai ;
	if (expr_condition) instruction_vrai ; else instruction_false
	```
- Itération
	```c
	while (expr_condition) instr_while ;	
	```

```ad-info
Si au lieu d'une instruction, on a plusieurs instructions, alors on utilise **{ }** pour les délimiters.
``` 
```c
if (tabEntiers[i] == 0) {
	tabEntiers[i] = tabEntiers[i] + 1;
	i++
}
```
### SC dérivées
- for
	```c
	for (pre_inst; cdt; pos_inst) {
		inst_for
	}

	```

- do while
	```c
	// 1 a n fois
	do inst_while; while (cdt) ;
	```

- switch (sélectionner le bon cas)
	```c
	switch (var_selec) {
		case val1 : .... ;
		case val2 : .... ; break;
		...
		default : .... ;
	}
	// on peut finir avec des break
	```
---
## Fonction / procédure
type_resultat nom_fct ( list_params avec_type);
```c
// Prototype de fonction (specification)
int carree (int i);

// algorithme de fonction (implementation)
int carree (int i) {
	return i * i
}
```
Fonction principale **main**.

Les spécification on les définit dans un fichier **.h** et l’implémentation dans le fichier **.c** (qui après compilation devient **.o**)

### Librairies
- un fichier **.h** qui donne les spécifications
- un fichier **.a / .so** (un ensemble de fichier **.o**) qui donne l’implémentation