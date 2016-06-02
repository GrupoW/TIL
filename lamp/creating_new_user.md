## How to create new user on linux

This example creates a new user called "demo", but you should replace it with a user name that you like.  

sign-in as `root` on your guest machine and run the following commands: 

**Step 1: Add user:**

```
$ adduser demo
```

**Step 2: Root privileges:**   

```
$ gpasswd -a demo sudo
```

**Step 3: Write permissions:**

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

**Step 4: Add Public Key Authentication :**  

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

**Step 5: Copy the public key:**

install `ssh-copy-id` (in case you don't already have it)

```
$ brew install ssh-copy-id
```

```
$ ssh-copy-id -i my.key.pub demo@SERVER_IP_ADDRESS
```

Your first time connecting to a new host, you will see a message that looks like this:  

```
The authenticity of host '111.111.11.111 (111.111.11.111)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
```

if you wan't to remove the password authentication, just add the following to the sshd config on the server `/etc/ssh/sshd_config`.  

```
PasswordAuthentication no
```


@reference:  

* [Initial Server Setup with Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04)   
* [Why doesn't chown -R root:www-data work on my Wordpress installation?](https://www.digitalocean.com/community/questions/why-doesn-t-chown-r-root-www-data-work-on-my-wordpress-installation) (read comments)
* [SSH Essentials: Working with SSH Servers, Clients, and Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)  
* [Disable password access through SSH](http://askubuntu.com/questions/1991/disable-password-access-through-ssh)  

