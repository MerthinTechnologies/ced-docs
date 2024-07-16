# Add new build agent stack

Each build agent comes with a predefined stack of tools available for the compilation process. All build agents should include a compatible version of Node for the agent to run and can add any additional tools, runtimes, and frameworks to be available by default on that stack. These are the steps to create a new build agent stack.

## Create a docker repository in DockerHub

Create a private docker repository with the name `merthin/ced-build-agent-<stack-name>`; for instance, `merthin/ced-build-agent-dotnet7`.

## Create the dockerfile

Create a docker file [in this folder](../../agents/build-agent/dockerfiles/). Use `<stack-name>.dockerfile` as the filename; for instance, `dotnet7.dockerfile`. Make sure to include the latest supported version of Node for the build agent to run and add all the tools required for the new stack.

This is an example of a dockerfile for DotNet 7.

```dockerfile
FROM ubuntu:22.04
LABEL ced-agent-id="build-agent"
LABEL ced-agent-version="1.0.0.local-dev"
LABEL ced-environment="local-dev"

RUN apt update && apt upgrade -y

# Agent user and group
RUN groupadd agents
RUN useradd -m agent
RUN usermod -a -G agents agent

# Build agent runtime
RUN apt install -y ca-certificates curl gnupg
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key \
  | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
RUN echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_18.x nodistro main" \
     > /etc/apt/sources.list.d/nodesource.list
RUN apt update
RUN apt install nodejs -y
RUN chown -R root:agents /usr/lib/node_modules/
RUN chmod -R 775 /usr/lib/node_modules/

# Stack tools for DotNet 7
RUN apt install wget -y
RUN wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUN rm packages-microsoft-prod.deb
RUN apt update && apt install -y dotnet-sdk-7.0
# End of stack tools

# Pack the build agent
WORKDIR /usr/src/app
COPY . .
RUN npm install
RUN npm run build
RUN chmod -R 700 /usr/src/app

CMD [ "node", "./bin" ]
```

### Test image locally

Make sure to build and run the container image locally to test the installation process.

Build image locally:

```bash
cp ./dockerfiles/<stack-name>.dockerfile ./dockerfile
cp ~/.npmrc .
docker build . -t build-agent-<stack-name>
```

Run image locally and make sure it has everything needed for the stack:

```bash
docker run -it --rm build-agent-<stack-name> bash
```

## Add GitHub workflows for the build agent on each environment

Add a set of GitHub workflows for the new build agent in [this folder](../../.github/workflows/) with the following names:

- `build-agent-<stack-name>-dev.yml` for development.
- `build-agent-<stack-name>-exp.yml` for experimental.
- `build-agent-<stack-name>-prod.yml` for production.

You can use these workflows as reference and just change the parameters for workflow name, agent id, agent name, dockerfile name and docker repository.

- [build-agent-node18-dev.yml](../../.github/workflows/build-agent-node18-dev.yml) as a template for a development build agent.
- [build-agent-node18-exp.yml](../../.github/workflows/build-agent-node18-exp.yml) as a template for an experimental build agent.
- [build-agent-node18-prod.yml](../../.github/workflows/build-agent-node18-prod.yml) as a template for a production build agent.
