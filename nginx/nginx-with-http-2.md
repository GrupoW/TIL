# How To Set Up Nginx with HTTP/2 Support

HTTP/2 is a new version of the Hypertext Transport Protocol, which is used on the Web to deliver pages from server to browser.

## Prerequisites

* One Ubuntu 18.04 server set up by following [the Ubuntu 18.04 initial server setup guide](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04), including a sudo non-root user and a firewall.
* Nginx installed on your server, which you can do by following [How To Install Nginx on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04).
* A domain name configured to point to your server. You can purchase one on Namecheap or get one for free on Freenom. You can learn how to point domains to DigitalOcean Droplets by following the How To Set Up a Host Name with DigitalOcean tutorial.
* A TLS/SSL certificate configured for your server. You have three options:
  * You can get a free certificate from Let’s Encrypt by following [How to Secure Nginx with Let’s Encrypt on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-18-04).
  * You can also generate and configure a self-signed certificate by following How to Create a Self-signed SSL Certificate for Nginx in Ubuntu 18.04.
  * You can buy one from another provider and configure Nginx to use it by following Steps 2 through 6 of  How to Create a Self-signed SSL Certificate for Nginx in Ubuntu 18.04.
* Nginx configured to redirect traffic from port 80 to port 443, which should be covered by the previous prerequisites.
* Nginx configured to use a 2048-bit or higher Ephemeral Diffie-Hellman (DHE) key, which should also be covered by the previous prerequisites.

### Redirec from port 80 to port 443

```
server {
        listen 80;
        listen [::]:80;
        access_log  off;
        error_log   off;
        server_name www.your-domain.com;
        return 301 https:/www.your-domain.com$request_uri;
}

server {
        listen 80;
        listen [::]:80;
        access_log  off;
        error_log   off;
        server_name your-domain.com;
        return 301 https://your-domain.com$request_uri;
}
```

### Redirec from SSL naked domain to WWW
```
server {

        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        access_log  off;
        error_log   off;

        server_name your-domain.com;

        ssl_certificate /etc/letsencrypt/live/your-domain.com/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem; # managed by Certbot

        return 301 https://www.your-domain.com$request_uri;
}
```

### Generate Diffie-Hellman Group
```
openssl dhparam -out /etc/nginx/ssl/dhparam.pem 2048
```

### Main Server Block with security improved 
```
server {

        listen 443 ssl http2;
        listen [::]:443 ssl http2;

        server_name www.your-domain.com;

        ssl_certificate /etc/letsencrypt/live/your-domain.com/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem; # managed by Certbot
        # include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        # ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

        # ---- START Configuration for improved security ---
     
        ssl_session_cache shared:le_nginx_SSL:50m;
        ssl_session_timeout 1d;
        ssl_session_tickets off;
        
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_prefer_server_ciphers on;

        ssl_ciphers EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5;
 
        ssl_dhparam /etc/nginx/ssl/dhparam.pem;
        ssl_ecdh_curve secp384r1;

        # OCSP stapling
        ssl_stapling on;
        ssl_stapling_verify on;
        ssl_trusted_certificate /etc/letsencrypt/live/your-domain.com/chain.pem;
        resolver 8.8.8.8 8.8.4.4 valid=300s;
        resolver_timeout 5s;

        # ---- END Configuration for improved security --- 
.
.
.
```

ssl_ciphers
ssl_dhparam
ssl_ecdh_curve
ssl_stapling

### Enabling HTTP Strict Transport Security (HSTS)

create file: /etc/nginx/snippets/security-headers.conf with the following contents:

```
# Strict Transport Security Header
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
add_header X-Frame-Options DENY;
add_header X-Content-Type-Options nosniff;
```

update naked domain block
```
server {
	listen 443 ssl http2;
	listen [::]:443 ssl http2;
	
	access_log  off;
	error_log   off;
	
	server_name your-domain.com;
	
	ssl_certificate /etc/letsencrypt/live/your-domain.com/fullchain.pem; # managed by Certbot      
	ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem; # managed by Certbot
	
	include /etc/nginx/snippets/security-headers.conf;

        return 301 https://www.your-domain.com$request_uri;
}
```

