## You must include the `mbstring` extension in your composer.json 

When deploying to dokku or heroku the [Multibyte String](http://php.net/manual/en/book.mbstring.php) extension for PHP must be enabled, otherwise [tale-jade](https://github.com/Talesoft/tale-jade) won't work.


####composer.json

```json
{
    "name": "root/local.dev",
    "require": {
         "php": ">=5.5.9",
         "ext-mbstring" : "*",
         "talesoft/tale-jade": "*"
    }
}

```
