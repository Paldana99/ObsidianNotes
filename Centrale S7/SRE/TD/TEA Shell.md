# UNIX SHELL
**Pablo ALDANA**
## Q1:
a)
```sh
man link
```
b)
```sh
man link | more
```
c)
```sh
man link | grep "file"
```
## Q2:
a)
```sh
man passwd
```
b) 
```sh
whereis passwd

return:
/usr/bin/passwd /etc/passwd /usr/share/man/man1/passwd.1.gz /usr/share/man/man1/passwd.1ssl.gz /usr/share/man/man5/passwd.5.gz
```
c) Il cherche par defaut de Linux, dans le `$PATH` et dans `$MANPATH`

## Q4:
a) Elle affiche le manuel de la commande intégré alias.
b) Avec `whereis alias` on retrouve le fichier de définition: 

	usr/share/man/man1p/cd.1p.gz
Alors on peut retrouver tous les commandes intégré avec:
```sh
ls /usr/share/man/man1p/
```
## Q5:
a) La clé est détecte automatiquement par le système (dans mon cas Manjaro-Arch). 
b)Avec la commande :
```sh
df
# /dev/sdb1       15548384  1192480  14355904   8% /run/media/pablo/A6DF-90A9
```
On peut voir que la clé USB est monte dans */run/media/pablo/A6DF-90A9*.
c) Pour voir le contenu il faut simplement:
```sh
ls -la /run/media/pablo/A6DF-90A9
```
d) Pour démonter a l'aider du CLI on peut utiliser:
```sh
umoun /dev/sdb1
```
On vérifie si on fait de nouveau la commande de c) ou b).
## Q6:
a) On peut utiliser:
```sh
ls --color
```
b) Par Default il est mis comme: `ls --color='always'

## Q7:
a) 
```sh
echo ./*p
```
b)
```sh
echo ./?????
```
c)
```sh
echo ./????p
```
## Q8:
a)
```
ln origin.txt destination.txt
ls -l
```
On peut voir que le compteur de lien augmente.
b)
```sh
ls -li
```
On observe qu'ils ont le même inode.
c) Si on supprime le fichier d'origine:
```sh
rm origin.txt
```
Le fichier de destination n'est pas supprime, mais on le numéro de lien est réduit en 1.

## Q9:
a) 
```sh
ln -s origin.txt destination_symbolic.txt
ls -li
```
b) Si on supprime le fichier d'origine, le lien symbolique perd son contenu.
c) Pour supprimer le lien symbolique
```sh
unlink destination_symbolic.txt
```
## Q10:
a)
```sh
rm -i file
```
- créer un alias
```sh
alias rmconfirm='rm -i'
```
- Il faudrait modifier le fichier **~/.bashrc**
- Il faut juste faire appel a l'original

b)
```sh
rm file
```
c) 
```sh
rm -r directory
```
d)
```sh
unalias name
```
## Q11:
a) non, car on premier on voit si on est l'utilisateur qui lui appartient, si c'est le cas l'algorithme va voire si il a accès ou pas.
b)
```sh
chmod 000 test
```
On peut bien modifier les les droits.  Même si on a pas les droits dans le directoire.
c) Oui on peut.

## Q12:
a) Il faut être root
```sh
su
useradd u1
useradd u2
groupadd g1
```
b)
```sh
usermod -a -G g1 u1
```
c)
```sh
usermod -a -G g1 u2
```

## Q13:
a)
```sh
mkdir dir
chmod 007 dir
```
b)
```sh
mkdir dir
chmod 070 dir
```
c) On fait un dir qui a des permissions seulement pour le user qui est le propriétaire, mais pour le groupe et others on met pas de permission.
```sh
mkdir dir
chmod 700 dir
```
## Q14:
Pour chaque fichier qu'il va créer mettre en place les permission de façon que le groupe web va avoir accès, et dans ce groupe on va rajouter a *www-data* par exemple. De cette façon, les autres utilisateurs de la machine pourront pas accéder, car ils font pas partie du groupe, et dans others il y a pas accès.

## Q15:
## Q16:
a) 
```sh
echo $TERM
```
b)
```sh
echo $USER
```
c)
```sh
echo $HOME
```
## Q17
Oui, on peut  faire:
```sh
export HELLO='hello'
# On change a root
su
echo $HELLO
# hello
```

## Q18:
a) *PATH* permet de rechercher ou il faut lancer les applications.
```sh
PATH="/"
ls # Ne marche plus
```
b) Avec apostrophe
```sh
echo 'la variable $PAHT vaut' $PATH
la variable $PAHT vaut /home/pablo/.nvm/versions/node/v16.6.2/bin:/home/pablo/.rbenv/shims:/home/pablo/.local/bin:/usr/local/bin:/usr/bin:/var/lib/snapd/snap/bin:/usr/local/sbin:/usr/lib/jvm/default/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl
```
Avec guillemets:
```sh
echo "la variable $PAHT vaut" $PATH
la variable  vaut /home/pablo/.nvm/versions/node/v16.6.2/bin:/home/pablo/.rbenv/shims:/home/pablo/.local/bin:/usr/local/bin:/usr/bin:/var/lib/snapd/snap/bin:/usr/local/sbin:/usr/lib/jvm/default/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl
```
## Q19:
Le prompt est charge dans la variable *$PS1*.
Si on change par:
```sh
PS1='[\u \A 1983 ~]\$'
```
## Q20:
Pour faire les changements pennées il faut changer les fichiers qui sauvegardent les définitions des variables.

## Q21: 
La commande touch permet de créer le fichier si il n'existe pas. 
Si il existe, il met a jour la datte de la dernière mise a jour a maintenant.
## Q22:
```sh
mkdir exos
tar xf exercices_module1.tar.gz --directory=exos
```
## Q23:
```sh
tar czf target.tar.gz exos/
```
## Q24:
```sh
pstree -p
```
## Q25:
`CTRL Z` Il met en pause le job. On peut le reprendre avec:
```sh
fg %(id)
```

## Q26:
```sh
sudo kill -9 `jobs -p -s`
```
## Q27:
a) 
ps -o pid,cmd,ruid,euid -u 1001
Permet de lister tous les processus avec les colonnes que on définit après le **-o**. Mais qui sont avec le id user après **-u**, ou chaque processus a comme user effective a celui ci. 
b) 
ps -o pid,cmd,ruid,euid -U 1001
Pareil que l'autre sauf que maintenant le ID de user après **-U**, permet de filtrer les processeur qui ont été crée par se utilisateur. 
c) 
## Q28:
a) echo - display a line of text
b) 
```sh
echo -n text
```
c)
```sh
echo -e text
```
d)
```sh
echo -n 'Hello ' > test.txt && echo World >> test.txt
```
## Q29:
```sh
echo -n 'Nb de comptes: ' > test.txt && wc --lines /etc/passwd >> test.txt
```
## Q30:
```sh
head -n 30 /etc/passwd | tail -n 11
```
## Q31:
```sh
tail -n +2 departements.txt | sort -k 2 -t ':'
```
## Q32:
- Pour les légumes:
Avec **uniq** et **cut**
```sh
cut -d':' -f1 legumesfruits.txt | uniq -c
```
 Avec **comm**:
```sh
 
``` 
- Pour les fruits: (Il faut supprimer les lignes vides)
Avec **uniq** et **cut** 
```sh
cut -d':' -f2 legumesfruits.txt | awk '$0 !~ /^[[:space:]]*$/' | uniq -c
```
Avec **comm**:
```sh

```
## Q33:
a)
```sh
tail -n +2 pays.txt| cut -d':' -f1,2 | sort -k 2 -t ':' > pc
```
b)
```sh
tail -n +2 pays.txt| cut -d':' -f2,3 | sort -k 1 -t ':' > cm
```
c)
```sh
paste -d '#' pc cm
```
d)

## Q34:
a)
```sh
echo $RANDOM > file
```
b)
```sh
cp pays.txt mid.txt

# On retrouve en premier la quantite de ligne pour connaitre la moitie
wc file
head --lines 20 mid.txt >> mid_random.txt ; echo $RANDOM >> mid_random.txt ; tail -n +21 mid.txt >> mid_random.txt
```
c)
```sh
diff mid.txt mid_random.txt
```
d)
```sh
diff mid.txt mid_random.txt > rustine
```
e)
```sh
patch mid.txt -o patched < rustine
```
f)
```sh
comm -23 mid_random.txt patched
```
## Q35
a)
```sh
tr '[a-z]' '[d-za-c]'
```
b)
```sh
tr '[:upper:]' '[:lower:]'
tr '[:lower:]' '[:upper:]' 
```
c)
```sh
tr -s "[:blank:]"
```
## Q36:
```sh
find / -perm $UID
```
Pour rentrer dans certains fichiers, il faudrait mettre **sudo**.
## Q37:
a)
```sh
find . -name '*.gif' -size +100k -exec cp {} ~/Pictures \; find . -name '*.png' -size +100k -exec cp {} ~/Pictures \; find . -name '*.jpeg' -size +100k -exec cp {} ~/Pictures \
```
c) On peut faire un tar.gz pour réduire tous les fichiers
```sh
find . -name '*.gif' -size +100k -exec cp {} ~/Pictures \; find . -name '*.png' -size +100k -exec cp {} ~/Pictures \; find . -name '*.jpeg' -size +100k -exec cp {} ~/Pictures \
tar czf target.tar.gz ~/Pictures/*
```
e)
f)

## Q38:
Il faudrait ajouter dans le fichier .bashrc pou que ça change.
```sh
cat saints.txt | tr -d ' ' | grep 'date +"%d"/"%m"' | cut -d: -f1 | tr -d '\n'
```
## Q39:
a) on indique que la ligne doit avoir rien grâce aux regex: **^$**
```sh
grep -c ^$ file.txt 
```
b) On fait un regex qui voit que chaque ligne après son numéro, il y a rien
```sh
nl -ba file.txt | grep -P '[0-9]+\t$'
```
c)
```sh
grep '[[:blank:]]' file.txt > out.txt
```
## Q40:
Avec REGEX, on peut indiquer qu'il doit pas contenir plus de characters différent a " ". 
```sh
grep -E '^[^ ]{1,2}$'
```
## Q41:
```sh
ls -l | grep '^d' | tr -s "[:blank:]" | cut -d' ' -f9
```
## Q42:
a)
- Premier méthode
```sh
# On retrouve combien de lignes il y a:
wc -l /etc/passwd
# Puis on fait un sort, et on voit la premier ligne depuis 1XX
sort --field-separator=: --key=3n /etc/passwd | grep -n 'x:1[0-9][0-9]'
# Comme ca on peut connaitre combien il y en a
```
- Deuxième méthode
```sh
grep -E ':x:[0-9]{3,}' /etc/passwd | wc -l
```
b)
On peut utiliser les *backreference* pour que le REGEX oblige de trouver le même UID et GID
```sh
grep -E ':([0-9]+):\1:' /etc/passwd
```
## Q43:
a)
```sh
grep -E '([A-z]+):\1:' pays.txt
```
b)
```sh
grep -c -E ':*dollar*' pays.txt
```
c)
```sh
grep -E '.*([A-z]{3}).*:.*\1.*:' pays.txt
```
d) En premier en retrouve combien de départements il y a en total, et ensuite en fait un **sort** pour voir combien il y en a après le nord
```sh
wc -l departements.txt
sort -k 2 -t ':' departements.txt | grep -n 'Nord:' | cut -d ':' -f1
```
On obtiens 43