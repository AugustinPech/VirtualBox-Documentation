# Installation de virtualBox sur UBUNTU
1. mettez à jour votre OS avec 2 commandes :

    `sudo apt update` et `sudo apt upgrade`
2. téléchargez la version de VBox sur [le site d'Oracle](https://www.virtualbox.org/wiki/Downloads)
3. rendez-vous dans votre répertoire de téléchargements

    `cd Downloads/`
4. vérification avec `ls`
5. `dpkg-deb -xv virtualbox-7.0_7.0.14-161095~Ubuntu~jammy_amd64.deb . | tree --fromfile`
6. `sudo apt install ./virtualbox-7.0_7.0.14-161095~Ubuntu~jammy_amd64.deb` 
7. Configurer le groupe `vboxusers` :

    `sudo usermod -a -G vboxusers $USER`

    si le groupe `vobxusers` n'existe pas :

    `sudo groupadd vboxusers`
8. lancer `virtualbox`


## Installation des ExtensionPack
1. téléchargez l'extension pack sur https://www.virtualbox.org/wiki/Downloads
2. dans l'interface de VBox `tools->extensions` 
## Téléchargement de l’image ubuntu serveur
1. Télécharger l'image d'ubuntu server sur [le site d'Oracle](https://www.ubuntu-fr.org/download/) (fichier `.iso`)

## création de la VM
1. sélectionner l'image .iso de Ubuntu server que vous avez téléchargé.
2. lors de la création cochez l'option

    [X] skip Unattended Installation
3. lors du paramètrage du hardware cochez l'option 

    [X] EFI enable,
4. allouez des ressources raisonnables

    [X] Pre-alocate full-size
5. valider la création et lancer votre machine
## Nice settings
|          chemin           |         choix         |                         sens                          |
| :-----------------------: | :-------------------: | :---------------------------------------------------: |
|    System -> Processor    | [X] enable Nested VT  |            peut contenir une VM dans la VM            |
|          Storage          |                       | permet de gérer les périphériques comme "en physique" |
| Display -> Remote Display |   [ ] enable Server   |              à priori : ne pas faire ça               |
|          Network          |   Adapter 1,2,3,...   |         permet de rajouter des cartes réseau          |
|     Réseau -> Avancés     | fixer la carte réseau |        `Paravirtualized network (virtio-net)`         |
|                           |                       |                                                       |

## installation de UBUNTU 

à propos de la partition de disk :

        set up LVM

LVM est un outil qui permet de gérer un lot de DD physiques comme un seul disque de manière dynamique.

Sur une VM ça ne change rien mais c'est super cool.q
## Installation des additions invités

avant de commencer il faut installer un module kernel : `sudo apt install dkms linux-headers-$(uname -r) build-essential` Il s'agit d'un driver VBox qui lie le noyau du Guest au noyau du Host.

`dpkg -L virtualbox-7.0 | grep -i .iso` vous donne la liste des chemins des fichiers `.iso` qui ont été installés avec le package virtualbox-7.0.
<br>vous devriez voir`/usr/share/virtualbox/VBoxGuestAdditions.iso`, nomalement.
<br>c'est l'iso qui est utilisé ici

1. insérer l'image .iso dans le guest
    * depuis le menu de VBox
        1. MaVBox ==> Settings ==> Storage
        <br>Dans controller IDE sélectionnez le lecteur optique (symbole de CD)
        2. à droite du menu déroulant `Optical Drive` sélectionnez l'icone CD puis l'option `choose a disk file` 
        3. allez chercher votre fichier `.iso` pour 'l'inserrer'
    * depuis la fenètre du Guest
        1. dans la barre d'outils :
        2. Devices ==> Insert Guest Additions CD image
        3. la commande `blkid` vous permet de voir qu'un fichier de `TYPE="iso9660"` est dans `/dev/` le fichier `sr0`
            
                /dev for device
                it has the devices in it 
                fucking genius
2. montez l'image du ROM `sr0`
        <br> `sudo mount /dev/sr0 /mnt/` mont l'image dans `/mnt`
        <br> `mount` pour run le contenu de `/mnt`
3. on ve voir ce qu'on a fait 
        <br> `cd /mnt`
        <br> `ls`
        <br> on voit plusieurs exécutables
4. On exécute le bon fichier
    1. `sudo ./autorun.sh` devrait fonctionner
    2. à défaut `sudo ./VBoxLinuxAdditions.run`
        * il manque surement le package `bzip2`
                <br>`sudo apt install bzip2`
        * retantez `sudo ./VBoxLinuxAdditions.run`
5. Finaliser l'install `sudo /sbin/rcvboxadd setup`
<br> c'est bien de reboot à ce stade