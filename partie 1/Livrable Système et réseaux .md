# Livrable Système et réseaux 

## généralités
**les options** d'un commande sont séparées par des ``-``
## HELP and DOC
| Commande      | Utilisation                                  | Exemples                                                                                                                                                                                                                                                                                                                                                                 
| :-----------: | :------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ 
| ``man``       | an interface to the system reference manuals | - ``man man``  affiche le manuel du manuel  <br>- `` man man ls cd...`` permet de naviguer dans des manuels successifs.  on fait ``q`` pour quitter le premier manuel puis ``enter`` pour passer au suivant<br>- ``man ls`` permet de voir le manue lde la commande ``ls`` <br>- - inside the manual <br>- - - ``q`` pour quitter<br>- - - ``/mot`` pour chercher un mot 
| `` ls -help`` | permet de voir l'aide de la commande ``ls``  | - ``man -help`` permet de voir l'aide du manuel                                                                                                                                                                                                                                                                                                                          
| `tldr`        | too long don't read                          | `tldr ls` donne une version résumée du manuel de la commande `ls` 

## navigation
| Commande |                Utilisation                | Exemples                                                                                                                                                                                                                                                                                                   |
| :------: | :---------------------------------------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ``pwd``  |          print working cirectory          |                                                                                                                                                                                                                                                                                                            |
|  ``cd``  |             change directory              | -``cd..`` remonte d'un niveau dans l'arboresence<br>-``cd ~``  ou ``cd`` sans chemin, renvoie au répertoire ``home/user``<br>-``cd ./`` avec cette syntaxe on peut écrire un chemin relatif à partir du répertoire courant <br>-``cd /`` avec cette syntaxe on écrit un chemin absolu à partir de ``root`` |
| ``find`` | search for files in a directory hierarchy |  |


## l'affichage
|                      Commande                      |                    Utilisation                     | Exemples                                                                                                                                                                                                                                                             |
| :------------------------------------------------: | :------------------------------------------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                       ``ls``                       |              list directory contents               | ``ls -l`` permet d'afficher du détail<br>- les alias <br>- - ``ll`` est un alias pour ``ls -l``<br>- - ``la`` est un alias pour ``ls -A`` <br>- -  ``l`` est une alias pour ``ls -CF``<br> - les options <br> - - `ls -t` sort by time <br> - - `ls -r` sort reverse |
|                      `lsblk`                       |                 list block devices                 |                                                                                                                                                                                                                                                                      |
|                      `blkid`                       |        locate/print block device attributes        | Pareil que `lsblk` mais avec les infos utiles qui manquent                                                                                                                                                                                                           |
|                     `printenv`                     |          print all or part of environment          |                                                                                                                                                                                                                                                                      |
|                      ``cat``                       | concatenate files and print on the standard output | permet d'afficher le contenu d'un fichier dans la **sortie standard** <br> i.e. le terminal dans notre situation                                                                                                                                                     |
| ``vi`` ``vim`` ``nano`` ``code`` ``more`` ``less`` |                 éditeurs de texte                  | ``vi note.md`` permet d'ouvrir mon ficheir de notes avec ``vi`` dans la terminal                                                                                                                                                                                     |
|                      ``less``                      |                     la blague                      | ``man less`` renvoie ``opposite of more`` et ``Less  is a program similar to more(1), but it has many more features.`` ce qui est une catastrophe                                                                                                                    |
|                       `echo`                       |               display a line of text               | `echo texte`                                                                                                                                                                                                                                                         |
|                      ``seq``                       |            print a sequence of numbers             | ``seq 1 5`` donne : <br>``1``<br>``2``<br>``3``<br>``4``<br>``5``                                                                                                                                                                                                    |

## les actions
### déplacement/copie
| Commande |        Utilisation         | Exemples                                                                                                                                                                                                                                                                                       |
| :------: | :------------------------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  ``cp``  | copy files and directories | ``cp file1 file2`` copie ``file1`` en tant que ``file2``<br>``cp file1 directory1`` copie ``file1`` dans ``directory1``<br>``cp file1 file2 directory1`` copie ``file1`` et ``file2``   dans ``directory1``<br>``cp -R directory1 directory2`` copie ``directory1`` en tant que ``directory2`` |
|  ``mv``  |    move (rename) files     | ``mv file1 file2`` renomme ``file1`` en tant que ``file2``<br>``mv file1 directory1``déplace ``file1`` dans ``directory1`` |


