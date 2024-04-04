## Introduction
Le wiki est un programme qui est écrit en langage php. Pour fonctionner, il a donc besoin d’un serveur web qui puisse exécuter des scripts php.
## Installer l’archive dokuwiki depuis le site de dokuwiki
- Télécharger [l’archive](https://download.dokuwiki.org/) (.tar.gz ou .tar.bz2) de la dernière version stable (ce qui est le choix par défaut)
- Maintenant que apache2 est installé, il génère des logs à chaque appel de page, et vous devez les rajouter dans les logs suivis en temps réel avec le terminal dédié (avec tail). Les logs d’apache sont dans /var/log/apache2/ et finissent par log.

`tail -f /var/log/*log /var/log/apache2/*log`

`scp ~/Downloads/dokuwiki-a6b3119b5d16cfdee29a855275c5759f.tgz ubuntu@92.222.217.84:~/`
- Toujours en ligne de commande, décompressez l’archive de dokuwiki dans le répertoire temporaire (/tmp/ ) puis déplacez le contenue de l’archive vers la racine du service web (les fichiers distribuées par apache2 (/var/www/domains/dokuwiki.local/html)

`tar -xvf dokuwiki-a6b3119b5d16cfdee29a855275c5759f.tgz -C /var/www/html/`

- Configurez un vhost : /etc/apache2/site-available/dokuwiki.local.conf qui contient la configuration pour ce nouveau vhost pour un accès en http.
Note : dokuwiki utilise les .htaccess, qu’il faut donc activer pour ce domaine (chercher : AllowOverride)
- Accédez au dokuwiki /var/www/domains/dokuwiki.local/html
  * Note : le service apache2 fonctionne en tant qu’utilisateur spécifique ( regardez ‘ps aux | grep apache2’)
  * Il faut que cet utilisateur puisse accéder aux fichiers et répertoires de dokuwiki pour que le système fonctionne.
  * Il ne faut pas que tous les utilisateurs puisse venir et accéder à tous les fichier (même pas en lecture).
  * Choisissez les droits/user et groupe que vous souhaitez pour les fichiers et appliquez les à tout le répertoire dokuwiki.
  * Lors de l’installation de dokuwiki, choisissez le mode d’accès wiki fermé (ou public éventuellement).

## Les questions auxquelles vous devriez pouvoir répondre :
- Comment fonctionne les limitations d’accès aux fichiers sous unix ?
- Quel est le rapport entre le propriétaire d’un fichier et un utilisateur ?
- Comment savoir à quels groupe j’appartiens ?
- Quelles sont les commandes pour modifier les droits d’un fichier, le propriétaire ? le groupe ? ...
- Comment je vérifie si mon service web sera relancer au prochain démarrage du serveur ?