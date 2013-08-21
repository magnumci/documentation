# Node.js Projects

Build environment includes the following Node.js versions:

- 0.6
- 0.8 - *default*
- 0.9
- 0.10
- 0.11

Node.js versions are installed and managed with [NVM](https://github.com/creationix/nvm).
Worker will use latest `0.10` version by default, and if you want to use a different
version, you can define it using build settings or in `.magnum.yml` config:

```
node_js: 0.11
```

## Dependencies

Magnum CI will detect if your application is using `package.json` and then
install dependencies with command:

```
npm install
```

To override, use `install` section of the config:

```
node_js: 0.10
install:
  - npm install package1
  - npm install package2
```

## Test Suite Execution

Default command to execute node.js test suite with `npm`:

```
npm test
```

To override, use `script` section of the config:

```
script:
  - command 1
  - command 2
```