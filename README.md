# Nginx + MariaDB/MySQL + PHP-FPM + PHP 7.0 + phpMyAdmin + Redis

Based on [laradock](https://github.com/LaraDock/laradock) (an environment to
start with Laravel).

It's made for having a __PHP__ + __DB__ environment quickly through
docker-compose configuration. You can use any library or framework.

The _workspace_ container gives you a basic Bash + PHP (with Composer)
installation.

## How to use
First, you need to install __docker-compose__.

You can create the environment cloning this repo:
```bash
# Cloning repository
git clone https://github.com/aboglioli/phpdock.git
cd phpdock

# Building the environment and setting it up.
# You can write mariadb instead of mysql if you want to use this.
# It can take a while (some minutes).
docker-compose up -d nginx mysql

# And access the workspace to install libraries or frameworks with composer
docker-compose exec workspace bash
```

## Public folder
Nginx and php-fpm __WORKDIR__ is _/var/www/public_ and __app/__ local directory
(where will be you application or PHP code) outside phpdock is referenced with
_/var/www_ inside application container (application code container).

So you have to make a directory called _public/_ inside _app/_ local directory.
It will have the root directory of your application. By this way, you can
include PHP files from the parent directory (_../_) to your code and that files
can't be accessed directly from the browser.


## Help & Questions
If you have problems, contact me: _alan.boglioli@gmail.com_
If you improve this and you want to share it, send a Pull Request.

## License
[MIT License](https://github.com/aboglioli/aboglioli/blob/master/LICENSE) (MIT)
