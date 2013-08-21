# Go Projects

Build environment includes the following Go versions:

- Go 1.0 - *default*
- Go 1.0.3

Go versions are installed and managed with [GVM](https://github.com/moovweb/gvm).
Worker will use `1.0` version by default, and if you want to use a different 
version, you can define it using build settings or in `.magnum.yml` config:

```
go: 1.0.3
```

## Dependencies

Default command to install dependencies and build application:

```
go get -d -v ./...
go build -v ./...
```

To override, use `install` section of the config:

```
go: 1.0.3
install:
  - go get package1
  - go get package2
```

## Test Suite

Default command to execute go test suite:

```
go test -v ./...
```

To override, use `script` section of the config:

```
script:
  - go run script.go
```