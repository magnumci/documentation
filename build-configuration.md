# Build Configuration

By default Magnum CI will try to detect application environment by analyzing the 
application structure and dependencies (libraries, databases). To override default
build execution settings and steps, you can define a `.magnum.yml` file under the
project root. This configuration file will be used to run commands that are required
to perform the build. Configuration file is a simple YAML-formatted file.

Build process is split into steps:

- `before_install` - Commands to execute before main installation script
- `install` - Command to execute project dependencies installation
- `before_script` - Commands to execute before running the test suite
- `script` - Commands to execute the main test suite
- `after_script` - Commands to execute when test suite execution is complete

Commands defined in each section (except `after_script`) should return exit code = 0, 
otherwise the build process will be terminated and marked as failed. 

Each specified command will be executed in shell. You can pass as many commands as you want.

Single command:

```yaml
before_script: bundle install
```

Multiple commands:

```yaml
before_script:
  - bundle install --path .bundle
  - npm install
```

Extended example:

```yaml
before_install:
  - sudo apt-get install my-fancy-package

install:
  - bundle install --path .bundle --binstubs
  - npm install

before_script:
  - /etc/init.d/xvfb start

script:
  - bundle exec rspec spec/

after_script:
  - rm testfile
```

### Language versions

Configuration file allows to set a specific language version you'd like to use
on the project. 


For ruby:

```yaml
ruby: 2.0.0
```

For Node.js:

```yaml
node: 0.10.0
```

For Go:

```yaml
go: 1.0.3
```

## System Services

Build image includes a set of services that are started automatically:

- PostgreSQL
- MySQL
- MongoDB

Services that are not started automatically:

- Redis
- Memcached
- ElasticSearch
- Xvfb

You can define a `services` section of the config like that:

```yaml
services:
  - redis-server
  - memcached
  - xvfb
```

And they'll be started before the test execution starts.

As an alternative to `services` section, you can use `before_install` :

```yaml
before_install:
  - sudo /etc/init.d/redis-server start
```

### Ruby Projects

Since most of ruby projects are using bundler to manage dependencies, Magnum CI
build system does automatic discovery of whats being used in application. Supported 
services:

- Redis
- Memcached