### Browser Caching

```
        .
        .
        .

        include /etc/nginx/snippets/security-headers.conf; 
	       
        # ---- END Configuration for improved security --- 
        
        # Browser Caching https://gist.github.com/philipstanislaus/654adafad91efb6de230845b5bdeae61

        location ~* \.(?:css|js|html)$ {
            access_log        off;
            log_not_found     off;
            expires           7d;
            add_header        Cache-Control "public, no-transform";
            include /etc/nginx/snippets/security-headers.conf;
        }
        
        location ~* \.(?:jpg|jpeg|gif|png|ico|xml|pdf|ppt|pptx|doc|docx|txt|bmp|rtf|svg)$ {
            access_log        off;
            log_not_found     off;
            expires           30d;
            add_header        Cache-Control "public"; 
            include /etc/nginx/snippets/security-headers.conf;
        }

        location ~* \.(?:eot|woff|woff2|ttf|otf) {
            access_log        off;
            log_not_found     off;
            expires           30d;
            add_header        Cache-Control "public";
            add_header        Access-Control-Allow-Origin *;
            include /etc/nginx/snippets/security-headers.conf;

            types     {font/opentype otf;}
            types     {application/vnd.ms-fontobject eot;}
            types     {font/truetype ttf;}
            types     {application/font-woff woff;}
            types     {font/x-woff woff2;}
        }

        location ~ /\. {
            access_log        off;
            log_not_found     off;
            deny              all;
        }


```


### References.  

* [SSL Configuration Generator](https://ssl-config.mozilla.org/)
* [Let's Encrypt from Start to Finish: Tuning with OpenSSL](https://blog.wizardsoftheweb.pro/lets-encrypt-from-start-to-finish-openssl-tuning/)
* [Let's Encrypt from Start to Finish: Useful Headers](https://blog.wizardsoftheweb.pro/lets-encrypt-from-start-to-finish-useful-headers/)
* [How To Set Up Nginx with HTTP/2 Support ](https://dev.to/grigorkh/how-to-set-up-nginx-with-http2-support-2mgb)
* [Aceleración SSL/TLS con NGINX](https://enmilocalfunciona.io/aceleracion-ssl-tls-con-nginx/)
* [Security/Server Side TLS](https://wiki.mozilla.org/Security/Server_Side_TLS)
* [Configure Nginx to use TLS 1.2 and 1.3 only](https://www.cyberciti.biz/faq/configure-nginx-to-use-only-tls-1-2-and-1-3/)
* https://gist.github.com/leandromoreira/1c655189b8fae2e24175
* https://gist.github.com/plentz/6737338
* [How to properly configure your nginx for TLS](https://medium.com/@mvuksano/how-to-properly-configure-your-nginx-for-tls-564651438fe0)
* [How to get a 100% score on SSL Labs (Nginx, Let’s Encrypt)](https://zurgl.com/how-to-get-a-100-score-on-ssl-labs-nginx-lets-encrypt/)
* [Getting a Perfect SSL Labs Score](https://michael.lustfield.net/nginx/getting-a-perfect-ssl-labs-score)
* [Super-fast Secure WordPress Install on DigitalOcean with NGINX, PHP7, and Ubuntu 16.04 LTS](https://morphatic.com/2016/05/21/super-fast-secure-wordpress-install-on-digitalocean-with-nginx-php7-and-ubuntu-16-04-lts/)
* [TLS All The Things! Perfect 100 SSL-Labs Score Revisited](https://dawnbringer.net/blog/1083/TLS_All_The_Things!_Perfect_ssl-labs_score_for_Nginx)
* [Adding HSTS to nginx config](https://serverfault.com/questions/874936/adding-hsts-to-nginx-config)


