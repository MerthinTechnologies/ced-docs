# Configure your source files to target a CED subsystem

This will allow you to connect your source files with CED, so they can be pushed to a subsystem for compilation and deployment.

## Create ced.json file

You need only one file to configure your project as a CED subsystem, that's the `ced.json` file.

First, step into your project's folder and run:

```bash
$ ced init
```

This will guide you through the steps to set the target subsystem. You need to provide the project id, the default environment and the subsystem id. Example:

```bash
$ ced init
  √ Project Id:  · roku-example
  Setting project Roku Example

  √ Default envrironment:  · development
  Setting environment development

  √ Subsystem Id:  · roku-media-api
  Setting subsystem Roku Media Api

  Project initialized
```

It will create a basic `ced.json` file with the following content:

```json
{
  "projectId": "roku-example",
  "defaultEnvironment": "development",
  "subsystemId": "roku-media-api",
  "config": {
    "path": "configuration.json",
    "format": "json"
  },
  "build": {
    "steps": [
      {
        "name": "Build",
        "command": "echo \"Build\""
      }
    ],
    "artifact": "./bin"
  }
}
```

## Set the configuration file for your project

CED will generate your project's configuration based on how the subsystem interacts with other subsystems through the discoverability service. Change the `config` section in `ced.json` to set the path and name of the configuration file and its format. For instance, you could use something like this to generate a configuration file under `src/services/` with `esModule` format.

```json
"config": {
  "path": "src/services/configuration.ts",
  "format": "esModule"
},
```

Available formats are `json`, `esModule` and `dotEnv`.

## Generate the configuration for local development

Run this command to generate the configuration for local development. CED will use the default environment to generate the local development configuration.

```bash
$ ced config:generate --localDev
```

Make sure to run this command whenever you change your ecosystem in CED.

From this point your code can reference this configuration file. CED will update it's content on every build based on the environment ecosystem.

## Set the build steps

Use the `build` section in the `ced.json` file to describe how this folder should be built by CED.

```json
"build": {
  "steps": [
    {
      "name": "Install",
      "command": "npm install"
    },
    {
      "name": "Build",
      "command": "npm run build"
    }
  ],
  "artifact": "./dist"
}
```

In this case we're describing two steps, one for dependency installation and other for building the project. Make sure to change `artifact` with the output folder of the compilation. This folder will be uploaded as the version's artifact for deployment.

## Ignore files

There are some files you don't want to push to CED, like dependencies folder and compilation output. Create a file `.cedignore` in the same folder as the `ced.json` file to define what to exclude. If you don't know what to exclude, you could use your `.gitignore` as a reference.

## Push source files to CED

Run the following command in the same folder where `ced.json` is. This will push source files to CED for compilation and deployment.

```bash
$ ced push:source
```

## Next

Check [this tutorial](./connect-github-repository-with-a-ced-subsystem.md) to automatically push your source files from a GitHub repository to a subsystem in CED.
