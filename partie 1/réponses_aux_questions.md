## Répondre aux questions suivantes :
- C’est quoi le “working directory” ?

    le working directory c'est le répertoire de travail 🥁
- Comment savoir “où” je suis dans l’arborescence de fichier?

    `§pwd`
- C’est que un chemin absolu ? c’est quoi un chemin relatif ?

    une chemin absolu est un chemin qui part de la racine du système de fichier.
    un chemin relatif part du répertoire courent.
- C’est quoi le Home directory d’un utilisateur ? comment y aller en une commande ?

    le home directory est le répertoire `home/username/` sur ubuntu.
    `cd` ou `cd ~`
- Comment se déplacer dans l’arborescence de fichier ?

    pour se déplacer dans l'arborescence des fichiers on utilise la commande `cd`

    `cd`
    `cd ..`
    `cd ~`
    `cd /home/username`

- Comment lister les fichiers présents ?

    `ls` et ses variantes // alias
- Comment voir le contenu d’un fichier ?

    `cat fichier` pour le voir sur la sortie standard
- Comment avoir de l’aide sur une commande ?

    `man commande` ou `commande --help`
- Comment copier/déplacer/renommer/supprimer un fichier ?

    `cp` ou `mv`
## Chemin et exploration de l’arborescence et caractères de remplacement
- Chemin de fichiers :
  - Dans le terminal, affichez le répertoire courant. Quel est le rapport
entre les deux ?

    L'explorateur de fichiers est une manière $ user friendly $ de naviguer dans les dossier et permet un certains nombre d'actions.

    Le terminal est moins $ user friendly $ mais permet d'exécuter plus d'actions à travers des lignes de commande.

- Comment lister tous les fichiers de la racine du système de fichier ?
    `ls`
  - Trier la liste par date ?
  `ls -t`
  - Ou dans l’ordre inverse ?
  `ls -t -r`
  - Comment voir les propriétés d’un fichier ? (taille, propriétaire,
groupe, ...)
    `ls -l -h` 
  - Comment lister tous les fichiers d’un répertoire ?
    `ll` ou `ls -l`
- A quoi sert la commande `echo` ?
la commande `echo texte` permet d'afficher `texte` dans la sortie standard. Elle peut être utilisée dans un script pour afficher certaines informations via la sortie standard.
- Avec ~~la même~~ une commande, listez tous les fichiers dont le nom termine par `.conf` dans le répertoire `/etc`

    `ls /etc/*.conf`
- Quels autres caractères de remplacement existent dans le bash ?

    `ls /etc/[[:alpha:]]?*.conf` donne le même résultat, à condition que otus les ficheirs aient au moins 2 caractères dans leur nom.
## Complétion et historique de commande
- Tapez ls /e puis :
    - la touche TABULATION (TAB) 1 fois : Que se passe-t-il ?
    la ligne est auto-complétée : on obtient `ls /etc/`
    - puis la touche tab 2 fois, que se passe-t-il ?
    cela devrait nous afficher l'ensemble des possibilités d'auto-complétion mais ici la liste serait trop longuqe alors on nous demande de confirmer. 
    - Comment passer à la page suivante ? Ou quitter immédiatement ?
    `enter` pour avancer d'une ligne
    `space` pour avancer d'une page
    `q` pour quitter
- Comment afficher l’historique des commandes que vous avez déjà tapées ?
    `history`
- Comment afficher la ligne de commande précédemment tapée ?
    `UP`
## Visualiser et modifier le contenu d’un fichier
- Affichez ce fichier sur le terminal
    - avec la commande de concaténation de fichier
    
    `nat notes.md`
    - visualisez le fichier page par page, et lisez le manuel pour pouvoir vous déplacer dans le fichier (revenir au début, aller à la fin, chercher un texte) - https://openclassrooms.com/fr/courses/43538-reprenez-le-controle-a-laide-de-linux/38696-manipuler-les-fichiers
    
    `less notes.md` puis `enter` pour avancer d'une ligne
    `space` pour avancer d'une page
    `q` pour quitter `Début` et `Fin` pour aller directement au début ou à la fin du doc.
- Plusieurs éditeurs en ligne de commande sont disponibles sous unix Vous pouvez lire le tutoriel `vimtuto` pour apprendre les commandes de base de `vim` (éditeur rustique mais présent sur quasiment toutes les machines unix)
    - Prenez des notes des commandes principales mais surtout testez
les commandes
    - Ref 1 : https://www.openvim.com/
    - Ref 2 : https://openclassrooms.com/fr/courses/43538-reprenez-le-controle-a-laide-de-linux/42693-vim-lediteur-de-texte-du-programmeur
- Quelle est votre identité actuellement sur le système ?

    `whoami`
- Installez le package vscode puis sublime-text depuis la ligne de
commande (apt-get) et lancez-le Ressource a lire (chapitre la fin, 8-9) (et pratiquer): Ref : https://www.pierre-giraud.com/shell-bash/commande-navigation-pwd-cd/
    - Quel est le rôle de ~ (lire le tilde) ?
    Le caractère tilde `~` permet de représenter le répertoire de base (home) d’un utilisateur
    - Comment mettre dans un fichier le résultat d’une commande unix ?
    `ls -l > list.txt`
    - A quoi sert la redirection d’une commande dans une autre ?
    par exemple dans `ls -l > list.txt` la sortie standard est ignorée pour être remplacée par un enregistrement dans un fichier `.txt`