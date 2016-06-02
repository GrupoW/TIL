##How To Set Up mod_rewrite for Apache

enable mod_rewrite:

```
$ sudo a2enmod rewrite
$ sudo service apache2 restart
```

add the following block to your `.conf` located at `/etc/apache2/sites-available/` and change your document root directory.

```apacheConf
<Directory /var/www/document_root_directory>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Order allow,deny
                allow from all
</Directory>
```

it should look like the following:

```apacheConf
<VirtualHost *:80>
ServerAdmin localserver@localhost
ServerName sample-domain.mx
ServerAlias www.sample-domain.mx
DocumentRoot /var/www/sample-domain/public
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
<Directory /var/www/sample-domain/public>
  Options Indexes FollowSymLinks MultiViews
  AllowOverride All
  Order allow,deny
  allow from all
</Directory>
</VirtualHost>
```

restart apache

```
$ sudo service apache2 restart
```


@reference: [How To Set Up mod_rewrite for Apache on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-mod_rewrite-for-apache-on-ubuntu-14-04)