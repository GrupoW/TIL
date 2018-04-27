## The process $PROCESS$ exceeded the timeout of 300 seconds.

if you get some error like this:

```
[Symfony\Component\Process\Exception\ProcessTimedOutException]
The process "NODE_ENV=production gulp build -p" exceeded the timeout of 300 seconds.


run-script [--timeout TIMEOUT] [--dev] [--no-dev] [-l|--list] [--] [<script>] [<args>]...
```

you can fix it by adding the following ENV var:


```
dokku config:set APP_NAME COMPOSER_PROCESS_TIMEOUT=2000
```
