# Installation de DEEPBGC sur une VM Ubuntu

## Prérequis
* Avoir installé VBox avec une VM Ubuntu fonctionnelle.

    Ici j'ai utilisé [Ubuntu Jammy Jellyfish 22.04.4](https://www.ubuntu-fr.org/download/)
* Il est pertinent de connaître [les commandes de base sur UBUNTU](https://korben.info/des-etoiles-lors-de-la-saisie-dun-mot-de-passe-dans-le-terminal.html)

## Installation de Anaconda

1. ce tutoriel fait référence à la [doc d'installation de Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)
2. télécharger [Anaconda](https://www.anaconda.com/download/)
3. ouvrez un terminal de commande

        ctrl + alt + t
4. Vérifiez le cryptage de l'installeur avec la commande :

    `sha256sum /home/lucien/Downloads/Anaconda3-2024.02-1-Linux-x86_64.sh` le retour devrait être :
    `c536ddb7b4ba738bddbd4e581b29308cb332fa12ae3fa2cd66814bd735dff231  /home/lucien/Downloads/Anaconda3-2024.02-1-Linux-x86_64.sh` pas de message d'erreur

    la   chaine de caractère correspond à "la somme" de tout le fichier. Si le fichier est comple, on devrait avoir la même chaîne de caractère. C'est une méthode pour vérifier que le fichier ou système de fichier est complet.
5. Pour exécuter l'installer de ANACONDA :
    
    `bash /home/lucien/Downloads/Anaconda3-2024.02-1-Linux-x86_64.sh`
    * suivez attentivement l'installation, lisez bien tout.
        * l'installer vous dit bonjour " Welcome to Anaconda...Press ENTER to continue"
            * appuyez sur ENTER
        * les conditions générales d'utilisation apparaissent
            * vous voulez les lire ? 
                * oui ? naviguez avec les flèches
                * non ? c'est mal : utilisez les commandes de navigation pour passer rapidement :
                    * SPACE pour sauter 1 page
                    * END-> pour jump à la fin
        * "Do you accept license terms ? \[yes|no\]" acceptez les conditions en tappant "yes" puis ENTER
        * vous avez l'opportunité de changer le répertoire d'installation. Si vous ne souhaitez pas le faire tappez ENTER

            l'installation de python et des paquets peut prendre un long moment.
        * On vous demande si vous voulez que ANACONDA soit lancé par défaut au démarrage du terminal.
            * à priori vous voulez que oui.
            * si vous voulez revenir sur cette décision : `conda config --set auto_activate_base false`
            * pour réactiver :`conda init --reverse $SHELL`
6. vérifiez votre installation
    * fermez puis ré-ouvrez votre terminal
    * exécutez la commande `conda list`
    * normalement vous voyez une list de package installés. 


## Installation de DEEPBGC avec conda

suivez le [README de référence](https://github.com/Merck/deepbgc?tab=readme-ov-file)  pour installer DEEPBGC.

Normalement c'est "straight foreward", il suffis de copier et exécuter les commandes.

Set up Bioconda and Conda-Forge channels:

```bash
conda config --add channels bioconda
conda config --add channels conda-forge
```

Install DeepBGC using:

```bash
# Create a separate DeepBGC environment and install dependencies
conda create -n deepbgc python=3.7 hmmer prodigal

# Install DeepBGC into the environment using pip
conda activate deepbgc
pip install deepbgc

# Alternatively, install everything using conda (currently unstable due to conda conflicts)
conda install deepbgc
```

## first steps
* téléchargez les données de test : 
```bash
deepbgc info
deepbgc download
```
