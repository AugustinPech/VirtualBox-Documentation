# Activité : Se connecter a distance en mode sécurisé
## Phase 1 - avec mot de passe

- Sur la vm, créez un nouvel utilisateur standard (useradd)
- Fixez lui un mot de passe. et vérifier son identité (une fois connectée en tant que cet utilisateur, utiliser la commande id)

**Objectif** : depuis votre poste, vous voulez vous connecter via ssh sur le compte du  sur la vm avec saisie du mot de passe.
- Sur la vm, installer le serveur pour le protocole ssh sur votre machine (openssh-server)
- Notez l’IP du serveur (la vm).
            
        192.168.56.3/24
- Depuis votre poste, connectez vous avec ssh vers le serveur en utilisant la saisie de votre mot de passe.

        ssh ringo@192.168.56.3
## Phase 2 - avec une clef publique/privée
Objectif : depuis votre poste, vous voulez vous connecter via ssh sur le compte du nouvel utilisateur sur la vm sans saisie de mot de passe et en utilisant une authentification par un système de clés publique/privée.
- Pour que vous puissiez vous connecter sur l’utilisateur de la vm.
    - Etapes : Génération d’une clef public/privé sur votre poste (depuis votre utilisateur habituel).
    - Installer VOTRE clef publique sur l’endoit spécifique du compte de l’utilisiateur dont vous avez recu le login / pass sur l’ordinateur distant.
    - Testez pour vérifier que tout marche correctement.
- Faites une capture des trames avec Wireshark et regardez le contenu.
    - Voyez-vous le contenu de vos échanges ?
                
            Oui, is on sniffe la bonne carte réseau
    - Quel est le port et le protocole de transport utilisé ? (celui qui est à l’intérieur des paquets IP dans la partie tcp)

            c'est le port 22, le port par défaut du protocole SSH.
## Phase 3 – paramètrages complémentaires
- Changer le port d’accès au serveur. (mais à quoi ca sert ??), et paramétrez votre client pour que la commande ssh ip_de_mon_serveur fonctionne encore. (man ssh_config)
        
        ça sert à sécuriser le SERVER pour éviter les scans automatiques.
        éventuellement ça peut servir à éviter des conflits sur le port 22 , si plusieurs services essayaient de s'y connecter.
- Vérifier/paramétrer que l’utilisateur root ne peux pas connecter via ssh
- Vérifier les services qui sont en écoute (listen) sur votre serveur ? (netstat & lsof)
`netstat -tuln`
`sudo lsof -i -P -n | grep LISTEN`
- Vérifier les services accessibles depuis l’extérieur de votre serveur (nmap).
        - depuis le guest : 
                - auto scan `nmap 192.168.56.3`
                - scan du host `nmap 192.168.8.174`
                - scan de l'adresse vboxnet du host via host only `nmap 192.168.56.1`
        - depuis le host :
                - auto scan `nmap 192.168.8.174`
                - scan du guest via host only `nmap 192.168.56.3`

## Phase 4 – Diverses utilisations de ssh
- Copier un fichier distant vers votre poste via le service ssh.

HOST --> GUEST
`scp -P 222 note.md augustin@192.168.56.3:/home/augustin/`

GUEST --> HOST
`scp -P 222 augustin@192.168.56.3:/home/augustin/note.md /home/augustin/Desktop/`
- Vérifiez que la completion fonctionne pour les fichiers distants 

        ce n'est pas dynamique
## Pour aller plus loin :
- tunnel ssh : Utiliser le tunnel ssh pour acceder au service web de la machine alors que son accès est bloqué par le firewall (tcp/80 reject). Expliquez le principe de fonctionnement. et comment ca permet de “contourner” des règles de filtrages IP.

Ref : https://phoenixnap.com/kb/ssh-port-forwarding
la syntaxe `ssh -L local_port:destination_server_ip:remote_port ssh_server_hostname` permet de connecter un port local vers un port distant d'un IP donnée




Trouver une utilisation et un exemple à présenter.



