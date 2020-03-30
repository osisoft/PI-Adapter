---
uid: ScheduleConfiguration
---

# Schedule configuration

OSIsoft adapters can be configured to run scans based on a schedule. If the adapter supports scheduling, then each data item in the data selection configuration can be assigned a schedule. The adapter will then query for data for those data items at the scheduled time.

## Configure schedule

Complete the following procedure to change the logging configuration:

1. Using any text editor, create a file that contains the logging configuration in JSON form.
    - For content structure, see [Example](#example).
    - For all available parameters, see [Schedules parameters](#schedules-parameters).

2. Save the file, for example as *Component_Schedules.json*.

3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/<ComponentId>/Schedules`.

    **Note:**  Replace _&lt;ComponentId&gt;_ with the ComponentId of the adapter, for example _OpcUa1_.

    `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using curl (run this command from the same directory where the file is located):

    ```bash
    curl -d "@Component_Schedules.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/<ComponentId>/Schedules"
    ```

On successful execution, the schedules change takes effect immediately during runtime.

## Schedules schema

The full schema definition for the schedules configuration is in the component specific schedules file: _AdapterName_Schedules_schema.json_

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Schedules parameters

The following parameters are available for configuring logging:

| Parameter                | Required | Type      | Description |
| ------------------------ | -------- | --------- | ----------- |
|**Id**              | Required | `string` | Unique identifier for the schedule. |
|**Period** | Required | `string` | The data sampling rate of the schedule. Expected format is HH:MM:SS.###. |
|**Offset**     | Optional | `integer` | The offset from the midnight when the schedule starts. Expected format is HH:MM:SS.### |

## Example

```code
[
  {
    "Id": "schedule1",
    "Period": "00:00:01.500",
    "Offset": "00:02:03"
  }
]
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/_ComponentId_/Schedules      | GET       | Gets all configured schedules. |
| api/v1/configuration/system/Schedules      | DELETE    | Deletes all configured schedules. |
| api/v1/configuration/system/Schedules      | POST      | Adds an array of schedules or a single schedule. Fails if any schedule already exists. |
| api/v1/configuration/system/Schedules      | PUT       | Replaces all schedules. |
| api/v1/configuration/system/Schedules/*id* | GET       | Gets configured schedule by *id*. |
| api/v1/configuration/system/Schedules/*id*| DELETE     | Deletes configured schedule by *id*. |
| api/v1/configuration/system/Schedules/*id* | PUT       | Replaces schedule by *id*. Fails if schedule does not exist. |
| api/v1/configuration/system/Schedules/*id* | PATCH     | Allows partial updating of configured schedule by *id*. |

**Note:** Replace *ComponentId* with the Id of your adapter component, for example Modbus1 or OpcUa1.
