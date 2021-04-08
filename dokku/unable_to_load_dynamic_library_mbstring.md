# PHP Warning:  PHP Startup: Unable to load dynamic library 'mbstring.so'

1. Make sure your app uses these 2 buildpacks:

```
https://github.com/heroku/heroku-buildpack-apt
https://github.com/heroku/heroku-buildpack-php
```

2. Create a new file Aptfile on root directory with content as below:
```
libonig-dev
libonig4
```

3. `git add`, `git commit` and deploy, it should work now
