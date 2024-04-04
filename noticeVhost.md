# les commandes pour ouvrir un nouveau vhost 
**Remarque:**  
  Si le Vhost est sur une VM il faut faire une redirection DNS depuis `/etc/hosts` dans le HOST

| HOST                             | GUEST                        |
| :------------------------------- | :--------------------------- |
| ```IPV4.de.la.VM monsite.truc``` | ```127.0.0.1 monsite.truc``` |
## avec NginX
- Pour créer un nouveau vHost il faut créer un fichier `newhost.local` à l'adresse `/etc/nginx/sites-available`
	- commande 1 :
`cd /etc/nginx/sites-available`
	 - commande 2 :
`sudo touch newhost.local`

- Ensuite il faut y placer du contenu :
	 - commande : 
`sudo vi newhost.local`
	- le contenu (les parties en  <span style="color:red">rouge </span> sont les points à modifier): 
	`server {`
		`listen 80;`
		`server_name` <span style="color:red">newhost </span>`.local;
		index index.php;`
		`root /var/www/` <span style="color:red">newhost </span>`;`
		`location ~ \.php$ {`
			`include snippets/fastcgi-php.conf;`
			`fastcgi_pass unix:/var/run/php/php` <span style="color:red">8.3 </span>`-fpm.sock;`
		`}`
	`}`
- on crée un lien symbolique : `sudo ln -s /etc/nginx/sites-available/newhost.local /etc/nginx/sites-enabled/`
- à l'adresse `/var/www/newhost` il faut créer un fichier `index.php`
	- commande 1 :
	`sudo mkdir /var/www/newhost`
	- commande 2 :
	`cd /var/www/newhost`
	- commande 3 :
	`sudo touch index.php`
- Ensuite il faut y placer du contenu :
 	- commande : 
`sudo vi index.php`
	- ici le contenu est une ligne de texte pour tester.

- il faut ajouter une ligne au fichier `etc/hosts` 
	- commande 1 :
	`sudo vi /etc/hosts`
	- il faut rajouter la ligne `127.0.0.1	`<span style="color:red">newhost</span>`.local`
## avec Apache2
|                                            installation de php-fpm                                             |                                                                                                                     config vhost                                                                                                                     |                                                    conf de php-fpm                                                     |               doc officielle apache complète de difficile               |
| :------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------: |
| [doc cloudbooklet](https://www.cloudbooklet.com/developer/how-to-install-php-fpm-with-apache-on-ubuntu-20-04/) | - [doc DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-18-04-quickstart-fr) <br> - [doc adventy](https://adventy.org/fr/tutoriel/comment-creer-et-configurer-un-hote-virtuel-sur-apache) | [doc it-connect](https://www.it-connect.fr/comment-configurer-apache2-avec-php-fpm-8-2-pour-executer-les-scripts-php/) | [doc apache](https://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html) |
|                                                                                                                |                                                                                                                                                                                                                                                      |                                                                                                                        |                                                                         |


### définir le DNS
- il faut ajouter une ligne au fichier `etc/hosts` 
*	- commande 1 :
```bash
sudo vi /etc/hosts
```
*
	* il faut rajouter la ligne

```bash
127.0.0.1	repo.truc
```
### le répertoire du projet

- créer le répertoire

	...si ce n'est pas déjà fait
```bash
sudo mkdir -p /var/www/repo.truc
```
- gérer les droits dans ce répertoire
```bash
sudo chown -R www-data:www-data /var/www/repo.truc #le groupe de apache possède le répertoire
sudo usermod -a -G www-data user # l'utilisateur actif est dans le gfroupe www-data 
sudo chmod -R 755 /var/www # (user)www-data : rwx (group)www-data : r-x (other) : r-x
```
### la conf
il y a une configuration par défaut dans les ficheir d'apache
- copier la conf par défaut en la renommant :
```bash
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/repo.truc.conf
```
- modifier la conf
```bash
sudo vi /etc/apache2/sites-available/repo.truc.conf
```
dokuwiki.local
- adapter le contenu par défaut à votre projet
```bash
<VirtualHost *:80>
	# Associate domain name with project folder
	ServerAdmin webmaster@repo.truc
	DocumentRoot /var/www/repo.truc/
	ServerName repo.loc
	ServerAlias repo.loc

	# (optional) Define log files
	ErrorLog ${APACHE_LOG_DIR}/repo.truc-error.log
	CustomLog ${APACHE_LOG_DIR}/repo.truc-access.log combined

	# (optional) Define log level (possible values include: debug, info, notice, warn, error, crit, alert, emerg)
	LogLevel warn

	<Directory /var/www/repo.truc>
		AllowOverride All
	
		# New directive needed in Apache 2.4.3: 
		Require all granted
	</Directory>
	 
</VirtualHost>
```
#### inclure php dans la conf

pour inclure la conf de PHP il y a 2 manières de faire :
1) inclure la même conf de php pour tous les sites

si on run la commande : 
```bash
sudo a2enconf php8.1-fpm
```
on ajoute alors la conf de php8.1-fpm au dossier conf-available de apache2.
Ce n'est pas forcément une bonne pratique car cela implique que la conf php8.1-fpm est appliquée dans tous les vhosts.

Pour revenir sur cette commande :
```bash
sudo a2disconf php8.1-fpm
```

2) inclure une conf de php par site 
il faut rajouter dans le fichier de conf de chaque vhost le bloque suivant :
```bash
<FilesMatch \.php$>
    SetHandler "proxy:unix:/run/php/php8.2-fpm.sock|fcgi://localhost/"
</FilesMatch>
```
Ici on inclue la conf de php8.2-fpm. La partie `/run/php/php8.2-fpm.sock|` peut être variable et il faut vérifier l'existence du fichier.
### ajouter le vhost aux sites d'apache
la commande :
```bash
a2ensite /etc/apache2/sites-available/repo.truc
```
permet d'ajouter le fichier de conf que l'on vient de créer aux sites enabled de apache.
On peut roleback avec :
```bash
a2dissite /etc/apache2/sites-available/repo.truc
```
### redémarrer papache2
```bash
sudo systemctl restart apache2
```