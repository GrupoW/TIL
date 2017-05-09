## Increase WP Upload Limit

ssh to host and go to the container's dir
```
cd /home/dokku/project_name
```

make the directory `nginx.conf.d` and create a file with upload limit setting:
```
sudo mkdir nginx.conf.d && echo "client_max_body_size 50M;" >> nginx.conf.d/upload.conf
```

restart nginx service
```
sudo service nginx reload
```
