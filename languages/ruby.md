# Ruby Projects

Magnum CI build environment includes the following versions of Ruby:

- MRI 1.9.2
- MRI 1.9.3
- MRI 2.0.0 - **default**
- MRI 2.1.0

Multiple ruby versions are managed with [RVM](https://rvm.io/). Magnum CI will use
`2.0.0` version by default, and if you want to use a different version, specify `ruby`
section in magnum config:

```
ruby: 1.9.3
```

You can also switch ruby runtime version using build configuration interface.

Projects using `.rvmrc`, `.ruby-version` or `.rbenv-version` files will automatically
detect and switch ruby version to the specified. RVM `.ruby-gemset` is ignored.

## Installing dependencies

For project using [Bundler](http://bundler.io/) build runner will automatically install
dependencies by running the following command:

```
bundle install --path .
```

You can override bundler arguments with `bundler_args` in magnum config:

```
bundler_args: "--binstubs --production"
```

If cases where you need to specify your own dependency installation steps,
you can add section `install` into magnum config (or use configuration interface):

```
install:
  - "sudo apt-get install -y utility"
  - "bundle install --path ~/bundle --without mysql"
```

## Running test suite

By default Magnum CI will try to execute the following command:

```
bundle exec rake test
```

You can set your own steps in magnum config (or use configuration interface):

```
script:
  - "bundle exec ci:backend"
  - "bundle exec ci:frontend"
```

## Example config

Here's the example config for ruby applications:

```
before_install: 
  - "sudo apt-get update"
  - "sudo apt-get install myutility"

install:
  - "bundle install --path ."

before_script:
  - "cp config/service.yml.sample config/service.yml"
  - "bundle exec rake service:setup"

script:
  - "bundle exec rake spec/"
  - "bundle exec rake benchmark"

after_script:
  - "bundle exec rake archive"
```

## Rails Applications

Magnum CI will automatically attempt to discover application environment from 
your project's `Gemfile`. All necessary services (Redis, ElasticSearch, etc) will be 
automatically started if their respective client libraries are loaded.

Database preparation steps:

```
bundle exec rake db:create
bundle exec rake db:schema:load
```

Test suite execution defaults to RSpec framework:

```
bundle exec rspec spec/
```

If you dont use RSpec it'll default to Test::Unit framework:

```
bundle exec rake test
```