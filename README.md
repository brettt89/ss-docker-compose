# SilverStripe 4 docker development environment

Docker based development environment for SilverStripe 4 applications
Can be used on multiple environments at the same time.

## Maintainer Contact

* Brett Tasker <brett.tasker@gmail.com>

## Requirements

* [Docker](https://docs.docker.com/engine/installation/)

## Install

To install globally run:

`composer global require brettt89/ss4-docker-compose`

Make sure your `~/.composer/vendor/bin` directory is in your PATH.

`echo 'export PATH=$PATH:~/.composer/vendor/bin/'  >> ~/.bash_profile`

Then you can run this script with `docker-ss <docker-compose command>` in your project root.

## How to use

`docker-ss` in a nutshell is basically a wrapper for `docker-compose` with some added functionality and checks. all `docker-compose` commands should run as expected via `docker-ss`

### Environment file

Ensure you have an environment file setup in your project root with the following settings.

```
# DB credentials
SS_DATABASE_CLASS = "MySQLPDODatabase"
SS_DATABASE_SERVER = "database"
SS_DATABASE_USERNAME = "root"
SS_DATABASE_PASSWORD = ""
SS_DATABASE_NAME = "SS_mysite"
```

### Start services

```bash
docker-ss up -d
```

By default, this setup will create 2 containers per project and 1 global nginx proxy (ss-proxy).

Containers:
 - **web** (web server)
   - Hostname: `{folder_name}.local`
 - **database** (database server)
   - Hostname: `{folder_name}.db.local`

NOTE: In order to access the servers by hostname you will need to map these domains to your "Hosts" IP.

E.g. File: `/etc/hosts`, (`{folder_name} = "./ss4"`)

```hostfile
127.0.0.1	ss4.local ss4.db.local
```

### Advanced usage

The docker-compose executable included in this package does some additional checks and configuration with commands. This should always be used over the native docker-compose function.

However all docker-compose commands can be used via this package as per usual.

#### Running dev/build.

```bash
docker-ss exec web ./vendor/bin/sake dev/build
```

#### SSH into web server (Bash terminal).

```bash
docker-ss ssh
```

#### Accessing database from client

```
Host: {folder_name}.db.local
Port: 3306
Database: SS_mysite
Username: root
Password: <empty>
```
