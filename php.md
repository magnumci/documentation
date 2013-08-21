# PHP Projects

Build environment has the latest PHP v5.3 with `phpunit` and `composer` 
packages installed. 

## Dependencies

Magnum CI will detect if application is using [composer](http://getcomposer.org/) 
and will attempt to install application dependencies with:

```
composer install --dev
```

You can override that by adding `install` section to `.magnum.yml` config:

```
install:
  - git clone PLUGIN_URL
```

## Test Suite Execution

For applications using [PHPUnit](http://www.phpunit.de/) and with defined `phpunit.xml`
manifest file Magnum CI will run test suite with:

```
phpunit
```

To override default test command, use `script` section in magnum config (or 
using build settings). Example:

```
script: phpunit --coverage-text .
```

## PHP Extensions

Build VM comes with list of preinstalled extensions. If you need to install a 
different extension, you can use `install` section in config. Example:

```yaml
install:
  - sudo apt-get update -y
  - sudo apt-get install -y php5-curl
```

Pre-installed extensions:

- bcmath
- bz2
- calendar
- Core
- ctype
- curl
- date
- dba
- dom
- ereg
- exif
- fileinfo
- filter
- ftp
- gd
- gettext
- hash
- iconv
- json
- libxml
- mbstring
- mcrypt
- memcache
- mhash
- mysql
- mysqli
- mysqlnd
- openssl
- pcntl
- pcre
- PDO
- pdo_mysql
- pdo_pgsql
- pdo_sqlite
- pgsql
- Phar
- posix
- readline
- Reflection
- session
- shmop
- SimpleXML
- soap
- sockets
- SPL
- SQLite
- sqlite3
- standard
- suhosin
- sysvmsg
- sysvsem
- sysvshm
- tokenizer
- wddx
- XCache
- XCache Cacher
- xdebug
- xml
- xmlreader
- xmlwriter
- zip
- zlib