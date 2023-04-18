# Data Collection

Torizon VS Code Extension v2 (ApolloX) has opt-out telemetry collection. Only *anonymous data* is being collected.

## What's Included in the ApolloX Telemetry Data

- Template chosen during project creation;
- Host operation system version (only Kernel);
- Board Torizon version;
- Board machine;
- Error log during initialization;
- The user region;

This data is collected only during the creation of a new project and registration of a new device.

## How to Opt-in or Out

Use the `apollox.telemetry` setting to enable or disable the telemetry collection. By default the `apollox.telemetry` is set to `true`.

### Opt-Out

Use the command pallet and chose:

![alt](https://docs1.toradex.com/112193-6aed58946967db95a844f67e1a85e758b715064f.png?v=1)

Then add to the properties:

```json
    "apollox.telemetry": false,
```
