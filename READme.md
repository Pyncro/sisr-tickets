# Gestion de parc

# 1.Installation VM

Nous utiliserons Ubuntu comme système d'exploitation sur Parallel.

La VM que nous allons utiliser est Parallel (uniquement pour macOS).
![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/parallel%20web.png)


Après avoir installé la VM avec succès, entrez dans le centre de contrôle et cliquez sur l'icône plus.
![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/Add%20IOS.png)

Attention, si vous utilisez une machine Mac M1, la plupart des fichiers IOS (comme linux mint) ne seront pas disponibles à l'installation.
![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/M1%20warning.png)

Cliquez sur l'icône Ubuntu et procédez à l'installation.
![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/choose%20Ubuntu.png)

Un compte sera déjà disponible mais aucun mot de passe n'est défini (il vous demandera d'entrer le mot de passe que vous souhaitez utiliser).
![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/Capture%20d’écran%202022-05-14%20à%2016.21.10.png)



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

![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/status%20works.PNG)

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









![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/glpi%20with%20ip.png)

![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/Accept%20terms%20of%20service.PNG)


![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/package%20extensions.PNG)

![images](https://github.com/Pyncro/sisr-tickets/blob/main/chhh/glpi%20menu.PNG)
