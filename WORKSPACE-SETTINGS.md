# Workspace Settings

The Torizon VS Code Extension v2 (ApolloX) provides a set of workspace settings that can be configured to customize the behavior of the extension. These settings are available in the `settings.json` file in the `.vscode` folder of the workspace.

## ApolloX properties

### `apollox.telemetry`

A boolean that enables or disables the telemetry collection. The telemetry is used to improve the extension and the templates. See [Data Collection](./USAGE-DATA.md) for more information.

### `apollox.templatesBranch`

A string that contains the branch to use for get the templates. For TorizonCore 5.0 projects set it to `bullseye`, for TorizonCore 6.0 project set it to `bookworm`. `bookworm` is the default value.

### `apollox.experimental`

A boolean that enables or disables the experimental features. The experimental features are not stable and can be changed or removed in the future.

### `apollox.debianRelease`

A string that contains the Debian release to use for torizon packages integration. See [Debian Torizon Packages](./DEBIAN-TORIZON-PACKAGES.md) for more information.

## Torizon Project Properties

### `torizon_psswd`

 A string that contains the password of the default debug Torizon device login. This property is used by the extension to connect to the Torizon device trough SSH. It's value depend on default device selected, and should set automatically by the extension.

### `torizon_login`

  A string that contains the login of the default debug Torizon device. This property is used by the extension to connect to the Torizon device trough SSH. It's value depend on default device selected, and should set automatically by the extension.

### `torizon_ip`

 A string that contains the IP address of the default debug Torizon device. This property is used by the extension to connect to the Torizon device trough SSH. It's value depend on default device selected, and should set automatically by the extension.

### `host_ip`

  A string that contains the IP address of the host development machine. This property is used by the extension to share the namespace domain of the local Docker registry with the Torizon device. It's value should set automatically by the extension.

### `torizon_workspace`
  
  A string that contains the path of the current workspace folder. This is used by the multi-container project mechanism (multi-container projects are experimental).

### `torizon_debug_port`
  
  A string that contains the main port used by the debug image forward it to the Torizon device. It's value depend on the development stack used and the port that the debugger is using.

### `torizon_debug_port2`
  
  A string that contains the secondary port used by the debug image forward it to the Torizon device. It's value depend on the development stack used, some stacks use two ports for different debug data to be shared.

### `torizon_debug_port3`
  
  A string that contains the third port used by the debug image forward it to the Torizon device. It's value depend on the development stack used, some stacks use three ports for different debug data to be shared.

### `torizon_debug_ssh_port`

  A string that contains the port used by the debug image to forward the SSH connection to the Torizon device.

### `torizon_gpu`
  
  A string that contains the GPU device prefix used by the extension to append it to the right Docker image base to be used. It's value depend on default device selected, and should set automatically by the extension.

### `torizon_arch`
  
  A string that contains the architecture of the default debug Torizon device. This property is used by the extension to build the application and the container to the right device architecture. It's value depend on default device selected, and should set automatically by the extension.

### `wait_sync`
  
  A string that contains the time in seconds that the extension will wait for the synchronization of the tasks execution between multi container projects. It's value depend on the number of containers that the project has (Multi-container projects are experimental).

### `torizon_run_as`
  
  A string that contains the user that the extension will use to run the application inside the container. It's value only takes effect in the debug container. It's useful when the application needs to run as root, the default user is `torizon`.

### `torizon_app_root`
  
  A string that contains the path of the application root folder inside the container. It's value only takes effect in the debug container. It's value normally is the `$HOME` folder of the user that the application is running. Make sure to set this property to the right value if the application is not running as `torizon` user.

## Docker properties

### `docker_registry`

A string that contains the Docker namespace of the DockerHub that will be used to push the production container image. This property is ask to the user during the first run of the `Create Production Docker Image` task and is stored. This value is used in the next runs of the task.

### `docker_tag`

A string that contains the tag of the production container image. This property is ask to the user during the first run of the `Create Production Docker Image` task and is stored. This value is used in the next runs of the task.

As the value is not ask to the user in the next runs of the task, if you want to change the tag, you can manually set this property in the `settings.json` file.

### `docker_login`

It is set by the extension when the user is asked for the DockerHub login during the first run of the `Create Production Docker Image` task. This value will used also to set the Docker image name, `${docker_login}/${project_name}:${docker_tag}`.

### `docker_password`

> ⚠️ This property was not designed to be set manually

It is set by the extension when the user is asked for the DockerHub password during the first run of the `Create Production Docker Image` task. The value `secret` means that the real value is stored in the VS Code vault. This property value is ask to the user during the first run of the `Create Production Docker Image` task and is stored. The value then is used in the next runs of the task. If you want to change the password, you can remove the property or set it to an empty string, then the extension will ask for the password again in the next run of the task.

## TorizonCore Builder Properties

Some properties are automatically set by the extension but are used from our companion extension [TorizonCore Builder](https://marketplace.visualstudio.com/items?itemName=Toradex.tcb-vscode). These properties are:

### `tcb.packageName`

A string that contains the name of the package that will be created in the Torizon IO platform after the TorizonCore Builder push. This property is set during the run of the `tcb-platform-publish` task.

### `tcb.version`

A string that contains the version of the TorizonCore builder to be used by the tasks. Check [TorizonCore Builder tags](https://hub.docker.com/r/torizon/torizoncore-builder/tags) for check the valid values.

### `tcb.fleetName`

A string that contains the name of the fleet that will be updated in the Torizon IO platform at the end of the CI/CD pipelines.
