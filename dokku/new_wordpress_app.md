## How to create new Wordpress app:

run the following commands:

replace APP_NAME with the corresponding application name

```
dokku apps:create APP_NAME
dokku mariadb:create BD_NAME
dokku mariadb:link BD_NAME APP_NAME
dokku memcached:create APP_CACHE_NAME
dokku memcached:link APP_CACHE_NAME APP_NAME
dokku storage:mount APP_NAME /var/lib/dokku/data/APP_NAME/uploads:/app/web/content/uploads
```

example `jeep`:

```
dokku apps:create jeep
dokku mariadb:create jeep_bd
dokku mariadb:link jeep_bd jeep
dokku memcached:create jeep_cache
dokku memcached:link jeep_cache jeep
dokku storage:mount jeep /var/lib/dokku/data/jeep/uploads:/app/web/content/uploads
```
