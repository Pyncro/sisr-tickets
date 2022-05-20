# Gestion de parc

# 1.Installation VM

Nous utiliserons Ubuntu comme système d'exploitation sur Parallel.

La VM que nous allons utiliser est Parallel (uniquement pour macOS).
![clipboard.png](nA9n0JeMM-clipboard.png)


Après avoir installé la VM avec succès, entrez dans le centre de contrôle et cliquez sur l'icône plus.
![clipboard.png](p-hUyl5c3-clipboard.png)

Attention, si vous utilisez une machine Mac M1, la plupart des fichiers IOS (comme linux mint) ne seront pas disponibles à l'installation.
![clipboard.png](skmxp_lGk-clipboard.png)

Cliquez sur l'icône Ubuntu et procédez à l'installation.
![clipboard.png](3af3o7df6-clipboard.png)

Un compte sera déjà disponible mais aucun mot de passe n'est défini (il vous demandera d'entrer le mot de passe que vous souhaitez utiliser).
![clipboard.png](n7pvmeatn-clipboard.png)



# 2.Install MySQL
 
 avant de commencer, procéder à la mise à jour du logiciel dans le terminal:
 
>sudo -i  > apt-get update > apt-get upgrade
>

Puis:


```
sudo apt install mysql-server mysql-client

```


```
mysql -u root -p
```


* Créez une base de données nommée glpi
* Créez un compte utilisateur MySQL nommé glpi
* Donnez un contrôle total sur la base de données glpi à l’utilisateur glpi

```
mysql> CREATE DATABASE glpi CHARACTER SET UTF8 COLLATE UTF8_BIN;
CREATE USER 'glpi'@'%' IDENTIFIED BY 'glpi';
GRANT ALL PRIVILEGES ON glpi.* TO 'glpi'@'%';
FLUSH PRIVILEGES;
quit;

```

# Install web Apache
```
sudo apt install apache2 php php-mysql libapache2-mod-php

```

```
sudo apt install php-json php-gd php-curl php-mbstring php-cas php-xml php-cli php-imap php-ldap php-xmlrpc php-apcu

```


```
sudo a2enmod rewrite

sudo systemctl restart apache2
```


```
sudo nano /etc/apache2/apache2.conf 
```

```
<Directory /var/www/html>
  AllowOverride All
</Directory>

```


```
sudo apt install locate

locate php.ini
```

```
sudo nano /etc/php/7.4/apache2/php.ini
```

```
file_uploads = On
max_execution_time = 300
memory_limit = 256M
post_max_size = 32M
max_input_time = 60
max_input_vars = 4440
```

Redémarrez Apache et vérifiez l’état du service :

![clipboard.png](vOMzGnlLb-clipboard.png)
# Install GLPI

```

cd /tmp

wget https://github.com/glpi-project/glpi/releases/download/9.4.5/glpi-10.0.0.tgz

tar -zxvf glpi-10.0.0.tgz

```

```
sudo mv glpi /var/www/html/
```

```
sudo chown -R www-data /var/www/html/glpi
```

```
sudo nano /etc/apache2/conf-available/glpi.conf
```

```
<Directory /var/www/html/glpi>
  AllowOverride All
</Directory>

<Directory /var/www/html/glpi/config>
  Options -Indexes
</Directory>

<Directory /var/www/html/glpi/files>
  Options -Indexes
</Directory>
```









![clipboard.png](Ybg3PVplv-clipboard.png)

![clipboard.png](UNPfsYw45-clipboard.png)


![clipboard.png](O5OPy29BX-clipboard.png)

![clipboard.png](ENOQcBiop-clipboard.png)