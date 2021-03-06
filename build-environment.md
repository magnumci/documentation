# Build Environment

Test suite builds are executed in an isolated environment on a host machine. 
Every time new build is scheduled, runner creates a fresh virtual machine from pre-built 
image for the corresponding project type. All images are built on top of the 64-bit 
Ubuntu 12.04 LTS and provisioned automatically. 

When build execution is complete the virtual machine gets permanently destroyed and 
there is no persistence (code, files, memory, etc) between builds. Each build is 
given a max of 1GB RAM memory and 30-minute execution time limit. These settings 
are adjustable on per-account basic, so if there is a need in extra time or memory, 
please contact [support](/support).

Build environment runs under `magnum` user and supports passwordless sudo commands 
in cases when you need to install any additional packages with aptitude or similar tools. 
Build environment comes with packages required to compile software, so there is no need 
to install anything.

## Source Control

SCM packages are installed with python-software-properties:

- Git 1.8.5
- Mercurial 2.8.2
- Subversion 1.7.9

## Languages

Build environment might include the following language runtimes based on project
type.

### Ruby

Multiple Ruby versions are managed with `rvm` and are latest patchlevels:

- MRI 1.9.2
- MRI 1.9.3
- MRI 2.0.0 (*default*)
- MRI 2.1.0

### Node.js

Multiple Node.js versions are managed with `nvm`. Releases:

- 0.8
- 0.10 (*default*)
- 0.11

### Go

Multiple Go versions are managed with `gvm`. Releases:

- go1
- go1.0.3
- go1.1.2
- go1.2 (*default*)

## Databases

Each test VM has the following databases preinstalled:

- MySQL 5.5.x
- PostgreSQL 9.3.x
- MongoDB 2.4.x
- Redis 2.8.x
- Memcached 1.4.x
- ElasticSearch 0.90.x
- RabbitMQ 3.0.x
- CouchDB 1.2.x
- Beanstalk 1.9.x

## Headless Testing

- Xvfb
- Phantom.js 1.9.x
- Firefox 25.0

## Environment Variables

General variables:

- `USER=magnum`
- `HOME=/home/magnum`
- `LANG=en_US.UTF-8`
- `LC_ALL=en_US.UTF-8`
- `DEBIAN_FRONTEND=noninteractive`
- `RAILS_ENV=test`
- `RACK_ENV=test`
- `CI=true`
- `MAGNUM=true`

Build specific variables:

- `CI_NAME`         - CI worker name (Magnum)
- `CI_BRANCH`       - Commit branch name (master)
- `CI_COMMIT`       - Commit SHA
- `CI_BUILD_ID`     - The id of the currently running build
- `CI_BUILD_NUMBER` - Number of the currently running build
- `CI_BUILD_PATH`   - Path to project build
- `CI_BUILD_URL`    - Website build URL