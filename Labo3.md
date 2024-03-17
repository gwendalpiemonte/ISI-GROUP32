# Labo3-Groupe32

## 2 Les maliciels

### Question 2.1
> Décrire ce qu’est un maliciel ainsi que ses caractéristiques.

Un maliciel est un logiciel se faisant passer comme un outil légitime dans l'objectif d'executer du code malveillant contenu dans l'exécutable.

Ses caractéristiques principales sont:
- Un hash/taille de fichier/métadonnées qui ne correspond pas au logiciel original
- Une version du logiciel non fonctionnel (une erreur est survenue)
- Une signature numérique falsifiée / enlevée

### Question 2.2
> Quelles sont les différentes catégories et fonctionnalités des maliciels.

Sources : 
- [Source principale (en anglais)](https://www.crowdstrike.com/cybersecurity-101/malware/types-of-malware/)
- [Tradutions francaises (tel que recommandé par l'académie francaise)](https://www.academie-francaise.fr/sites/academie-francaise.fr/files/lexique_informatique_et_cybersecurite_2022.pdf)

| Type         | Fonctionnalité |
|:-------------|:---------------|
| Ransongiciel | Désactive l'accès de la victime à ses données tant qu'une rançon n'est pas payée. |
| Maliciel sans fichier | Effectue des modifications dans les fichiers natifs du système d'exploitation |
| Logiciel espion | Collecte des données d'activité des utilisateurs à leur insu |
| Publiciels | Affiche des publicités indésirables |
| Chevaux de Troie | Se déguise en code attrayant |
| Vers | Se propage à travers un réseau en se répliquant |
| Source de Programme Malveillant (Rootkit) | Donne aux pirates le contrôle à distance du périphérique de la victime |
| Enregistreurs de frappe | Surveille les frappes des utilisateurs |
| Maliciel mobile | Infecte les appareils mobiles |
| Maliciel effaceur | Efface irrémédiablement les données des utilisateurs. |

### Question 2.3
Tenter de trouver des fonctionnalités non données en cours, faire travailler son imagination !

## 3 Description de l’environnement

## 4 Utilitaire wine

## 5 Analyse du Malware « Live Messenger »

### Question 5.1
Illustrer et expliquer les manipulations effectuées.

### Question 5.2
Que peut-on déduire du fait que les empreintes ne correspondent pas ?

### Question 5.3
À votre avis, pourquoi est-il utile de vérifier l’intégrité d’un programme téléchargé ?

### Question 5.4
À quoi sert l’outil « Regshot » ?

### Question 5.5
Pourquoi utiliser un environnement de « test » cloisonné ?
Pourquoi utilise-t-on le « snapshot » dans les logiciels de virtualisation (Virtualbox,
VMware, . . .) ?

### Question 5.6
Illustrer et expliquer les manipulations effectuées.

### Question 5.7
Que constatez-vous dans le rapport généré par Regshot ?

### Question 5.8
Que contiennent les fichiers créés par le maliciel ?
Indice : Pour rappel, le dossier C :\ se trouve à l’emplacement
"/home/<username>/.wine/drive_c"

### Question 5.9
À quoi sert « strace » ?

### Question 5.10
Illustrer et expliquer les manipulations effectuées.

### Question 5.11
Quel type de filtre a été utile et efficace pour réaliser la capture ?

### Question 5.12
Dans l’output de strace, qu’est-il possible de visualiser pour ce cas ? Expliquer en détail.
Indice : Regarder la taille des fichiers

### Question 5.13
Tenter de comprendre comment le maliciel traite le fichier « msnsettings.dat ».

### Question 5.14
Quels types d’informations le fichier comprend-il ?

### Question 5.15
Quelles conclusions en tirez-vous ? Pouvez-vous affirmer ces conclusions ?

### Question 5.16
Comment fonctionne « fakedns » ?

### Question 5.17
Illustrer et expliquer les manipulations effectuées.

### Question 5.18
Quels types d’informations ont été capturées grâce à Wireshark ?

### Question 5.19
Expliquer de manière détaillée le comportement du maliciel.

### Question 5.20
Illustrer et expliquer les manipulations effectuées.

### Question 5.21
Après toutes ces analyses comportementales, pouvez-vous identifier à quel(s) type(s) de maliciels « Windows Live Messenger » appartient ? Pourquoi ?

### Question 5.22
Que pouvez-vous en déduire ?

### Question 5.23
À quelle(s) catégorie(s) de codes malveillants appartient ce code malveillant ? (virus, ver, spyware, etc.)

### Question 5.24
Quelle est l’utilité d’un tel code malveillant ?

### Question 5.25
Comment se propage ce code malveillant ?

### Question 5.26
Comment l’infection par ce code malveillant est-elle réalisée ?

### Question 5.27
Que contiennent les registres « ESI » et « ECX » ?

### Question 5.28
Que contiennent les registres « EDI » et « EBX » ?

### Question 5.29
Après avoir déterminé les valeurs contenues dans les registres, est-il possible d’expliquer l’opération assembleur de la ligne suivante : « CMP CL, BL » ?

### Question 5.30
Fort de ces constatations, à votre avis, que se passe-t-il si le champ « e-mail address : » contient « ISI16 » ?













