### Install apache and mod
```
$sudo apt-get install apache2 libapache2-mod-fastcgi
```
### Install php and modules
```
$sudo apt-get install php5-fpm php5-pgsql php5-mcrypt
```
### Enable apache modules
```
$sudo a2enmod actions fastcgi alias
```

### Configure php5-fpm
Edit file /etc/apache2/mods-enabled/fastcgi.conf
```
<IfModule mod_fastcgi.c>
    AddHandler php5-fcgi .php
    Action php5-fcgi /php5-fcgi
    Alias /php5-fcgi /usr/lib/cgi-bin/php5-fcgi
    FastCgiExternalServer /usr/lib/cgi-bin/php5-fcgi -socket /var/run/php5-fpm.sock -pass-header Authorization
    
    <Directory /usr/lib/cgi-bin>
        Require all granted
    </Directory>
</IfModule>
```
### Create virtual host
First create directory, and own rights
```
mkdir /home/lara
chown -R UN:UG /home/lara 
```
Edit file /etc/apache2/sites-available/001-lara.conf
```
<VirtualHost *:16080>

        ServerAdmin webmaster@localhost
        DocumentRoot /home/lara/public

        <Directory /home/lara/public>
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error_lara.log
        CustomLog ${APACHE_LOG_DIR}/access_lara.log combined

</VirtualHost>
```
restart apache and php5-fpm
```
$sudo systemclt restart apache2 php5-fpm
```
