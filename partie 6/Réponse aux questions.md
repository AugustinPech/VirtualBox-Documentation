## Introduction
Le document a été écrit pour le service web apache2.

- Pour regarder en temps réel les log dans le système vous pouvez ouvrir un premier terminal, et utilise la commande tail (cherchez la bonne option) Le fichier de log système est /var/log/syslog.

`tail -f /var/log/syslog`
- Dans un terminal dédié, en une seule commande, suivez au fil de leurs remplissage, les fichiers de log contenu dans le répertoire /var/log/. Il faut suivre le fichier syslog ainsi que tous les fichiers qui terminent par log dans ce même répertoire.

`tail -f /var/log/syslog /var/log/*.log`
- Installez le service apache2 et le language php => Regardez les logs en temps réel, trace de ce qui se passe durant l’installation.
- A partir de votre navigateur, votre site est disponible sur http://127.0.0.1
* Vous devez avoir la page par défaut Apache2

* Pour valider que le php fonctionne, écrivez le fichier suivant /var/www/html/info.php qui contient ce qui suit
```php
<?php phpinfo(); ?>
```
* Pour vérifier appelez depuis votre navigateur :
http://127.0.0.1/info.php
* Vous devez avoir une page avec de nombreuses informations liées
à php.
* Félicitations, le serveur web est opérationel.

## Questions auxquelles vous devriez pouvoir répondre maintenant :
* Dans le monde unix/Linux, c’est quoi un service ?, c’est quoi un daemon ?

        Un service est un (ou plusieurs) programmes qui forunissent une fonctionnelité à l'OS.

        Un démon est u ntype particulier de service qui tourne en arrière plan , sans avoir forcément d'intéraction avec l'utilisateur.
* C’est quoi le service php-fpm ?

        PHP FastCGI Process Manager est un service d'interprétation PHP qui est utilisé par apache (ou NginX, ou autre) pour interpréter des script PHP de manière dynamique.
* Comment s’articule-t-il avec apache ? (dessin du traitement d’une requette php)

        lorsque la requète HTTP reçue par le serveur APACHE pointe vers un script PHP, APACHE requière que PHP-FPM exéxcute le code.
* Puis-je avoir plusieurs versions différentes de php sur mon serveur ?

        oui
* Pourquoi c’est pas php qui joue le role du serveur web directement ?

        PHP n'est pas conçu pour être serveur WEB. Il génère du contenu dynamqiue.
* Pour aller plus loin :
    * Tous les scripts php de mon serveur partagent-ils le même espace mémoire ?

            non
    * Comment améliorer la sécurité de mon service php ?

            il existe une très grande variété de techniques et bonnes pratiques de sécurité en PHP. On peut notamment siter le filtrage des données de l'utilisateur pour éviter les injections de code.