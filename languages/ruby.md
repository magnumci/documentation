# Ruby Projects

Build environment includes the following versions of Ruby:

- MRI 1.8.7 
- MRI 1.9.2
- MRI 1.9.3
- MRI 2.0.0 - *default*

Versions are managed with [RVM](https://rvm.io/). Magnum CI will use ruby
`2.0.0` by default, and if you want to use a different version, specify `ruby`
section in magnum config:

```
ruby: 1.9.3
```

Also, if your project is using `.rvmrc`, `.ruby-version` or `.rbenv-version` files,
defined version will be picked up automatically.

## Dependencies

Magnum CI will detect if project is using Bundler and execute command:

```
bundle install --path .
```

You can override bundler arguments with `bundler_args` in magnum config:

```
bundler_args: "--binstubs --production"
```

## Test Suite Execution

By default Magnum CI will try to execute `bundle exec rake test`. 

You can set your own steps in magnum config:

```
script:
  - "bundle exec ci:backend"
  - "bundle exec ci:frontend"
```

## Rails Applications

For rails application Magnum CI will discover environment using `Gemfile` and
execute the following steps:

- `bundle exec rake db:create`
- `bundle exec rake db:schema:load`

If RSpec is detected, worker will execute `bundle exec rspec spec/`. Otherwise,
it'll execute the default command: `bundle exec rake test`
