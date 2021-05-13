---
uid: SchedulesConfiguration
---

# Schedules

Complete the following steps to configure schedules. Use the `PUT` method in conjunction with the `http://localhost:5590/api/v1/configuration/<ComponentId>/Schedules` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for schedules into the file.

    For sample JSON, see [Example](#example).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Schedules parameters](#schedules-parameters).

4. Save the file. For example, as `ConfigureSchedules.json`.

5. Open a command line session. Change directory to the location of `ConfigureSchedules.json`.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the schedules configuration.

    ```bash
    curl -d "@ConfigureSchedules.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/<ComponentId>/Schedules"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * For a list of other REST operations you can perform, like updating or replacing a schedules configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

On successful execution, the schedules change takes effect immediately during runtime.

## Schedules schema

The full schema definition for the schedules configuration is in the  `AdapterName_Schedules_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\<AdapterName>\Schemas`

Linux: `/opt/OSIsoft/Adapters/<AdapterName>/Schemas`

## Schedules parameters

The following parameters are available for configuring schedules:

| Parameter                | Required | Type      | Description |
| ------------------------ | -------- | --------- | ----------- |
|**Id**              | Required | `string` | Unique identifier for the schedule<br><br>Allowed value: any string identifier |
|**Period** | Required | `string` | The data sampling rate of the schedule. The expected format is HH:MM:SS.###. * <br><br>Invalid input: `null`, negative timespan, zero <br> Default value: `null` (must be specified)|
|**Offset**     | Optional | `string` | The offset from the midnight when the schedule starts. The expected format is HH:MM:SS.### * <br><br>Invalid input: negative timespan<br>Default value: `null`|

**\* Note:** You can also specify timespans as numbers in seconds. For example, `"Period": 25` specifies 25 seconds, or `"Period": 125` specifies 2 minutes and 5 seconds.

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
| api/v1/configuration/_ComponentId_/Schedules      | GET       | Gets all configured schedules |
| api/v1/configuration/_ComponentId_/Schedules      | DELETE    | Deletes all configured schedules |
| api/v1/configuration/_ComponentId_/Schedules      | POST      | Adds an array of schedules or a single schedule. Fails if any schedule already exists |
| api/v1/configuration/_ComponentId_/Schedules      | PUT       | Replaces all schedules |
| api/v1/configuration/_ComponentId_/Schedules/*id* | GET       | Gets configured schedule by *id* |
| api/v1/configuration/_ComponentId_/Schedules/*id*| DELETE     | Deletes configured schedule by *id* |
| api/v1/configuration/_ComponentId_/Schedules/*id* | PUT       | Replaces schedule by *id*. Fails if schedule does not exist |
| api/v1/configuration/_ComponentId_/Schedules/*id* | PATCH     | Allows partial updating of configured schedule by *id* |

**Note:** Replace *ComponentId* with the Id of your adapter component.
