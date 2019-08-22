## How know MariaDB IP Address:

print the containers with `docker ps -a`:

```
root@zombeats:/home# docker ps -a
CONTAINER ID        IMAGE                            COMMAND                CREATED            STATUS                  PORTS              NAMES
9bb043653336        dokku/zombts:deployed            "/start"              6 days ago          Up 6 days              5000/tcp            app_zombts_1426962032_16369
36d26bb052aa        busybox:buildroot-2014.02        "true"                6 days ago          Exited (0) 6 days ago                      cache_data_zombts
9b98ea49b3b0        ayufan/dokku-alt-mongodb:latest  "/usr/bin/start_mong  6 days ago          Up 6 days              27017/tcp          mongodb_single_container
d2a5dcadd44a        dokku/kikobeats-blog:deployed    "/start"              7 days ago          Up 7 days              5000/tcp            app_kikobeats-blog_1426940104_29078
01c804801ca6        ayufan/dokku-alt-mariadb:latest  "/usr/bin/start_mari  7 days ago          Up 7 days              3306/tcp            mariadb_single_container
8eeb59abbd54        busybox:buildroot-2014.02        "true"                7 days ago          Exited (0) 7 days ago                      cache_data_kikobeats-blog
```


inspect the container using `docker inspect 9b98ea49b3b0 | grep IPAddress` to check what IP Adress has being exposing and voilá!:

```
"IPAddress": "172.17.0.11"
```



