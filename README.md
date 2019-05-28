<p align=center><img height=150 src="https://raw.githubusercontent.com/php-protein/docs/master/assets/protein-large.png"></p>

# Protein | URL
## Helper object for parsing, building and handling URLs

### Install
---

```
composer require protein/url
```

Require the class via :

```php
use Protein\URL;
```

### Parse an URL
---

Create a new URL object passing the existing URL as constructor parameter, that will be automatically parsed into URL components.

```php
$url = new URL('https://user:pass@www.alpha.beta.com:9080/path/to/resource.html?foo=bar&another[]=2&another[]=3#frag_link');

print_r($url);
```

```
Object
(
    [scheme] => https
    [user] => user
    [pass] => pass
    [host] => www.alpha.beta.com
    [port] => 9080
    [path] => /path/to/resource.html
    [query] => Array
        (
            [foo] => bar
            [another] => Array
                (
                    [0] => 2
                    [1] => 3
                )

        )

    [fragment] => frag_link
)
```

URL class can autocast itself as the builded URL string :

```php
echo "$url";
```

```
https://user:pass@www.alpha.beta.com:9080/path/to/resource.html?foo=bar&another%5B0%5D=2&another%5B1%5D=3#frag_link
```

## Build or modify an URL
---

You can modify or build from scratch an URL altering the single components :

```php
$url = new URL();

$url->host = 'caffeina.com';
$url->user = 'demo';

echo $url;
```

```
demo@caffeina.com
```

```php
$url = new URL("ftps://test.com:9000/index.php");

$url->scheme = 'https';
$url->port = false;

echo $url;
```

```
https://test.com/index.php
```

## Examples
---

#### Build a mailto address :

```php
$link = new URL('mailto://');
$link->user = 'info';
$link->host = 'myserver.com';

$link->query['subject'] = 'This is a subject';
$link->query['body'] = 'Hi! This is a test... :D';

echo $link;
```

```
mailto://info@myserver.com?subject=This+is+a+subject&body=Hi%21+This+is+a+test...+%3AD
```