# Labo2-Groupe32

## 2 Calculs de sécurité théorique


### Question 2.1
Exactement 1 caractère numérique ?

Les caractères numériques allant de 0 à 9, ceux-ci apportent 10 possibilités. De ce fait il y aura 10^1 possibilités.

### Question 2.2
Exactement 2 caractères numériques ?

En reprenant la question 2.1, nous pouvons dire qu'il y aura 10^2 possibilités.

### Question 2.3
Exactement 6 caractères numériques ?

En reprenant la question 2.1, nous pouvons dire qu'il y aura 10^6 possibilités.

### Question 2.4
Entre 0 et 6 caractères numériques ?

$$
\sum_{i = 0}^{6} 10^i 
$$

### Question 2.5
Exactement 1 caractère alphanumérique (non sensible à la casse) ?

36 caractères alphanumériques, ce qui fait donc 36 possibilités

### Question 2.6
Exactement 8 caractères alphanumériques (non sensible à la casse) ?

$26^8 $

### Question 2.7
Entre 0 et 8 caractères alphanumériques (non sensible à la casse) ?

$$
\sum_{i = 0}^{8} 26^i \approx 2^{38}
$$

### Question 2.8
Exactement 1 caractère alphanumérique (sensible à la casse) ?

$$
26 \times 2 + 10 = 62
$$

### Question 2.9
Exactement 8 caractères alphanumériques (sensible à la casse) ?

$$
62^8
$$

### Question 2.10
Entre 0 et 8 caractères alphanumériques (sensible à la casse) ?

$$
\sum_{i = 0}^{8} 62^i 
$$

### Question 2.11
Exactement 1 caractère ASCII (7 bits) ?

$$
2^7
$$

### Question 2.12
Exactement 8 caractères ASCII ?

$$
2^{7*8} = 2^{56}
$$

### Question 2.13
Entre 0 et 8 caractères ASCII ?

$$
\sum_{i = 0}^{8} 2^{7i} 
$$

### Question 2.14
Combien de temps faudra-t-il « en moyenne » pour casser un mot de passe de la question 2.6 ?

Il faut donc $1/2$ jours "en moyenne"

### Question 2.15

Toujours avec la même base, combien de temps faudra-t-il « au maximum » pour casser un mot de passe de la question 2.12 ?

Cela correspond à $24^8= 110 075 314 176$ heures, ou $24^7=4'586'471'424$ jours, ou encore $12'557'074$ années

### Question 2.16
Combien de temps faudra-t-il « en moyenne » pour casser un mot de passe de la question 2.12 ?

$\frac{12'557'074}{2} = 6'278'537$ années

### Question 2.17
En considérant des attaques « hors ligne », décrire trois manières de freiner (soit bloquer, soit ralentir) l’attaquant ?

Il est nécessaire de rajouter des salts pour réduire la vitesse de l'attaquant, ou incorposer une clef d'encryption supplémentaire, chargée a l'execution. Cela permets encore de réduire les risques. Choisir le facteur de difficulté (nb d'itérations) tel que l'expérience utilisateur n'est pas impactée, mais il n'est pas instantané côté serveur (target souvent choisie à `500ms`)

### Question 2.18
En considérant des attaques « en ligne », décrire deux manières de freiner (soit bloquer, soit ralentir) l’attaquant ?

Mettre en place un ratelimiting, s'assurer que les opérations cryptographiques sont en "temps-constant", et bloquer après un certain nombre de tentatives sur une IP.

### Question 2.19
Les mots de passe ne sont pas stockés en clair, pourquoi ?

Parce que les stockés en clair permettrait à un attaquant de les récupérer s'il a accès à l'emplacement où ils sont stockés. Ce qui lui permet par la suite d'accéder directement au service sécurisé par le mot de passe (notion de persistance).

### Question 2.20
Les mots de passe ne sont pas stockés en clair, mais pourtant ils ne sont pas chiffrés, pourquoi ?

L'opération de chiffrage est (par définition) bi-directionnelle, ce qui indique qu'il est possible de retrouver le mot de passe en clair si un attaquant parvient a obtenir la clef d'encryption.

