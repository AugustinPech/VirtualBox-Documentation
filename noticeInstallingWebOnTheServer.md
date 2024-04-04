# Installing a web server on a VMserver
## Installer apache 
pour vérifier si apache2 est installé `sudo systemctl status apache2.service`

à défaut `sudo apt install apache2`

vérifier que APACHE2 écoute sur le prot 80 `sudo ss -ltnp`

la sortie ressemble à ça :
| State  | Recv-Q | Send-Q | Local Address:Port | Peer Address:Port | Process                                                                            |
| :----: | :----: | :----: | :----------------: | :---------------: | ---------------------------------------------------------------------------------- |
| LISTEN |   0    |  128   |    0.0.0.0:222     |     0.0.0.0:*     | users:(("sshd",pid=723,fd=3))                                                      |
| LISTEN |   0    |  4096  |  127.0.0.53%lo:53  |     0.0.0.0:*     | users:(("systemd-resolve",pid=646,fd=14))                                          |
| LISTEN |   0    |  128   |      [::]:222      |      [::]:*       | users:(("sshd",pid=723,fd=4))                                                      |
| LISTEN |   0    |  511   |        *:80        |        *:*        | users:(("apache2",pid=739,fd=4),("apache2",pid=738,fd=4),("apache2",pid=737,fd=4)) |

* vérification :
    * dans le HOST,
        * ouvrir un navigateur
        * tapper l'IP : `nomdelaVM`
        * si ça ne marche pas : verifier la config de `/etc/hosts`
    * dans la VM,
        * pour suivre les logs :
            *  passer en mode root : `sudo -i`
            *  ouvrir le fichier de log `tail -f /var/log/apache2/access.log`
## Install php for apache2
doc2ref : https://ubuntu.com/server/docs/programming-php
* installer php avec le module pour APACHE2  `sudo apt install php8.1-fpm`
* créez un fichier `var/www/html/info.php` contenant
    ```php
        <? php
            phpinfo();
        ?>
    ```
* enable the php8.1-fpm configuration `sudo a2enconf php8.1-fpm`
* `sudo systemctl restart apache2`
* testez l'install via le HOST/CLIENT avec l'url `http://monNomDeDomaine.truc/info.php`

## Firewall configuration
### NFtable
* vérifier l'install :
    * il y a un fichier de conf ?
       - la commande : `ls /etc/*nf*` devrait retourner un fichier `nftables.conf`
            * à défaut :
                * installer NFTable :
                    * vérifier si on a le package `dpkg -L | grep -i nft`
                        * à défaut : `sudo apt install nftables`
    * si il y a un fichier de conf :
        * la service tourne-t-il ? `sudo systemctl status nftables.service` puis en fonction `sudo systemctl start nftables.service`
        * desactivez ufw `sudo systemctl disable ufw.service `
        * arrêtez `sudo systemctl stop ufw.service`
        * activez NFTables`sudo systemctl enable nftables.service `
    * changer une config NFTables
        * pour configurer nftables-apply on copie la conf de gérald sur son repo gitHub
            * créez un Dir `mkdir bin`
            * aller dedans `cd bin/`
            * cloner la came de Gerald `git clone https://github.com/geraldhmt/nftables-apply.git`
            * regarder le contenu `find . -ls | grep -v \\.git/`
            * copier le fichier `nftables-apply` dans `/usr/local/sbin/` pour le rendre exécutable par **root**
        * vérification :
            * la commande `sudo which nftables-apply` devrait renvoyer le chemin vers l'exécutalbe nftables-apply
    * pour mettre à jour les règles il faut créer un fichier `candidate` qui est le "futur" fichier de conf du par-feu :`sudo touch nftables-candidate.conf`
        * modifier le fichier :`sudo vi nftables-candidate.conf`
        
        pour avoir une conf toute faite qui marche bien : [cliquer sur le lien et copier le contenu](https://wiki.nftables.org/wiki-nftables/index.php/Simple_ruleset_for_a_server) 
        
    * pour appliquer le nouveau ruleset : `sudo nftables-apply`
    un choix s'offre à vous, avant de choisir : 
        
          Là , il faut vraiment être sûr.
          testez une nouvelle connextion SSH sur un autre terminal.
    * si ça fonctionne choicissez oui
    * sinon il faut changer la config de `nftable-candidate.conf` 
### SSHGuard
* `sudo apt install sshguard`
* ouvrez les logs `sudo journalctl -f`
* dans un autre terminal testez une connection avec un user bidon
    * vous avez dans le log un message d'attaque.