## How to add new ssk key:

run the following command as root:

```
cat ~/.ssh/id_rsa.pub | ssh root@rauluranga.com dokku ssh-keys:add $USER
```

example:

```
cat /Users/raul/Downloads/seca_rsa.pub | ssh root@rauluranga.com dokku ssh-keys:add seca
```

@reference:  
[User Management](https://github.com/dokku/dokku/blob/master/docs/deployment/user-management.md)  
