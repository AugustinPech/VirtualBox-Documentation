## Consigne
- Vérifiez que votre serveur web est bien paramétré sur votre vm, sinon installez le.

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
- Faites le test d’accès aussi depuis votre poste.
- Renseignez-vous sur les différents firewalls disponibles sous linux (ubuntu/debian) et des outils de configurations associés

        La notion de pare-feu :
      Un pare feu est un composant du réseau qui se positionne en intermédiaire entre 2 éléments. 
      Il filtre le passage entre ces 2 éléments , le plus osuvnetin est paramétré pour ne laisser passer que certains types de connexions.
      Un pare-feu peut être logiciel ou matériel.

Doc Ref. [iptable](https://doc.ubuntu-fr.org/iptables) , [firewall](https://doc.ubuntu-fr.org/pare-feu), [NFtable](https://en.wikipedia.org/wiki/Nftables)

- Que pensez-vous de ce qui est dit dans ce document concernant “la soit disant” non utilité d’avoir un firewall sur un réseau local ou à la maison ?
    
    [Dans le cas où votre routeur inclut un module de pare-feu et que celui-ci est activé, vous n'avez pas réellement besoin d'activer un pare-feu logiciel dans votre système Ubuntu.](https://doc.ubuntu-fr.org/pare-feu) -- $doc-ubuntu$ --
      
      Dans ce cas, le pare-feu du rooter peut être considéré suffisant.
      Puisque le rooter est connecté en NAT sur l'Internet , la connexion devrait être 'one-way'.
      
      
- Dans quel cas, celà vous parait légitime ou non légitime ?

      Il est légitime d'avoir un pare-feu dans le cas d'un réseau domestique, un utilisateur malveillant pourrait se connecter au Wifi sans être présent dans le logement.

      On peut considérer que ce niveau de sécurité est suffisant, ça dépend de l'enjeu.
    en IPV4 :
      
      une machine branchée sur un host en NAT sur le net n'est pas routable.

    en IPV6 :

      une machine est routable directement, il faut un pare feu.
## Après échanges avec le formateur :
- Configurez le firewall pour bloquer tous les accès entrant sauf l’accès à votre service web (et ssh ).

DOC Ref. [service ufw](https://help.ubuntu.com/community/Gufw)
- Testez, bloquez tous les accès entrant , puis tester à nouveau (y compris le surf depuis votre serveur vers internet)

fait, voir [notice d'intall de web server](../noticeInstallingWebOnTheServer.md)
- Regardez depuis la ligne de commande, les règles présentent dans le firewall.

  les règles sont contenues dans le fichier de conf `less /etc/nftables.conf`
- Vous devez pouvoir tapper les commandes en ligne de commande pour pouvoir paramétrer les firewall sur le serveur distant.

  Je ne comprend pas la queqstion, si s'en est une.

## Informations & pistes :
    Si services ufw retenu :
    - desactivation du service nftables : systemctl disable nftables.service
    - activation du service ufw : systemctl enable ufw.service
    - Lancement du service ufw : systemctl start ufw.service

    [Suivre la notice](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

    Garder une trace des quelques commandes utilisées pour ouvrir / fermer des ports / ...
    Valeurs par defaut :
    ufw status verbose | grep -i default
Si nftables retenu :
https://github.com/geraldhmt/nftables-apply/

- Après avoir récupéré (et vérifier) nftables-apply, l’installer dans /usr/local/sbin (par exemple)

  Vérification :
  `sudo which nftables-apply` => Doit donner : /usr/local/sbin/nftables-apply
- Créer un fichier a appliquer (/etc/nftables-candidate.conf) à partir de https://wiki.nftables.org/wiki-nftables/index.php/Simple_ruleset_for_a_server
- tester la mise en place du nouveau fichier de regles avec : `nftables-apply`
- Autres exemple de fichiers : https://wiki.gentoo.org/wiki/Nftables/Examples
## Fail2Ban / sshguard :
Pour améliorer la protection de votre serveur, vous avez entendu parlé
de Fail2Ban ou sshGuard.
### Questions guides :
  - A quoi sert sshGuard ou fail2ban ? (les objectifs)
    
      ce sont des outils de filtre des requètes SSH destinés à bloquer les attaques de type "brut force" 
  - Quel est le principe de fonctionne de fail2ban/sshguard (comment est articulé le principe de fonctionnement) ?

      SSHGuard utilise des journaux système pour repérer les requêtes SSH et surtout les répétition de requêtes invalides.
      Si plusieurs requètes invalides arrivent sur le serveur depuis une même adresse IP, SSHguard//fail2ban bloque cette addresse pendant un temps donné ou éventuellement définitivement
  - Comment je peux vérifier que c’est fonctionel ?

      j'ouvre le log `sudo journalctl -f`
      J'envoie des requêtes SSH invalides au serveur en surveillant le log.
  - Quels fichiers sont utilisés pour la detection des attaques ?

      les journaux système
- Pour aller plus loin (option)
  - tunnel ssh : Comment utiliser ssh et une connexion sur la machine pour utiliser l’accès ssh pour acceder au service web de la machine alors que son accès est bloqué par le firewall (tcp/80 reject).
  - Expliquez le principe de fonctionnement. et comment ca permet de “contourner” des règles de filtrages IP. (Vous pourrez faire ca plus facilement après installation du service apache sur le serveur)
- Sauvegarde via ssh + rsync
  - Faite un script de synchronisation avec rsync a distance. L’objectif est de faire une synchronisation (pour une sauvegarde), alors que l’on a que l’accès ssh à la machine distante.
  - Remarque : Attention aux chemins utilisés pour ne pas écraser vos données.
  
Doc2Ref : https://doc.ubuntu-fr.org/rsync

Références :

https://www.sshguard.net/

http://doc.ubuntu-fr.org/fail2ban

https://www.installerunserveur.com/installer-fail2ban

https://www.linuxtricks.fr/wiki/fail2ban-bannir-automatiquement-les-intrus