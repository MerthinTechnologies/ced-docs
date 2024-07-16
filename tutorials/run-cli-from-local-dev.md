# Run CLI from local development environment

This will guide you through the steps to run a local build of the CLI.

## Build and run the core-api locally

You need to run the core-api locally so it can serve the CLI. Run from the root folder:

```bash
$ cd ./backend/core-api
$ npm install
$ npm run build
$ npm run start
```

## Build and run the SPA locally

You need to run the SPA if you need to login with your local build of the CLI. Run from the root folder:

```bash
$ cd ./spa
$ npm install
$ npm run start
```

## Build CLI

Run from the root folder:

```bash
$ cd ./cli
$ npm install
$ npm run build
```

## Run commands from local CLI

Run this from the CLI folder in order to execute commands from the local CLI.

```bash
$ node ./lib/bin.js <command>
```

Example:

```bash
$ node ./lib/bin.js session
```
