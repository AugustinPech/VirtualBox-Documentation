# Configuration d'une nouvelle connexion SSH
DOC de ref. https://doc.ubuntu-fr.org/ssh

Dans une connexion SSH on nomme "CLIENT" et "SERVER" les deux extrèmités de la connexion.
## Installation
* sur le SERVER
    1. Pour vérifier si le service est déjà installé :
        * `ssh -V`
        * `sudo systemctl`... `status` // `start` // `stop`  // `restart`...`ssh`
    2. pour installer `sudo apt install openssh-server`
* sur le CLIENT
    1. normalement `openssh-client` est déjà installé sur UBUNTU
    2. sinon `sudo apt install openssh-client`
## Connexion depuis le CLIENT
* en IPV4 `ssh <nom_utilisateur>@<ipaddress>`
    * le port par défaut est le `22`
    * pour préciser le port : `-p <num_port>`
    * si il y a un mot de passe : il sera demandé.
* en IPV6 `ssh -6 <nom_utilisateur>@<adresse ipv6>`

* pour quitter `logout`

## Utilisation de clés SSH public / privée
DOC de ref.  https://doc.ubuntu-fr.org/ssh#authentification_par_un_systeme_de_cles_p
* générer une clés sur le CLIENT
    * générer la clé `ssh-keygen -t ed25519`
    * ajouter la clé à SSH-agent `ssh-add chemin/vers/ma/clé`
    * copiez la clé vers l'utilisateur distant `ssh-copy-id -i ~/.ssh/id_ed25519.pub <username>@<ipaddress>`
    * attendez un peu, réessayez une 20aine de fois

## Changer le port du protocol SSH
* sur le SERVER 
    1. ouvrez le fichier de config de votre SERVER SSH `sudo vi /etc/ssh/sshd_config`
    2. trouvez la ligne `Port 22`
    3. changez le port 
    4. restart le daemon SSH `sudo systemctl restart sshd`
* sur le CLIENT
    DOC Ref. https://www.rix.fr/blog/cours/utiliser-la-configuration-ssh-client
    https://www.ssh.com/academy/ssh/config
    1. aller dans la répertoire de config de votre CLIENT SSH `sudo vi /etc/.ssh/`
    2. créez le fichier config `sudo touch config`
    3. dans votre fichier de config il y a une syntaxe à respecter pour rentrer des paramètres par défaut.

| dans le fichier `~/.ssh/config`                                                                                        | dans le fichier `/etc/hosts` | commentaires                                                                                                                                                            |
| :--------------------------------------------------------------------------------------------------------------------- | :--------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Host maVMTropCool <br>--HostName 192.168.56.3 <br>--User ringo <br>--Port 222 <br>--IdentityFile ~/.ssh/id_ed25519.pub | //                           | le fichier de config SSH peut assumer <br> la responsabilité du stockage de l'IP <br> mais c'est moins sécurisé, si le fichier <br> fuite , il y a trop d'informations. |
| Host maVMTropCool <br>--User ringo <br>--Port 222 <br>--IdentityFile ~/.ssh/id_ed25519.pub                             | 192.168.56.3 maVMTropCool    | le fichier `/etc/hosts` donne la  <br> entre ce nom de domaine et une adresse IP |

## Bloquer la connexion SSH pour l'utilisateur root
* sur le SERVER
    1. ouvrez le fichier de config de votre client SSH `sudo vi /etc/ssh/sshd_config`
    2. changer le ligne `PermitRootLogin` ...  `no`
## synchroniser 2 répertoires CLIENT <-> SERVER
doc ref https://doc.ubuntu-fr.org/rsync


la commande : `rsync -az /home/augustin/Desktop/Système\ et\ réseau/ augustin@192.168.56.3:/home/augustin/` copie un directory vers un autre mais n'est pas dynamique


## transfert de fichier
doc Ref . https://doc.ubuntu-fr.org/ssh

la commande `scp -P 222 note.md augustin@192.168.56.3:/home/augustin/` à la même structure que `cp` mais il y a une écriture alternatif de chemin avec la syntaxe `user@IP:/path/` à la palce de `/path/`
## port forwarding 
la syntaxe `ssh -L local_port:destination_server_ip:remote_port ssh_server_hostname` permet de connecter un port local vers un port distant d'un IP donnée

## Framework anti-intrusion
### SSHGuard
n'est pas compatible avec `ufw`
### Fail2Ban
[Fail2ban est un service analysant en temps réel les journaux d'évènement de divers services (SSH, Apache, FTP, entre autres) à la recherche de comportements malveillants et permet d'exécuter une ou plusieurs actions lorsqu'un évènement malveillant est détecté.](https://fr.wikipedia.org/wiki/Fail2ban)
--- $wikipedia$ ---
## 
