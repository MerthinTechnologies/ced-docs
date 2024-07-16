# Install and uninstall extensions

To work with CED extensions you'll need to install the extensions management commands. Make sure to have the CED CLI already installed as described [here](./install-cli.md).

## Install extensions management commands

These commands aren't available to the CED CLI by default. You'll need to install a CLI extension package.

```
npm install -g @ced/cli-extensions-management
```

Run the CLI and you should be able to see new commands like:

```
ext:list [options] <type>
ext:install <sourceUrl>
ext:uninstall [options] <type>
```

## Install

Use this command to install extensions. Make sure to be familiar with [Extension Sources](../glossary/ExtensionsSource.md).

```
ced ext:install <sourceUrl>
```

## Uninstall

```
ced ext:uninstall [options] <type>
```
