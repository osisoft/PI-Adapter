---
uid: DataFiltersConfiguration
---

# Data filters configuration

PI adapters can be configured to perform data filtering to save network bandwidth. Every data item in the data selection configuration can be assigned the ID of a data filter. The adapter will then filter data for those data items based on the data filter configuration.

## Configure data filters

Complete the following steps to change the data filters configuration:

1. Using any text editor, create a file that contains the data filters configuration in the JSON format.
    - For content structure, see [Data filters example](#data-filters-example).
    - For all available parameters, see [Data filters parameters](#data-filters-parameters).

2. Save the file, for example, as `ConfigureDataFilters.json`.

3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to run a PUT command with the contents of the file to the following endpoint: `http://localhost:5590/api/v1/configuration/<ComponentId>/DataFilters`.

    **Note:**  Replace _&lt;ComponentId&gt;_ with the ComponentId of the adapter, for example, _Modbus1_.

    `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using `curl`:

    ```bash
    curl -d "@ConfigureDataFilters.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/<ComponentId>/DataFilters"
    ```

    **Note:** Run this command from the same directory where the file is located.

On successful execution, the change that you have made to data filters takes effect immediately during runtime.

## Data filters schema

The full schema definition for the data filters configuration is in the  `AdapterName_DataFilters_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\<AdapterName>\Schemas`

Linux: `/opt/OSIsoft/Adapters/<AdapterName>/Schemas`

## Data filters parameters

The following parameters are available for configuring data filters:

| Parameter                | Required | Type      | Description |
| ------------------------ | -------- | --------- | ----------- |
|**Id**              | Required | `string` | Unique identifier for the data filter. <br><br>Allowed value: any string identifier<br> |
|**AbsoluteDeadband** | Optional | `double` | Specifies the absolute change in data value that should cause the current value to pass the filter test. <br> **Note:** You must specify `AbsoluteDeadband` or `PercentChange`.<br><br>Allowed value: double value representing absolute deadband number<br>Default value: `null` |
|**PercentChange**     | Optional | `double` | Specifies the percent change from previous value that should cause the current value to pass the filter test. <br> **Note:** You must specify `AbsoluteDeadband` or `PercentChange`.<br><br>Allowed value: double value representing percent change<br>Default value: `null` |
|**ExpirationPeriod**     | Optional | `timespan` | The length in time that can elapse after an event before automatically storing the next event. The expected format is HH:MM:SS.###. * <br><br>Allowed value: any timespan <br>Default value: `null`|

**\* Note:** You can also specify timespans as numbers in seconds. For example, `"ExpirationPeriod": 25` specifies 25 seconds, or `"ExpirationPeriod": 125` specifies 2 minutes and 5 seconds.

## Data filters example

```code
[
  {
    "Id": "DuplicateData",
    "AbsoluteDeadband": 0,
    "PercentChange": null,
    "ExpirationPeriod": "01:00:00"
  }
]
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/_ComponentId_/DataFilters      | GET       | Gets all configured data filters. |
| api/v1/configuration/_ComponentId_/DataFilters      | DELETE    | Deletes all configured data filters. |
| api/v1/configuration/_ComponentId_/DataFilters      | POST      | Adds an array of data filters or a single data filter. Fails if any data filter already exists. |
| api/v1/configuration/_ComponentId_/DataFilters      | PUT       | Replaces all data. |
| api/v1/configuration/_ComponentId_/DataFilters      | PATCH     | Allows partial updating of configured data filter. |
| api/v1/configuration/_ComponentId_/DataFilters/*id* | GET       | Gets configured data filter by *id*. |
| api/v1/configuration/_ComponentId_/DataFilters/*id*| DELETE     | Deletes configured data filter by *id*. |
| api/v1/configuration/_ComponentId_/DataFilters/*id* | PUT       | Replaces data filter by *id*. Fails if data filter does not exist. |

**Note:** Replace *ComponentId* with the Id of your adapter component, for example, Modbus1.
