##How to add new ssk key:

run the following command as root:

```
cat ~/.ssh/id_rsa.pub | ssh root@rauluranga.com sshcommand acl-add dokku $USER
```

example:

```
cat /Users/raul/Downloads/id_rsa.pub | ssh root@rauluranga.com "sudo sshcommand acl-add dokku ivan"
```

@reference:  
[advanced-installatio](https://github.com/dokku/dokku/blob/master/docs/advanced-installation.md)  
[dokku add new ssh key](https://www.digitalocean.com/community/questions/dokku-add-new-ssh-key)