---
uid: SchedulesConfiguration
---

# Schedules

You can configure PI adapters to run scans based on a schedule. If the adapter supports schedules, each data item in the data selection configuration can be assigned a schedule. The adapter will then sample data for those data items at the scheduled time.

**Note:** If the adapter supports scheduling and you start an ingress component without a schedules configuration, a default schedules configuration will be added to be used as an example.

**Note:** When the adapter framework scheduler misses or skips a scan due to any reason, either one of the following messages is printed: `Scan skipped for schedule id <Id>` or `Scan missed for schedule <id>`.

## Configure schedules

Complete the following steps to change the schedules configuration:

1. Using any text editor, create a file that contains the schedules configuration in the JSON format.
    - For content structure, see [Example](#example).
    - For all available parameters, see [Schedules parameters](#schedules-parameters).

2. Save the file. For example, `ConfigureSchedules.json`.

3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to run a PUT command with the contents of the file to the following endpoint: `http://localhost:5590/api/v1/configuration/<ComponentId>/Schedules`.

    **Note:**  Replace _&lt;ComponentId&gt;_ with the ComponentId of the adapter.

    `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using `curl`:

    **Note:** Run this command from the same directory where the file is located.

    ```bash
    curl -d "@ConfigureSchedules.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/<ComponentId>/Schedules"
    ```

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
