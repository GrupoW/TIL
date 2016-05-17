##How to deploy a PHP aplication to dokku with nested document root:

####project structure:

```
├── Procfile
├── composer.json
├── composer.lock
├── public/
│   ├── index.php
└── vendor/
```


####composer.json:

```json
{
    "name": "root/local.dev",
    "require": {
    	"php": ">=5.5.9",
        "ext-mbstring" : "*",
    }
}
```

####Procfile:  
```
web: vendor/bin/heroku-php-apache2 public/
```

####index.php:  

```php
<?php
  echo "Hello World";
```

	 