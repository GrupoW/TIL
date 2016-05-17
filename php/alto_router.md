##How to use [AltoRouter](http://altorouter.com) for php

project structure:

```
├── app/
│   ├── controllers/
│       └── home_controller.php
├── composer.json
├── composer.lock
├── index.php
└── vendor/
```

composer.json:

```php
{
    "name": "root/local.dev",
    "require": {
    	"php": ">=5.5.9",
        "ext-mbstring" : "*",
        "altorouter/altorouter": "^1.2",
    }
    "autoload": {
        "psr-4": {
            "App\\Controllers\\": "app/controllers"
        }
    }
}

```

home_controller.php:

```
<?php 
namespace App\Controllers;

Class HomeController {   
  
  function index() {
  	echo "Hello Index!";
  }	
  
}
```


index.php:  

```php

require_once __DIR__ . '/vendor/autoload.php';

$router = new AltoRouter();
$router->map( 'GET', '/', 'App\Controllers\HomeController#index', 'home');

// match current request
$match = $router->match();

var_dump(match);

if ($match) {
  
  list($controller, $method) = explode("#",$match['target']);

  if(is_callable(array($controller,$method))) {
    $object = new $controller();
    call_user_func_array(array($object,$method), array($match['params']));
  } else {
    echo "Can not find $controller->$method";
    exit();
  }

} else {
  // no route was matched
  header($_SERVER["SERVER_PROTOCOL"]." 404 Not Found", true, 404);
  echo '404 Not Found<br/>';
  // include("notFound.php");
}
```