# Link local CLI extensions with CLI

This tutorial will guide you through the process of linking local CLI extensions to work with CED CLI. This guide will use as example the CLI extension: ced-cli-extensions-management

## Prerequisites

[Install CLI](install-cli.md) and follow that tutorial before trying to follow this guide.

## Build the extension desired

From the root folder:

```bash
$ cd ./libs/cli-extensions/ced-cli-extensions-management
$ npm install
$ npm run build
```

## Link CLI to use local extension

For Windows

```bash
$ npm link
```

For Mac

```bash
$ sudo npm link
```

## Test to make sure everything was done correctly

In system terminal type the following code.

```bash
$ npm ls --depth 0 -g
```

The process worked if the extension points to a local file directory.

## Creating feedback loop

With VScode open the root folder of the extension desired.

Press ⌘ + ⇧ + B (for Mac) or run command "Task: Run Build Task" and select the task "tsc: watch - tsconfig.json".

Now, any changes will be reflected in the CLI everytime you save in the extension file.
