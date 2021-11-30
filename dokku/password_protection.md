## Add Basic Auth to your Dokku APP:

**With NGINX:**  
add the following lines to your nginx.conf:

```
# Basic Password Protection
location / {
  auth_basic "Restricted";
  auth_basic_user_file /app/public/.htpasswd;
}
```

create an `.htpasswd` in your public folder and add the contents from [htpasswd generator site](https://hostingcanada.org/htpasswd-generator/), for example: 

```
mysecretuser:{SHA}OTaE2jKfdhdhta+aEertrter2SPE=
```

@reference:  
[Basic authorization for app](https://github.com/dokku/dokku/issues/111)   
[Password protecting directories with Nginx](https://help.dreamhost.com/hc/en-us/articles/215837528-Password-protecting-directories-with-Nginx) 
