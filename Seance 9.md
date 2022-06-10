# InterNet Protocol: IP

## ARP:
Address Résolution Protocol, permet de trouver par une IP l'@ MAC.
	- Resaux Local: Bloque par les routeurs.


## ICMP: 
Internet Control Message Protocol: Systeme erreurs / messages.

## Addressage 
(logique) / Routerus -> **Format IP**.

Fragmentation -> etre capable de reconstituer

Envoie de plusieurs paquet mais ils vont arriver en desordre.

une @IP est codée sur 32 bits (4 octets). Notation humaine: 4 valeurs (0 - 255) séparées par un **.** :
> X1.X2.X3.X4

![[Drawing 2022-06-10 14.08.25.excalidraw]]


#### IPv4:
- 1975 : IP (original) est dit **ClassFull** (RFC)
- 1985: Subnetting (RFC)
- 1992: CIDR = Classless Inter Domain Rating (RFC)

#### IPv6

### **Notion de classe**: Découper l'espace d'@ en classe de taille var.
- 3 classes A,B,C pour l'@ des RL (gérer communication unicast et broadcast)
- 1 classe D pour l'@ du multicast IP (par default, ne passe pas le routeur)
- 1 classe E pour l'inter-rezo 

### Masque:
@IP doit informer sur l'@ du RL et l'@ machine dans le RL.

**Operation**:
- @IP **ET Logique** masque = @IP du RL.
- @IP - @IP du LR = @machine

exemple: 

192.168.0.10 -> @RL: **192.168.0** et @machine **.10**

ET logique: 192.168.0.0 -> adresse RL -> Toutes machine du RL est préfixée par 192.168.0

| Classe | 4 premier byte de l@ | Valeurs possible du premier oct | Masque predefini | @RL (octect) | @mach | Capacité @rezo         | Capacité @machine | Plages d'@                                                |
| ------ | -------------------- | ------------------------------- | ---------------- | ------------ | ----- | ---------------------- | ----------------- | --------------------------------------------------------- |
| A      | 0xxx                 | 0 - 127                         | 255.0.0.0        | 1            | 3     | $128$                  | $256^3$     16M   | 0.x.x.x  ->  126.x.x.x                                    |
| B      | 10xx                 | 128 - 191                       | 255.255.0.0      | 2            | 2     | $64 \times 256$  16384 | $256^2$   65736   | 128.0.x.x ... 128.255.x.x ... 129.255.x.x ... 191.255.x.x |
| C      | 110                  | 192 - 223                       | 255.255.255.0    | 3            | 1     | $32 \times 256^2$ 2M   | 256               | 192.0.0.x  223.255.255.255                                |
| D      | 1110                 | 224 - 239                       | NONE             |              |       |                        |                   |   224.0.0.0 a 239.255.255.255 chaque @ est 1 rezo multicast                                                        |
| E      | 1111                 | 240 - 255                       | NONE             |              |       |                        |                   |      240.0.0.0 a 255.255.255.255.255 @ de l'Inter Rezo                                                     |

1 machine peut etre adresse au **unicast**, on utiliser sur @IP l'@IP fourn l'@ RL.
@RL prefixe RL 0.....0 et utiliser prefixe RL 1......1 pour une comm broadcast.

example:
RL : 
192.168.0.0 -> @RL
192.168.0.255 -> @broadcast

et: 192.168.0.1 ... 192.168.0.254 -> @unicast par machine. 

#### Subnetting:
Decouper 1 plage d'@ en +sieurs. Sous plages -> Infra en SS-RL.
- Agrandir l'@ rezo local et diminuer l'@ machine
- Besoin de routeur
- $-$ tous les SS-rezos ont la même taille.

**Example:** Univ Lille -> 134.206.0.0

1 RL de $256^2$ machines.
Subnetting: 256 SS-RL de 256 machines:
134.206.0.X
134.206.1.X
...
134.206.255.X

### CIDR:
1992:
192.0.0.x -> 193.255.255.0 elles etait deja assigne et on peut pas les repprendre immediatement.

Utiliser les regions (continents) pour la repartition des classes C.

> Europe : 194.0.0.x ... 195.255.255.0
> USA :     196.0.0.x ... 197.0.0.X

### @prive
A communique avec 1 machine a l'exterieur verra son @privee translatee avec l'@ public du R: NAT - Network Address Translation

A : 10.x.x.x/8
B : 172.16.x.x/16 ... 172.31.x.x/16
C: 192.168.0.x/24 ... 192.168.255.x/24