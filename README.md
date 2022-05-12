# Gestion de parc

Nous utiliserons Linux mint comme système d'exploitation sur Hyperv.
![clipboard.png](nd3uouyud-clipboard.png)
 
 
 commencant par:
 
>sudo i  > apt-get update > apt-get upgrade
>

Puis:


```
sudo apt-get install apache2 php mysql-server libapache2-mod-php php-mysql php-curl php-mbstring  php-gd php-xml

```


```
sudo apt-get install glpi 
```


```
cd /tmp
```

```
wget https://github.com/glpi-project/glpi/releases/download/10.0.0/glpi-10.0.0.tgz
```

```
cd /opt/
```


```
sudo tar -xvzf /tmp/glpi-10.0.0.tgz
```

> cd /etc/apache2/conf-available/

```
touch glpi.conf
```

```
Alias /glpi /opt/glpi

<Directory /opt/glpi>
  DirectoryIndex index.php
  Options FollowSymLinks
  AllowOverride Limit Options FileInfo
  Require all granted
</Directory>
```


```
sudo a2enconf glpi.conf
```

```
sudo systemctl reload apache2
```a

```
sudo systemctl restart apache2
```
