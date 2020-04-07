Nginx is an extremely efficient and quite flexible web server. When you want to do a redirect in Nginx, you have a few options to select from, so you can choose the one that suits you best to do an Nginx redirect.

# Using Maps

firstmake sure you have the `map_hash_bucket_size` property in there, if not. add the following line inside of *http* block of your pdate nginx.conf file.

```
http {
  […]
  map_hash_bucket_size 128;
}
```

include your map file outside of the *server* block and redirect condition.

```
include redirect-map.conf;
server {
    […]
    if ( $redirect_uri ) {
        return 301 $redirect_uri;
    }
}
```

the file redirect-map.conf may then look something like this:

```
map $request_uri $redirect_uri {
    /about.html          /about-us;
    /customers.html      /our-customers;
    /products.html       /our-products;
}
```

@reference: [How to do an Nginx redirect](https://www.bjornjohansen.com/nginx-redirect)

