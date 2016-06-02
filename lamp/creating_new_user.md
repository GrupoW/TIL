## How to create new user on linux

This example creates a new user called "demo", but you should replace it with a user name that you like.  

sign-in as `root` on your guest machine and run the following commands: 

**Add user:**

```
$ adduser demo
```

**Root privileges:**   

```
$ gpasswd -a demo sudo
```

**Write permissions:**

```
$sudo usermod -a -G www-data demo
```
set permissions for user group www-data

```
sudo chgrp -R www-data /var/www/html
```

followed by
  
```
sudo chmod -R g+w /var/www/html
```

**Add Public Key Authentication :**  

The next step in securing your server is to set up public key authentication for your new user.  
Before you generate an SSH key, you can check to see if you have any existing SSH keys.

```
$ ls -al ~/.ssh 
```

By default, the filenames of the public keys are one of the following:

* id_dsa.pub
* id_ecdsa.pub
* id_ed25519.pub
* id_rsa.pub

install `ssh-copy-id` (in case you don't already have it)

```
$ brew install ssh-copy-id
```

**Copy the public key:**

```
$ ssh-copy-id -i my.key.pub demo@SERVER_IP_ADDRESS
```




@reference:   
[Initial Server Setup with Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04)   
comments on: [Why doesn't chown -R root:www-data work on my Wordpress installation?](https://www.digitalocean.com/community/questions/why-doesn-t-chown-r-root-www-data-work-on-my-wordpress-installation)