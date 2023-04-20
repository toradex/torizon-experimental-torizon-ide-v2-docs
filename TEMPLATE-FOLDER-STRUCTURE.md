# Project Workspace Structure

Some files and folders are created by the extension and are used to manage the project. This section describes the workspace structure and the files that are created by the extension.

## 📂 .conf

### 📄 .container

This file is used to store the container (docker-compose service) name. It's useful when the project needs to be updated and the updater needs to auto complete the container name. It's read by the `projectUpdater.ps1` script.

### 📄 .template

This file is used to store the template name. It's useful when the project needs to be updated and the updater needs to know which template to use.

### 📜 checkDeps.ps1

This file is used to check if the dependencies are installed on the machine, based in the `deps.json` file. It's used by the `check-deps` task.

### 📜 createDockerComposeProduction.ps1

This file is used to create the production Docker images and merge it on the `docker-compose.production.yml` file. It's used by the `create-production-image` task.

### 📄 deps.json

This file is used to store the Debian packages dependencies that are required to run the project locally. It's read by the `checkDeps.ps1` script.

### 🗝️ id_rsa / id_rsa.pub

This files are used to store the SSH key pair used to access the development container in the target board.

> ⚠️ These are not secure keys!! They are only used to access the development container in the target board. Do not use these keys for any other purpose.

### 📜 projectUpdater.ps1

This file is used to update the project to the latest version of the template. It's used by the `try-update-template` task.

### 📜 runContainerIfNotExists.ps1

This file is used to run the dependency containers if they are not running. It's used by the `run-torizon-binfmt` and `run-docker-registry` tasks.

### 📜 shareWSLPorts.ps1

This file is used to open the firewall from the Windows side and be possible to access the WSL ports from the target device. It's used by the `run-share-wsl-ports` task.

> ⚠️ Although this script runs always when the extension is activated, it's only execute the actual content if in a WSL 2 environment.

### 📜 tcb-env-setup.sh

This file is used to setup the TorizonCore Builder. It's used by the `tcb-platform-publish` task.

> ⚠️ This script is not the same as the one in the [TorizonCore Builder](https://developer.toradex.com/torizon/os-customization/torizoncore-builder-tool-customizing-torizoncore-images/) documentation. It's a modified version that is used by the extension.

### 📜 torizonIO.ps1

This file is used to manage the Torizon Platform API. It's used by the `platform-update-fleet` task.

### 📜 torizonPackages.ps1

This file is used to add the packages described in the `torizonPackages.json` file to the `Dockerfile` and `Dockerfile.debug` files.

### 📄 update.json

This file is used to store the update match table of the files that needs to be changed the name. It's read by the `projectUpdater.ps1` script.

## 📂 .github/workflows

### 📄 build-application.yaml

This file is used to configure the GitHub Actions workflow to build and deploy the application to the Torizon IO platform. Check the [Github Actions Integration](./GITHUB-ACTIONS.md) documentation for more information.

## 📂 .vscode

### 📄 extensions.json

This file is used to store the extensions that are recommended by the project to work correctly. For example, the extension that runs the debugger, the code syntax highlight, etc. It's used by the VS Code to ask the user to install the recommended extensions.

### 📄 launch.json

This file is used to store the configurations to launch the application with the debugger. It's used by the VS Code to list and launch the application debuggers.

### 📄 settings.json

This file is used to store the settings of the project. It's used by the VS Code and the ApolloX extension to set the project settings. Check the [Workspace Settings](./WORKSPACE-SETTINGS.md) documentation for more information.

### 📄 tasks.json

This file is used to store the tasks that are available to run on the project. It's used by the VS Code to list and run the project tasks. These tasks are also used by the `launch.json` in a dependency chain of tasks to build and deploy the application on the target before the launch of the debugger. Check the [Workspace Tasks](./WORKSPACE-TASKS.md) documentation for more information.

### 📜 tasks.ps1

This file is used to run the tasks described in the `tasks.json` file on the CLI and CI/CD environments. Check the [Using Project Tasks in CLI](./USING-PROJECT-TASKS-IN-CLI.md) documentation for more information.

## 📄 .dockerignore

This file is used to list files and folders to ignore when building the Docker image.

## 📄 .gitignore

This file is used to list files and folders to ignore when committing the project to a Git repository.

> ⚠️ This is a started point for your project. The list of files and folders to ignore may change depending on your project. So, pay attention when adding files and folders to the repository and add them to `.gitignore` if necessary.
> ⚠️ Make sure to maintain the `credentials.zip` and the `*.lock.yml` files on the `.gitignore`. `credentials.zip` should not be public shared by security reasons and the `*.lock.yml` files are generated by TorizonCore Builder.

## 📄 .gitlab-ci.yml

This file is used to configure the GitLab CI pipeline. Check the [GitLab CI Integration](./GITLAB-CI.md) documentation for more information.

## 📄 docker-compose.yml

This file is used to configure the Docker Compose services, build parameters, port forwarding, devices, capabilities for the production and debug containers. Check the [Compose file reference](https://docs.docker.com/compose/compose-file/) documentation for more information.

## 📄 Dockerfile

This file is used to configure the Docker image that will be used to build the production image. Check the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) documentation for more information.

## 📄 Dockerfile.debug

This file is used to configure the Docker image that will be used to build the debug image. Check the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) documentation for more information.

## 📄 torizonPackages.json

This file is used to list the Debian packages that will be installed on the production and debug containers. Check the [Debian Torizon Packages](./DEBIAN-TORIZON-PACKAGES.md) documentation for more information.
