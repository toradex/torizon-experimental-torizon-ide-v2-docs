# Torizon VS Code Extension v2 (ApolloX)

From feedback and past experience, we have redesigned the Torizon Extensions, from scratch, to add usability improvements for containerized application development.

## Getting Started

> ⚠️ For the extension to work correctly, it is necessary to have the following ports accessible between your computer and the development board:
> 
> - **2375** (Docker API)
> 
> - **5000** (Local Docker Registry)
> 
> - **2222** (Container SSH Connection)
> 
> - **22** (Dev Board SSH Connection)

### Install Prerequisites Dependencies

- Linux or WSL 2 (Debian or Ubuntu)

- [gnupg](https://packages.debian.org/bullseye/gnupg)

- [Docker Engine](https://docs.docker.com/engine/install/)

- [Docker Compose](https://docs.docker.com/compose/install/)

- [Visual Studio Code](https://code.visualstudio.com/)
  
  - > ⚠️ For WSL 2 it should be installed on Windows Side

### Installing

In VS Code select `Extensions` from the activity bar and search for `toradex.apollox-vscode`:

![](https://docs1.toradex.com/111419-apollox_gs.gif)

After the extension installation a new icon will be shown in the activity bar, select it for activate the extension. During the first activation some checks are run to verify dependencies. If any installable dependency is detected, an installation attempt will be performed and your `sudo` user password will be requested for each of the dependencies:

![](https://docs.toradex.com/111425-ezgif-3-dcb901bf1f.gif)

### Torizon Device Registering

For use of the Torizon integrated development environment features a device with [Torizon OS](https://www.toradex.com/operating-systems/torizon-core) must be registered to be used with the extension. Select the Torizon icon in the activity bar to scan for devices in your local network:

![](https://docs.toradex.com/111426-ezgif-3-39e3466b43.gif?v=2)

Also is possible to rescan the devices clicking in the `Refresh Devices` icon:

![](https://docs.toradex.com/111427-ezgif-3-90981cc5e4.gif)

After the scan, expand the device to registry and click on `Connect`, input the device `user` and `password`:

![](https://docs.toradex.com/111428-ezgif-3-a32b08de74.gif)

After the connection the device will be listed under `CONNECTED DEVICES`.

### Setting a Torizon Device as Default

Multiple Torizon devices can be registered. To use the Torizon integrated development environment features a device must be selected as default. Expand a connected device and click on `Set Default`:

![](https://docs.toradex.com/111429-ezgif-3-48255510dd.gif?v=2)

The default device will be used as target for the remote deploy, remote debug.

Also the default device will be used as context for the [Docker VS Code extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker):

![](https://docs.toradex.com/111430-ezgif-3-4cc12cf3bd.gif)

The management of the Torizon default device Docker containers, images, volumes and networks can all be used by the Docker VS Code extension.

> ⚠️ If during the first connection from the Torizon default device the VS Code Docker extension shows a `Failed to connect` warning. Click on the `Refresh` icon to try again.

To differentiate between the registered devices and default device, the icon changes to:

![](https://docs.toradex.com/111431-apolloxdefaultselected.png)

### Creating a new Single Container Project

Open a new VS Code window and select the `Explorer` on activity bar. There will be two buttons for creating Projects. Click on `New Torizon Project`:

![](https://docs.toradex.com/111445-ezgif-2-6e7d09550d.gif)

A new tab will be opened with a list of templates that can be used for the project creation. Click on the image describing the template to create a new project based on it:

![](https://docs.toradex.com/111446-ezgif-2-584b355b72.gif)

> ⚠️ The templates shown in this documentation image are still in preview. Other templates can be added or removed without prior notice.

Input the project `Name`, project `Container name (docker-compose service)`, choose a system folder on `Creation path` to store the new project files and click on `Create Project` button:

![](https://docs.toradex.com/111447-ezgif-2-4dd51c86a4.gif)

This will trigger the create project task with the user inputs. A new output tab will be show with the project creation progress:

![](https://docs.toradex.com/111448-ezgif-2-2d4294cf8e.gif)

At end, if everything went as expected, the VS Code window will reload using the new created project as default workspace:

![](https://docs.toradex.com/111451-ezgif-2-4966529dac.gif)

In the first load of a new project a notification `Do you want to check for dependencies on your system?` is shown. Choose yes, this will run a check for the packages that are needed, template based, (as SDK for example) to build the project. Also it's try to install the packages that are not found.

> ⚠️During the first load of a new project some extra tasks are triggered:
> 
> - `run-torizon-binfmt`: run the `torizon/binfmt` Docker image to registry foreign architecture interpreters (we need this to build containers for `arm` architecture);
> 
> - `run-docker-registry`: run a local Docker registry to be used to exchange images between development PC and the target board;
> 
> - `run-share-wsl-ports`: this task is specific for **Windows** users (that need to use WSL 2). By default the services created on a WSL 2 distro does not been visible to the external network. This task run a PowerShell script on the Windows side (**as administrator**) binding the ports between WSL 2 and Windows that are needed to be accessible from the target board;
> 
> - `check-deps`: this task run a check for the packages that are needed (as SDK for example) to build the project. Also it's try to install the packages that are not found;

> ⚠️ **FOR WINDOWS (WSL 2) USERS ONLY**
> 
> As previously said, the `run-share-wsl-ports`, runs a PowerShell script as administrator on Windows side. This needs user confirmation, so an `User Account Control` window will be shown:
> 
> ![](https://docs.toradex.com/111449-apolloxuac.png)
> 
> Click `Yes`. After the confirmation a new empty terminal will be shown (it's normal do not close it):
> 
> ![](https://docs.toradex.com/111450-apolloxpwshwindows11.png)
> 
> The terminal will run the script and will be closed automatically.

### Remote Debug

To build the project and remote deploy it on the target board and make a remote debug session, with a new project loaded, add a breakpoint to the code, select `Run and Debug` from the activity bar and select the target board Torizon architecture. With this done, click on the `play` icon (or press `F5` keyboard key) to start a new remote debug session:

![](https://docs.toradex.com/111452-code_2yv89pxwtd.gif)

> ⚠️The first time the debug is run it may take some time to start the debug session. This task has several automated steps, your application will be compiled for the selected architecture, a new docker image will be built, delivered to the target (the default device), the image will be initialized on the target and then connected to the VS Code debugger.

> ⚠️ Once the user selects the Torizon architecture in the `Run and Debug` combo box, VS Code will use this same option for the next sessions, not having to select it again. So, the user can start a new debug session just by pressing `F5` key.

### Build and Release Docker Image

To generate an image for production, ready to be deployed using the Torizon Platform OTA, select `TASK RUNNER` and click on `create-production-image`. This task needs some inputs, the container registry user name (the [Dockerhub](https://hub.docker.com/) user name for example), the image tag (to differentiate versions for example), select the architecture of the target card (`arm` for arm 32 bit and `arm64` for arm 64 bit) and finally the password to be used in conjunction with the registry user name (to push the image):

![](https://docs.toradex.com/111454-code_ugpf9n26ge.gif)

If everything ran as expected, a `✅ docker-compose.prod.yml created` message will be displayed at the end. The `docker-compose.prod.yml` file can be used as input for a new `Upload Docker Compose Package` on [Torizon Platform](https://app.torizon.io/) update system.

> ⚠️The first time the `create-production-image` is run it may take some time. This task has several automated steps, your application will be compiled for the selected architecture, a new docker image will be built for release production, the image will be push to the Docker registry and a `docker-compose.prod.yml` will be created on the root of the project workspace.
