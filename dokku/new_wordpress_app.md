## How to create new Wordpress app:

run the following commands:

replace APP_NAME with the corresponding application name

```
dokku apps:create APP_NAME
dokku mariadb:create BD_NAME
dokku mariadb:link BD_NAME APP_NAME
dokku storage:mount APP_NAME /var/lib/dokku/data/APP_NAME/uploads:/app/web/content/uploads
```

example `jeep`:

```
dokku apps:create jeep
dokku mariadb:create jeep
dokku mariadb:link jeepbc jeep
dokku storage:mount jeep /var/lib/dokku/data/jeep/uploads:/app/web/content/uploads
```
