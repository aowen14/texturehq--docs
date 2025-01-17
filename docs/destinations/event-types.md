---
sidebar_position: 3
title: Event Types
---

# Event Types

_We are continually adding more event types as we build out the Texture platform so if there is an event type you would like to see, please let us know._

First some overall notes on the event types:

We follow the [Standard Webhook Specification](https://www.standardwebhooks.com/) as closely as possible for maximum compatibility with existing webhook integrations.

- All events are sent to the destination as a JSON object.
- All events have a `type` property that indicates the type of event.
- All events have a `version` property that indicates the version of the event type. We use semver for versioning.
- All events have a `key` property that is a unique identifier for the event. The `key` is a hash of the event data and is used to deduplicate events helping you avoid duplicate events.


## `command.failed`

Fired whenever a command run against a device fails.

```js title="Command Failed Event"
{
    "type": "command.failed",
    "version": "0.0.2",
    "key": "cc0e387d55ab78fb204c5c2225eff0aa6a9ca3f32a8d5542f75fe9b8bd972d87",
    "timestamp": "2024-08-22T15:54:52.013Z",
    "data": {
        "workspaceId": "cllzcf9xe00066g7dcsxyq1e5",
        "commandId": "cllzcbw0t00016g7dfua590dd",
        "deviceId": "cllzcbw0t00016g7dfua590dd",
        "error": {
            "message": "Failed to execute command"
        },
        "issuedAt": "2023-09-01T20:48:24.967Z",
        "executedAt": "2023-09-01T20:48:24.967Z"
    }
}
```


| Key | Description |
| --- | ----------- |
| type | The type of event, in this case `command.failed` |
| version | The version of the event type, following semver |
| key | A unique identifier for the event |
| timestamp | The date and time when the event occurred |
| data.workspaceId | The ID of the workspace associated with the command |
| data.commandId | The unique identifier for the command |
| data.deviceId | The ID of the device on which the command was executed |
| data.status | The status of the command, in this case "failed" |
| data.error.message | A description of the error that occurred |
| data.issuedAt | The date and time when the command was issued |
| data.executedAt | The date and time when the command was executed |


## `command.succeeded`

Fired whenever a command run against a device succeeds.

```js title="Command Succeeded Event"
{
    "type": "command.succeeded",
    "version": "0.0.2",
    "key": "cc0e387d55ab78fb204c5c2225eff0aa6a9ca3f32a8d5542f75fe9b8bd972d87",
    "timestamp": "2024-08-22T15:54:52.013Z",
    "data": {
        "workspaceId": "cllzcf9xe00066g7dcsxyq1e5",
        "commandId": "cllzcbw0t00016g7dfua590dd",
        "deviceId": "cllzcbw0t00016g7dfua590dd",
        "issuedAt": "2023-09-01T20:48:24.967Z",
        "executedAt": "2023-09-01T20:48:24.967Z"
    }
}
```


| Key | Description |
| --- | ----------- |
| type | The type of event, in this case `command.succeeded` |
| version | The version of the event type, following semver |
| key | A unique identifier for the event |
| timestamp | The date and time when the event occurred |
| data.workspaceId | The ID of the workspace associated with the command |
| data.commandId | The unique identifier for the command |
| data.deviceId | The ID of the device on which the command was executed |
| data.status | The status of the command, in this case "succeeded" |
| data.issuedAt | The date and time when the command was issued |
| data.executedAt | The date and time when the command was executed |

## `device.discovered`

Fired when a new device is connected to the Texture platform. Includes the following payload:

```js title="Device Discovered Event"
{
    "type": "device.discovered",
    "version": "0.0.1",
    "key": "cc0e387d55ab78fb204c5c2225eff0aa6a9ca3f32a8d5542f75fe9b8bd972d87",
    "timestamp": "2024-08-22T15:54:52.013Z",
    "data": {
        "deviceId": "cllzcbw0t00016g7dfua590dd",
        "deviceModel": "ac_powerwall",
        "deviceType": "battery",
        "workspaceId": "cllzcf9xe00066g7dcsxyq1e5",
        "organizationId": "cllzcf78o00036g7d0r4gjry1",
        "manufacturer": "tesla",
        "customer": {
            "referenceId": "c1b1504d-4784-5d90-9459-a512c4789b35",
        },
        "site": {
            "location": {
                "latitude": 37.7749,
                "longitude": -122.4194
            }
        },
        "state": {
            "id": "cltyhxpy406poq4z3zx19y2fs",
            "charge": 18069.15789473684,
            "chargePercentage": 59.30925587453832,
            "chargingState": "charging",
            "whConsumed": 0,
            "chargeRate": -2290,
            "backupReserve": 30,
            "gridStatus": "idle",
            "gridPower": 0,
            "gridEnergy": 0,
            "isStormModeEnabled": true,
            "isStormModeActive": false,
            "createdAt": "2024-03-19T14:55:10.493Z"
        },
        "createdAt": "2023-09-01T20:48:24.967Z",
        "updatedAt": "2023-09-01T20:48:24.967Z"
    }
}
```

| Key | Description |
| --- | ----------- |
| type | The type of event, in this case `device.discovered` |
| version | The version of the event schema, following semver |
| key | A unique identifier for this event instance |
| timestamp | The date and time when the event was generated |
| data.deviceId | The unique identifier for the device in Texture's system |
| data.deviceModel | The specific model of the device |
| data.deviceType | The category or type of the device (e.g., `battery`, `inverter`, `vehicle`, etc.) |
| data.workspaceId | The identifier for the workspace to which this device belongs |
| data.organizationId | The identifier for the organization to which this device belongs |
| data.manufacturer | The manufacturer of the device |
| data.customer.referenceId | An external reference ID for the customer |
| data.site.location.latitude | The latitude coordinate of the device's location |
| data.site.location.longitude | The longitude coordinate of the device's location |
| data.state | The current state of the device, including various metrics |
| data.state.id | Unique identifier for this state instance |
| data.state.charge | The current charge of the device in watt-hours |
| data.state.chargePercentage | The current charge level as a percentage |
| data.state.chargingState | The current charging status of the device |
| data.state.whConsumed | The watt-hours consumed by the device |
| data.state.chargeRate | The rate at which the device is charging or discharging |
| data.state.backupReserve | The percentage of charge reserved for backup |
| data.state.gridStatus | The current status of the grid connection |
| data.state.gridPower | The power currently drawn from or supplied to the grid |
| data.state.gridEnergy | The energy exchanged with the grid |
| data.state.createdAt | The timestamp when this state was recorded |
| data.createdAt | The timestamp when the device was first discovered |
| data.updatedAt | The timestamp when the device information was last updated |


_Note that when you configure a destination, you can specify which device types are fired for a given destination which can act as a kind of filter. So for example you could say that you want only Battery updates to go to a given webhook and we will filter them for you._

## `device.updated`

Fired whenever we get updated data for a device.

```js title="Device Updated Event"
{
    "type": "device.updated",
    "version": "0.0.1",
    "key": "cc0e387d55ab78fb204c5c2225eff0aa6a9ca3f32a8d5542f75fe9b8bd972d87",
    "timestamp": "2024-08-22T15:54:52.013Z",
    "data": {
        "deviceId": "cllzcbw0t00016g7dfua590dd",
        "deviceModel": "ac_powerwall",
        "deviceName": "Susie's Powerwall",
        "manufacturer": "tesla",
        "deviceType": "battery",
        "workspaceId": "cllzcf9xe00066g7dcsxyq1e5",
        "organizationId": "cllzcf78o00036g7d0r4gjry1",
        "customer": {
            "referenceId": "c1b1504d-4784-5d90-9459-a512c4789b35",
        },
        "state": {
            "id": "cm05mna4f00bn9dkcm5zylwt0",
            "charge": 5378,
            "chargePercentage": 20,
            "chargingState": "idle",
            "whConsumed": 0,
            "chargeRate": 0,
            "backupReserve": 20,
            "gridStatus": "importing",
            "gridPower": 201,
            "gridEnergy": 17,
            "isStormModeEnabled": true,
            "isStormModeActive": false
            "createdAt": "2024-08-22T18:39:38.479Z",
        },
        "createdAt": "2023-09-01T20:48:24.967Z",
        "updatedAt": "2023-09-01T20:48:24.967Z"
    }
}
```

The lion's share of these events will be triggered from the Device state updates which we get mostly on 5 or 15 minute intervals from the devices, however we are always looking to get tighter interval telemetry data as well as allow for specifying filters on that data. Stay tuned as we continue to add richer functionality to the filtering data to these events.

## `device.disconnected`

Fired whenever a device disconnects from the Texture platform.

```js title="Device Disconnected Event"
{
    "type": "device.disconnected",
    "version": "0.0.1",
    "key": "cc0e387d55ab78fb204c5c2225eff0aa6a9ca3f32a8d5542f75fe9b8bd972d87",
    "timestamp": "2024-08-22T15:54:52.013Z",
    "data": {
        "deviceId": "cllzcbw0t00016g7dfua590dd",
        "deviceModel": "ac_powerwall",
        "deviceType": "battery",
        "workspaceId": "cllzcf9xe00066g7dcsxyq1e5",
        "organizationId": "cllzcf78o00036g7d0r4gjry1",
        "manufacturer": "tesla",
        "customer": {
            "referenceId": "c1b1504d-4784-5d90-9459-a512c4789b35",
        },
        "site": {
            "location": {
                "latitude": 37.7749,
                "longitude": -122.4194
            }
        },
        "createdAt": "2023-09-01T20:48:24.967Z",
        "updatedAt": "2023-09-01T20:48:24.967Z"
    }
}
```

The following events are only available for organizations that have opted 
in to Grid Services. If you are interested in Grid Services, please reach out to us.

## `enrollment.approved`

Fired whenever an enrollment is approved.

```json
{
  "type": "enrollment.approved",
  "version": "0.0.1",
  "key": "8f7d3b2e1a9c6f4e0d5b8a7c2e1f3d5b8a7c2e1f3d5b8a7c2e1f3d5b8a7c2e1f",
  "timestamp": "2024-03-20T14:30:00Z",
  "data": {
    "workspaceId": "clm2n3o4p5q6r7s8t9u0v1w2x",
    "organizationId": "cla1b2c3d4e5f6g7h8i9j0k1l",
    "customer": {
      "referenceId": "cust-123456-abcdef"
    },
    "program": {
      "manager": "GridCo Energy Services"
    }
  }
}
```