### la création / suppression
| Commande  |      Utilisation       | Exemples                                |
| :-------: | :--------------------: | --------------------------------------- |
| ``touch`` | change file timestamps | ``touch file1`` crée ``file1``          |
| ``mkdir`` |    make directories    | ``mkdir $(seq 1 5)`` crée 5 répertories |
|``rm``|remove files or directories|``rm -R directory1`` supprime ``directory1`` <br> ``rm file1``supprime ``file1``|
### les systèmes de fichiers
| Commande | Utilisation | Exemples |
| :------: | :---------: | -------- |
| `mount`  |             |          |
## les métacaractères
| Caractère |                              Utilisation                               | Exemples                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| :-------: | :--------------------------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   ``#``   |             sert à mettre un commentaire sur une commande              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   ``*``   |               est un alias pour une série de caractères                | ``cp *.txt directory1`` copie tous les fichiers ``.txt`` du répertorie courant dans ``directory1``<br>il peut s'imbriquer dans le nom pour attraper les fichiers correspondants à une nommenclature ``cp Entreprise-*-RAP-*.doc`` par exemple pourrait avoir du sens celon la nommenclature des fichiers dans le répertoire.                                                                                                                                                                                              |
|   ``?``   |                      idem mais pour un caractère                       | ``cp d?r?-l*`` copie ``dora-l'exploratrice.exe`` aussi bien que ``d2r3-l.svg``                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|  ``[ ]``  |    est une manière d'écrire un alias pour un ensemble de caractère     | ``cp n[oa]te.md`` copie aussi bien ``note.md`` que ``nate.md``<br>- on peut écrire une class de caractères dans les ``[]``<br>- ``[[:alnum:]]`` qui représente n’importe quel caractère alphanumérique ;<br>- ``[[:alpha:]]`` qui représente n’importe quel caractère de l’alphabet ;<br>- ``[[:lower:]]`` qui représente n’importe quel lettre minuscule de l’alphabet ;<br>- ``[[:upper:]]`` qui représente n’importe quel lettre majuscule de l’alphabet ;<br>- ``[[:digit:]]`` qui représente n’importe quel chiffre. |
|  ``{ }``  | permet de créer différentes chaines de caractères à partir d’un schéma | ``touch 2024-{RAP, MAN, DOC}.md`` pourrait permettre de créer 3 fichiers ``.md`` en une seule commande                                                                                                                                                                                                                                                                                                                                                                                                                    |
|   ``$``   |         permet d'écrire des sous commandes dans nos commandes          | ``mkdir $(seq 1 5)`` crée 5 répertories                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|   `\|`    |         pipe (l'anglais pour tuyau pas le français pour pipe)          | permet de manager la sortie standard<br> - `history \| less` permet de voir l'historique des commandes dans less                                                                                                                                                                                                                                                                                                                                                                                                          |
## les +
| Commande |         Utilisation         | Exemples |
| :------: | :-------------------------: | -------- |
| ``seq``  | print a sequence of numbers | ``seq 1 5`` donne : <br>``1``<br>``2``<br>``3``<br>``4``<br>``5`` |
## VIM

|                      Commande                       |         Utilisation         | Exemples                                                                              |
| :-------------------------------------------------: | :-------------------------: | ------------------------------------------------------------------------------------- |
| [`k` `l` `m` `j`] <br> [`UP` `DOWN` `LEFT` `RIGHT`] |         navigation          | touches directionnelles dans VIM                                                      |
|                      `ESCAPE`                       | pour revenir au mode normal | quitter le mode en cours                                                              |
|                        `:q!`                        |         force quit          | quitter sans sauvegarder                                                              |
|                        `:q`                         |            quit             | quitter <br> si le fichier n'est pas sauvegardé il y aura une demande de confirmation |
|                        `:wq`                        |      sauver & quitter       | attention au droits, on peut avoir des problèmes                                      |
|                         `x`                         |       en mode normal        | supprime le caractère surligné                                                        |
|                         `i`                         |         mode insert         | ouvre le mode insertion avant le caractère surligné                                   |
|                         `a`                         |         mode append         | ouvre le mode insertion après le caractère surligné                                   |
|                   `vim file.txt`                    |       ouvrir // créer       | ouvre le `file.txt`<br> à défaut crée `file.txt`                                      |
|                         `d`                         |       duplicate line        |                                                                                       |
|                         `p`                         |                             |                                                                                       |
|                         `u`                         |                             |                                                                                       |


