# Database Setup

Build environment includes the following databases:

- [PostgreSQL](http://www.postgresql.org/) - *started automatically*
- [MySQL](http://dev.mysql.com/) - *started automatically*
- [MongoDB](http://www.mongodb.org/) - *started automatically*
- [Redis](http://redis.io)
- [Memcached](http://memcached.org/)
- [ElasticSearch](http://www.elasticsearch.org/)
- [RabbitMQ](http://www.rabbitmq.com/)
- [CouchDB](http://couchdb.apache.org/)
- [Beanstalkd](http://kr.github.io/beanstalkd/)

## PostgreSQL

PostgreSQL server is automatically started with each build and listens on
`127.0.0.1:5432`. Its also configured to trust all local connections. Use user
`postgres` and blank password for  authentication. Default database encoding is
set to UTF8.

Database creation example:

```
psql -c 'create database hello;' -U postgres
```

## MySQL

MySQL server is automatically started with each build and listens on
`127.0.0.1:3306`. Use user `root` with blank password for
authentication.

Database creation example:

```
mysql -u root -e 'create database hello;'
```

## MongoDB

MongoDB server is automatically started and listens on `127.0.0.1:27017`. User
authentication is not required. Does not require to create a database, it'll be
created dynamically based on your application behavior.

## Redis

Redis server should be started manually. Configured to listen on
`127.0.0.1:6379`. Does not require authentication.

Use magnum config (or build settings) to require redis on startup:

```
services:
  - redis-server
```

## Memcached

Memcached server should be started manually. Configured to listen on
`127.0.0.1:11211`. Does not require authentication.

Use magnum config (or build settings) to require memcached on startup:

```
services:
  - memcached
```

## ElasticSearch

ElasticSearch server should be started manually. Configured to listen on
`127.0.0.1:9200`. Does not require authentication.

Use magnum config (or build settings) to require elasticsearch on startup:

```
services:
  - elasticsearch
```

## RabbitMQ

RabbitMQ server should be started manually. Configured to listen on
`127.0.0.1:5672`. Does not require authentication.

Use magnum config (or build settings) to require rabbitmq on startup:

```
services:
  - rabbitmq-server
```

## CouchDB

CouchDb server should be started manually. Configured to listen on
`127.0.0.1:5984`. Does not require authentication.

Use magnum config (or build settings) to require couchdb on startup:

```
services:
  - couchdb
```

## Beanstalkd

Beanstalkd server should be started manually. Configured to listen on
`127.0.0.1:1130`. Does not require authentication.

Use magnum config (or build settings) to require beanstalkd on startup:

```
services:
  - beanstalkd
```
