# SilverStripe 4 docker development environment

Install docker based development environment for SilverStripe 4 application

## Maintainer Contact

* Brett Tasker <brett.tasker@gmail.com>

## Requirements

* [Docker](https://docs.docker.com/engine/installation/)
* SilverStripe 4.0+

## How to use

### Require ss4-docker-compose configuration

```bash
composer require --dev brettt89/ss4-docker-compose
```

### Start services

```bash
./vendor/bin/docker-compose up -d
```

By default, this setup will create 2 containers per project and 1 global nginx proxy (ss-proxy).

Containers:
 - **web** (web server)
   - Hostname: {folder_name}.local
 - **database** (database server)
   - Hostname: {folder_name}.db.local

NOTE: In order to access the servers by hostname you will need to map these domains to your "Hosts" IP.

E.g. File: /etc/hosts, ({folder_name} = ss4)

127.0.0.1	ss4.local

### Advanced usage

The docker-compose executable included in this package does some additional checks and configuration with commands. This should always be used over the native docker-compose function.

However all docker-compose commands can be used via this package as per usual.

E.g. SSH into web server.

```bash
./vendor/bin/docker-compose exec web /bin/bash
```
