# Connect a GitHub repository with a CED subsystem

This tutorial will guide you through the steps to deploy a folder from a GitHub repository to a CED subsystem.

The folder with source files should have already been configured to target a CED subsystem. Follow [these instructions](./configure-your-source-files-to-target-a-ced-subsystem.md) to configure a folder as a CED subsystem.

## Create a CLI token for automation

Use this command to generate an automation CLI token.

```bash
$ ced login --ci <token-name>
```

Make sure to name the token in a way that reveals its purpose, for instance:

```bash
$ ced login --ci GitHubAutomation
```

This will return a new token after opening an authentication link in the browser. Copy that token, we'll use it later, and make sure not to expose it, it can be used to access CED with your identity.

```bash
Opened a link in your default browser: https://www.cloudedgedistribution.com/cli-login?request-token=gx3wsuef4RwNtE1dwbdQPtq7mexxfopHTDfqVHi4WAPzAnwwzdrUUqNackbYvyWrDFQaT7A9q0pPiOMVtL5tzulBEMcHU3mnrXkA&named-token=GitHubAutomation
Please continue in your browser.
+ Login completed

  Token: dqwRJx0vKAdRt3hO5xDmF7zfwXPR35OtujKSeKPB6TxejALbiUXvUgxXZBt0Nbxgk2dWg95WNsbrbfapcj9eFzTtSFr31D9W6wTs
```

## Set the token as a secret in the GitHub repository

Create a secret in your GitHub repositoy, name it `CED_CLI_TOKEN` and set it with the token from the step above.

## Create a GitHub workflow for your subsystem

Create GitHub workflow under `.github/workflows/` folder. It's a good idea to name it the same as your subsystem id, for instance: `my-app.yml`. For monorepos tt makes sense to have multiple GitHub workflows targeting multiple subsystems in CED. Use this content as a reference for your workflow:

```yaml
name: My App

env:
  CED_ENVIRONMENT: development
  CED_PROJECT_PATH: project-folder
  CED_CLI_TOKEN: ${{secrets.CED_CLI_TOKEN}}

on:
  push:
    branches:
      - master
    paths:
      - 'project-folder/**'

jobs:
  push-to-ced:
    runs-on: ubuntu-latest
    timeout-minutes: 20
    steps:
      - uses: actions/checkout@v2
      - uses: MerthinTechnologies/push-ced-source-action@v1
```

Let's move step by step through the content.

```yaml
name: My App
```

First we set the name of the workflow. It's a good idea to name it after your subsystem.

```yaml
env:
  CED_ENVIRONMENT: development
  CED_PROJECT_PATH: project-folder
  CED_CLI_TOKEN: ${{secrets.CED_CLI_TOKEN}}
```

We create some variables for the workflow. Set `CED_ENVIRONMENT` with the CED environment you want to target. Use `CED_PROJECT_PATH` to specify the path of the project within the repository, you could use a folder for monorepos or `./` if you want to push the whole repository to the subsystem. In any case, this folder should contain the `ced.json` file. The variable `CED_CLI_TOKEN` uses the secret we created above.

You don't need to specify the target subsystem id because that's already in the `ced.json` file.

```yaml
on:
  push:
    branches:
      - master
    paths:
      - 'project-folder/**'
```

Next we define the trigger event. In this case we're triggering the workflow whenever something gets pushed to `master` branch with changes within the `project-folder` path. You could change `master` with your integration branch and make sure the triggering path matches with the `CED_PROJECT_PATH` variable defined above.

```yaml
jobs:
  push-to-ced:
    runs-on: ubuntu-latest
    timeout-minutes: 20
    steps:
      - uses: actions/checkout@v2
      - uses: MerthinTechnologies/push-ced-source-action@v1
```

Finally, we define the actual steps to push source files from GitHub to CED. We're using a custom GitHub action that can be found [here](https://github.com/MerthinTechnologies/push-ced-source-action).

With this configuration your project in a GitHub repository will automatically be pushed to a CED subsystem whenever something gets pushed to the integration branch.
