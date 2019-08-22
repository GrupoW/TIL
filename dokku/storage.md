## How to use dokku storage:

```
# on your dokku host
storage:list <app>, List bind mounts for app's container(s) (host:container)
storage:mount <app> <host-dir:container-dir>, Create a new bind mount
storage:unmount <app> <host-dir:container-dir>, Remove an existing bind mount
```

### Example

```bash
dokku storage:mount app-name /var/lib/dokku/data/storage:/app/storage
``` 
 
 **IMPORTANT!!!**
 
you must append the "/app" path to the container directory.!!!  
the second path is relative to the root path, not the application working directory.

@reference:   
[dokku storage](https://github.com/dokku/dokku/issues/2284)  
[How to persist folders and files with dokku and docker-options](http://maximilianschmitt.me/posts/persist-folders-files-dokku-docker-options/)
