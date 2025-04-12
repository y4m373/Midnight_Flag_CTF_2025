# Description

I only trust what I see and, guess what ? I don't see any vulnerability in my app. 

# Solving

For this challenge, we have access to the source code. We can see two part of the website `back` and `front` in the `apache.conf` :

```
<VirtualHost *:80>
    DocumentRoot /var/www/html/front
</VirtualHost>

<VirtualHost *:8080>
    DocumentRoot /var/www/html/back
    <Location />
        Require ip 127.0.0.1
    </Location>
</VirtualHost>

Listen 8080
```
In front we have a page that permit to `curl` an url but only if it's not 'localhost' or '127.*` :

```php
// Prevent DNS rebinding
try {
    $ip = gethostbyname($parsed['host']);
} catch(Exception $e) {
    die("Failed to resolve IP");
}

// Prevent from fetching localhost
if (preg_match("/^127\..*/",$ip) || $ip === "0.0.0.0"){
    die("Can't fetch localhost");
}

$url =  str_replace($parsed['host'],$ip,$url);
```

So i tried this payload : `http://[::ffff:7f00:1]:8080/flag.php` Which bypass the test but I got an error message : `You are not allowed to do that`.
In fact in the `flag.php` there is an other test to check if you are a local user :

```php
<?php

if ($_SERVER['HTTP_HOST'] === "localhost:8080"){
    echo getenv('FLAG');
} else {
    echo "You are not allowed to do that";
}
?>
```
You have to be `localhost` and i'm `127.0.0.1` so I crafted this page that redirect to `http://localhost:8080/flag.php` and uploaded it on my vps and create a simple php server `php -S ip:port -t web/`.
And when I curl it, it gave me : `MCTF{a1104b51a44ecb61585cafacd59f77c1}`