## Tests de connectivité et chemins
|      Commande      |                      Utilisation                       | Exemples                                                                                                                  |
| :----------------: | :----------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------- |
|       `ip a`       | présente les cartes réseaux et leurs IP sur la machine | ![alt text](image.png)                                                                                                    |
| `whois domaine.xx` |            traduit un IP en nom de domaine             | `whois 88.198.21.14`   <br>    `whois google.fr`                                                                          |
|     `nslookup`     |            traduit un nom de domaine en IP             | `nslookup google.fr`                                                                                                      |
|       `host`       |                   DNS Lookup utility                   |                                                                                                                           |
|    `traceroute`    |     trace la route vers un IP ou un nom de domaine     |                                                                                                                           |
|     `ip route`     |        idem que `ip a` mais avec moins d'infos.        |                                                                                                                           |
|  `ip route show`   |              affiche la table de routage               |                                                                                                                           |
|       `dig`        |        demande au DNS l'adresse IP d'un domaine        | par défaut la requète est envoyée au DNS du FAI <br> `dig domaine.fr @D.N.S.I.P` pour contourner un bloquage par le DNS par défaut en forçant <br> options : `NS`  `A` <br>`1.0.0.1` est un DNS public |
|        `ss`        |                  list of used sockets                  | `ss -t` list les protocoles TCP <br>        `sudo ss -tlp` TCP Listen Processus                                           |
| `nftable` ou `nft` |                                                        | `nft flush ruleset` désactive le firewall |

### la commande dig

1. `dig . NS`: Cette commande interroge les serveurs de noms racine pour obtenir la liste des serveurs de noms autoritaires pour la zone racine du DNS. Cela renverra une liste des serveurs de noms racine du DNS.

2. `dig com. NS @b.root-servers.net.`: Cette commande interroge le serveur de noms racine "b.root-servers.net." pour obtenir la liste des serveurs de noms autoritaires pour la zone de domaine de premier niveau (TLD) ".com". Cela renverra une liste des serveurs de noms autoritaires pour la zone ".com".

3. `dig organic-ip.com. NS @b.root-servers.net.`: Cette commande interroge le serveur de noms racine "b.root-servers.net." pour obtenir la liste des serveurs de noms autoritaires pour le domaine "organic-ip.com". Cela renverra une liste des serveurs de noms autoritaires pour le domaine "organic-ip.com".

4. `dig www.organic-ip.com. NS @b.root-servers.net.`: Cette commande interroge le serveur de noms racine "b.root-servers.net." pour obtenir la liste des serveurs de noms autoritaires pour le sous-domaine "www.organic-ip.com". Cela renverra une liste des serveurs de noms autoritaires pour le sous-domaine "www.organic-ip.com".

5. `dig www.organic-ip.com. A @ns13.ovh.net`: Cette commande interroge le serveur de noms "ns13.ovh.net" pour obtenir l'adresse IP associée au sous-domaine "www.organic-ip.com". Cela renverra l'adresse IP du serveur web associé au sous-domaine "www.organic-ip.com".

## prorpiétés et droits
### visibilité sur les groupes et users
|        Commande         | Utilisation | Exemples                                |
| :---------------------: | :---------: | --------------------------------------- |
| `getent group www-data` |             | voir les utilisateurs d'un group        |
|        `groups`         |             | voir les groups de l'utilisateurs actif |
|                         |             |                                         |


|  Commande  |      Utilisation      | Exemples                                                                                                                                                                                         |
| :--------: | :-------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|  `chown`   |     change owner      |                                                                                                                                                                                                  |
|  `chmod`   |      change mode      | `chmod -V 777` prints the new rights   <br> `chmod 123 monFichier` = `chmod u=x , g=w , o=wx monFichier` <br> `chmod u+r` owner gains reading right <br> `chmod u-x` owner looses execute rights |
|  `chgrp`   |     change groupe     |                                                                                                                                                                                                  |
| `usermod`  |                       | no go                                                                                                                                                                                            |
| `groupadd` |   ajoute un groupe   |                                                                                                                                                                                                  |
| `adduser`  | ajoute un utilisateur | `adduser paul` ouvre une série de lignes de dialogue permettant de rentrer plusieurs informations sur le nouvel utilisateur                                                                      |
|            |                       |                                                                                                                                                                                                  |
pour la syntaxe de `chmod 123 monFichier` :
- le premier chiffre définit les droits de owner
- le second chiffre définit les droits du groupe
- le troisième chiffre définit les droits de other
`chmod 123 monFichier` = `chmod u=x , g=w , o=wx monFichier`

        r vaut 4
        w vaut 2
        x vaut 1