### Question 2.21
Sous quelle forme sont stockés les mots de passe ?

Ils sont stockés sous forme hashée, une opération cryptographique à sens unique (il est très complexe d'effectuer l'opération dans le sens inverse).

## 3 Identification des empreintes des mots de passe

### Question 3.1
Quel est le type d’empreintes contenues dans les deux fichiers mentionnés ci-dessus ?
Sur quels arguments basez-vous votre réponse (capture d’écran, explications et
justifications) ?

Pour le fichier KaliHash.txt, le format ressemble grandement au fichier /etc/shadow de Linux.
En regardant la documentation de crypt(5) (https://manpages.debian.org/unstable/libcrypt-dev/crypt.5.en.html), il est possible de trouver le format de chaque hash:
- $1$ indique que les mots de passe sont encryptés à l'aide de `md5crypt`.

Pour le fichier XPHash, comme indiqué dans le cours, les deux hash LM et NTLM sont présents pour chacun des utilisateurs.


## 4 Hashcat

### Manipulation 4.1
Extraire le dictionnaire rockyou.txt de l’archive /usr/share/wordlists/rockyou.txt.gz.

### Question 4.1
Quelle doit être la valeur de l’option -m pour les deux fichiers ?

`-m 1000 / 3000` pour XPHash.txt
`-m 500` pour KALIHash.txt

### Question 4.2
Quels sont les différents modes d’attaque de hashcat ? Expliquer brièvement leur
fonctionnement ainsi que les arguments nécessaires pour utiliser ces modes.

  # | Mode
 ===+======
  0 | Straight
  1 | Combination
  3 | Brute-force
  6 | Hybrid Wordlist + Mask
  7 | Hybrid Mask + Wordlist
  9 | Association



### Question 4.3
Quel est le mode d’attaque par défaut ?

Par défaut, Hashcat utilisera une attaque appropriée en fonction du type de hachage que vous essayez de casser.

`-a 0` (Dictionary)

### Manipulation 4.2
Lancer hashcat avec le mode d’attaque par défaut sur le fichier XPHash.txt, puis sur
le fichier KALIHash.txt. Noter les commandes et le résultat obtenu.

```sh
$ hashcat -m 1000 XPHash.txt   ../wordlists/rockyou.txt
82cf6feab03795ff1e1b7e3b43e9764e:funtime
$ hashcat -m 3000 XPHash.txt   ../wordlists/rockyou.txt
99194a696e6dede0:JULIETT
4738b39ea1ebbf44:FUNTIME
$ hashcat -m 500  KALIHash.txt ../wordlists/rockyou.txt
$1$iQlQrcnz$qmUTfRdy7A.aEWFbxaCks1:funtime
```

### Question 4.4
Qu’est-ce qu’un masque ? Avec quel(s) mode(s) l’utilise-t-on ?

Mask, and Hybrid modes.


### Question 4.5
Quels sont les alphabets (charsets) prédéfinis ?

  ? | Charset
 ===+=========
  l | abcdefghijklmnopqrstuvwxyz [a-z]
  u | ABCDEFGHIJKLMNOPQRSTUVWXYZ [A-Z]
  d | 0123456789                 [0-9]
  h | 0123456789abcdef           [0-9a-f]
  H | 0123456789ABCDEF           [0-9A-F]
  s |  !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
  a | ?l?u?d?s
  b | 0x00 - 0xff


### Question 4.6
Quels sont les alphabets et le masque utilisés par défaut pour le bruteforce ?

Guess.Charset....: -1 ?l?d?u, -2 ?l?d, -3 ?l?d*!$@_, -4 Undefined
Guess.Mask.......: ?1?2?2?2?2 [5]

### Manipulation 4.3
Lancer hashcat en mode bruteforce avec la configuration par défaut. Noter la
commande et le résultat obtenu.

```sh
hashcat -m 500 -a 3 KALIHash.txt --status -O
```

### Question 4.7
Quelle(s) option(s) permet(tent) de tester différentes longueurs pendant le bruteforce ?

Il suffit de changer le masque utilisé.

### Question 4.8
Quelle option permet de définir un nouvel alphabet ?

Il suffit de changer le masque utilisé (avec un argument)

### Manipulation 4.4
Lancer hashcat en mode bruteforce avec la bonne configuration, sachant qu’un des
mots de passe contient des majuscules et des minuscules et a une longueur entre 4 et
7 caractères. Noter la commande et le résultat obtenu.

```sh
hashcat -m 1000 -a 3 ntlm.txt -1 "?l?u" --increment-min=4 --increment-max=7 -i "?1?1?1?1?1?1?1?1" -O

f57300698a5b0b55234837d920eaa3ee:RdQom
04b365a8953171d1e9decf74feb7ecac:nceipo
82cf6feab03795ff1e1b7e3b43e9764e:funtime
```

### Manipulation 4.5
Lancer hashcat en mode bruteforce avec la bonne configuration, sachant qu’un des
mots de passe commence par un signe de ponctuation, puis est suivi de caractères
alphanumériques (longueur max. 6 caractères). Noter la commande et le résultat
obtenu.

```sh
hashcat -m 1000 -a 3 ntlm.txt --potfile-path current-2.potfile -1 "?l?u?d" --increment-min=1 --increment-max=6 -i "?s?1?1?1?1?1?1?1" -O

46599a6541e638a90afba723ad58df81:?xA1W
```

### Manipulation 4.6
Un dernier mot de passe peut être trouvé avec le mode bruteforce. A vous de trouver
le masque et le(s) alphabet(s) adéquats. Noter la commande et le résultat obtenu.

```sh
# Pas trouvé...
```


### Manipulation 4.7
Tester les deux variantes du mode permettant de méler bruteforce et attaque
par dictionnaire. Utiliser des masques courts et des alphabets simples. Noter les
commandes et les résultats obtenus.

```sh
hashcat -m 1000 -a 6 --potfile-path current-2.potfile ntlm.txt ../wordlists/rockyou.txt "?d?d?d?d" -i

78817779602482e0219a0c97d71dde90:juliette173
```

### Question 4.9
A quoi servent les "rules" de hashcat ? Avec quel(s) mode(s) les utilise-t-on ? Comment
fonctionnent-elles ?

Les rules permettent d'effectuer une/plusieurs permutations/modifications sur le dictionaire original.

### Question 4.10
Quelles sont les "rules" déjà à disposition ?

Si nous nous référons au github de hashcat (https://github.com/hashcat/hashcat/blob/master/rules):
- Incisive-leetspeak.rule
- InsidePro-HashManager.rule
- InsidePro-PasswordsPro.rule
- T0XlC-insert_00-99_1950-2050_toprules_0_F.rule
- T0XlC-insert_space_and_special_0_F.rule
- T0XlC-insert_top_100_passwords_1_G.rule
- T0XlC.rule
- T0XlC_3_rule.rule
- T0XlC_insert_HTML_entities_0_Z.rule
- T0XlCv2.rule
- best66.rule
- combinator.rule
- d3ad0ne.rule
- dive.rule
- generated.rule
- generated2.rule
- leetspeak.rule
- oscommerce.rule
- rockyou-30000.rule
- specific.rule
- stacking58.rule
- toggles1.rule
- toggles2.rule
- toggles3.rule
- toggles4.rule
- toggles5.rule
- top10_2023.rule
- unix-ninja-leetspeak.rule

### Question 4.11
Que fait l’ensemble de "rules" définies dans le fichier leetspeak.rule ?

En prenant le fichier ligne par ligne:
```txt
sa4 # change tous les a en 4
sa@ # change tous les a en @
sb6 # change tous les b en 6
sc< # change tous les c en <
sc{ # change tous les c en {
se3 # change tous les e en 3
sg9 # change tous les g en 9
si1 # change tous les i en 1
si! # change tous les i en !
so0 # change tous les o en 0
sq9 # change tous les q en 9
ss5 # change tous les s en 5
ss$ # change tous les s en $
st7 # change tous les t en 7
st+ # change tous les t en +
sx% # change tous les x en %
```


### Manipulation 4.8
Lancer hashcat en utilisant leetspeak.rule. Noter la commande et le résultat obtenu.

```sh
hashcat -m 1000 -a 0 ntlm.txt ../wordlists/rockyou.txt -r leetspeak.rule -O

b295d7dd10b0afe1b6bbce24b74b8663:57r4wb3rry
```

### Question 4.12
Tous les mots de passe ont-ils été trouvés ? Si non, à votre avis, pourquoi ?

Après toutes les tentatives au dessus, il reste un seul mot de passe non trouvé (celui de Bob).
Il est possible qu'il ait utilisé un mot de passe plus complexe / long, et qu'une méthode de brute-force ne suffit pas a le trouver.

### Manipulation 4.9
Reporter les mots de passe trouvés avec hashcat dans le tableau en 6.1. Préciser le
mode d’attaque et les éventuels paramètres supplémentaires sous "méthode".

## 5 « Rainbow tables »

### Manipulation 5.1
Ouvrez le navigateur internet Firefox de votre machine Kali et rendez-vous sur le lien
http://rainbowtables.it64.com/.
Sur cette page web, vous pouvez directement copier les hash des mots de passe se
trouvant dans le fichier XPHash.txt et les tester. Le site va ensuite comparer les
hash que vous aurez entrés avec leur rainbow table de LMHash et vous retourner un
résultat le cas échéant.
Reportez les mots de passe trouvés dans le tableau en 6.1.

### Question 5.1
Sous linux, un sel (salt) est ajouté aux mots de passe avant qu’ils soient hachés. Pour
quelle raison l’utilisation de ce sel rend-elle les attaques au moyen de tables « rainbow
» inefficaces ?

Les rainbow tables précalculent en avance les hashs. Dans le cas de l'ajout d'un sel, les rainbow tables sont totalement inutiles, car aucun mot de passe ne sera trouvé.

# 6 Résultats

### Question 6.1
Mot de passe Outil Méthode
Eve | nceipo | hashcat (NTLM, Bruteforce)
Mallory | juliette173 | hashcat (LN, Wordlist) -> (NTLM, Hybrid attack)
Alice | funtime | hashcat (Unix MD5, Wordlist)
Bob | !XS8D?@ | Rainbow table.
Dave | 57r4wb3rry | hashcat (NTLM, Wordlist + Rule)
Carol | RdQom | hashcat (LN, Bruteforce)
Oscar | ?xA1W | hashcat (NTLM, 4.5)
Trudy | 98230293 | hashcat (LN, Bruteforce) -> (NTLM, Bruteforce number only)

# 7 Avantages et inconvénients des deux outils

### Question 7.1
Remplir le tableau suivant en mettant :
• « + » pour avantage, tout en justifiant la réponse
• « - » pour inconvénient, tout en justifiant la réponse

| x                                      | Hashcat | Rainbow tables | Explications |
|----------------------------------------|---------|----------------|--------------|
| Méthode(s) de craquage                 | +       | -              | Hashcat supporte les salts et beaucoup d'autres méthodes |
| Temps de craquage                      | -       | +              | Les rainbow-tables sont couteuses a produire, mais rendent le temps de craquage extrèmement rapide |
| Temps de préparation avant le craquage | +       | -              | Les rainbow-tables nécessitent beaucoup de temps de préparation |
| Craquage sur tous les OS               | +       | -              | Techniquement, les deux outils peuvent être executés sur tous les OS, mais dû à l'utilisation de sel sur Linux, hashcat gagne |


# 8 CrackStation

### Manipulation 8.1
Utiliser l’utilitaire en ligne https://crackstation.net/ pour récupérer les mots de
passe.

### Question 8.1
Quel est l’algorithme utilisé par le site web (victime) pour hasher et stocker les mots
de passe ?

### Question 8.2
Quelle est la technique utilisée par CrackStation pour retrouver les mots de passe ?

### Question 8.3
Pourquoi certaines empreintes ne sont pas retrouvées ? Comment l’expliquer ?