| syntaxe numerique | syntaxe alphabétique |   signification    |                            note                            |
| :---------------: | :------------------: | :----------------: | :--------------------------------------------------------: |
|         7         |         rwx          | read write execute |                                                            |
|         6         |         rw-          |     read write     |                                                            |
|         5         |         r-x          |    read execute    |                                                            |
|         4         |         r--          |        read        |                                                            |
|         3         |         -wx          |   write execute    |                                                            |
|         2         |         -w-          |       write        |                                                            |
|         1         |         --x          |      execute       | --x on a directory means you can path through but not read |
|         0         |         ---          |                    |                                                            |
## naviguer dans les log

|     Commande     |                Utilisation                 | Exemples                                                                                                                                      |
| :--------------: | :----------------------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------- |
|       `ps`       | report a snapshot of the current processes | `ps auxwf`    All User X=etendu W=wide F=forest   output in a tree view so you can see the parent -> child process of all users relationships |
|     `dmesg`      |  print or control the kernel ring buffer   |                                                                                                                                               |
| `journalctl ssh` |         Query the systemd journal          | `journalctl -f -u ssh` pour follow dynamiquement |

## Netplan
Netplan est l'utilitaire de gestion de réseau dans ubuntu server.

|      Commande      |           Utilisation           | Exemples                                                                                                                                                                                          |
| :----------------: | :-----------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cd /etc/netplan/` | localisation du fichier `.yaml` | voir la [doc Netplan](https://ubuntu.com/server/docs/network-configuration) pour trouver la syntaxe. L'idée est de modifier le fichier de config pour donner des paramètres à chaque carte réseau |
|                    |                                 |                                                                                                                                                                                                 |

## SSH tools
| Commande |        Utilisation         | Exemples                                                                                 |
| :------: | :------------------------: | ---------------------------------------------------------------------------------------- |
|  `scp`   |  OpenSSH secure file copy  | just like `cp` but with alternative path syntaxe :`user@192.168.11.1:/home/user/note.md`  <br> `scp -P 222 note.md augustin@192.168.56.3:/home/augustin/`|
| `rsync`  | [repository synchronisation](https://doc.ubuntu-fr.org/rsync) |          `--exclude="nom_de_dossier"` <br> `--exclude-from=ExclusionRSync` charge un fichier de règle s'exclusion <br> `--include="*.csv" --exclude="*"` <br>  `--delete-after` : à la fin du transfert, supprime les fichiers dans le dossier de destination ne se trouvant pas dans le dossier source. <br> `-z` : compresse les fichiers (Limite la bande passante mais augmente l'utilisation processeur et le temps de transfert : inutile en réseau local ou avec très bon débit) <br> `-v` : verbeux <br> `-e ssh` : utilise le protocole SSH    |

## Pipe et stdOutPut

| Commande |          Utilisation           | Exemples                                                        |
| :------: | :----------------------------: | --------------------------------------------------------------- |
|   `>`    | modification de sortie stadard | `ls > fichier` écrit le résultat de la commande dans un fichier <br> `0>` `1>` sortie standard `2>` sortie d'erreur <br> `2>&1` envoie les erreurs vers la sortie standard <dr> `2>/dev/null` supprime directement la sortie des erreurs |
|   `>>`    | modification de sortie stadard | `ls >> fichier`  écrit le résultat à la suite dans le fichier
|   `<`    |    change l'entrée standard    | `grep < fichier` change le std input                            |
|   `\|`   |              pipe              | change le std output                                            |
|          |                                |                                                                 |

## virtual Machines 
|             Commande              |         Utilisation          | Exemples                                   |
| :-------------------------------: | :--------------------------: | ------------------------------------------ |
|       `vboxmanage list vms`       | liste les VMs depuis le Host |                                            |
| `less /var/log/vboxadd-setup.log` |                              | accède aux logs de setup                   |
| `sudo journalctl -f -u 'v*box*'`  |                              | accède aux logs du user v\*box\* et follow |
|                                   |                              |                                            |

