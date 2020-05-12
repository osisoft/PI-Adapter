---
uid: BufferingConfiguration
---

# Buffering configuration

You can configure OSIsoft adapters to buffer data egressed from the adapter to endpoints. Buffering is configured through the buffering configuration parameters in the system configuration.

**Note:** OSIsoft recommends that you do not modify the default buffering location unless it is necessary. Changes to the buffering configuration parameters only take effect during adapter service startup.

## Configure buffering

1. Using any text editor, create a file that contains the buffering configuration in the JSON format.
   - For content structure, see the sample output in [Examples - Retrieve the buffering configuration](#examples).
   - For a table of all available parameters, see [Buffering parameters](#buffering-parameters).
2. Save the file. For example, *Buffering.json*.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests and execute a `PUT` command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/buffering`

     **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

     Example using `curl`:

     ```bash
      curl -d "@Buffering.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/buffering"
     ```

**Note:** Run this command from the same directory where the file is located.

## Buffering schema

The full schema definition for the system buffering is in the *System_Buffering_schema.json* here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Buffering parameters

The following parameters are available for configuring buffering:

| Parameter | Required | Type | Description |
| ----------| -------- | ---- | ----------- |
| **EnablePersistentBuffering**  | Optional |  `boolean` | Enables or disables on-disk buffering <br><br> Default: True <br><br> **Note:** If you disable persistent buffering, in-memory buffering is used. In-memory buffering is limited by value in the MaxBufferSizeMB property. |
| **MaxBufferSizeMB**  | Optional     |`integer` | Defines the maximum size of the buffer files that are persisted on disk or used in memory when EnablePersistentBuffering is set to false per configured endpoint. The unit is specified in MB (1 Megabyte = 1048576 bytes). Consider the capacity and the type of storage medium to determine a suitable value for this parameter. <br><br> Allowed values: [1, 2147483647] <br><br> Default: 1024 |
| **BufferLocation**   | Required  | `string` | Defines the location of the buffer files. Absolute paths are required. Consider the access-control list (ACL) when you set this parameter. <br><br> Allowed value: Valid path to a folder location in the file system <br><br> Default: <br> **Windows:** _%ProgramData%\OSIsoft\Adapters\\{AdapterInstance}\Buffers_ <br> **Linux:** _/usr/share/OSIsoft/Adapters/{AdapterInstance}/Buffers_ |

## Examples

The following examples are buffering configurations made through the`curl` REST client.

### Retrieve the buffering configuration

```cmd
curl -X GET "http://localhost:5590/api/v1/configuration/system/buffering"
```

Sample output:

```code
{
    "bufferLocation": "C:/ProgramData/OSIsoft/Adapters/Modbus/Buffers",
    "maxBufferSizeMB": 1024,
    "enablePersistentBuffering": true
}
```

`200 OK` response indicates success.

### Update MaxBufferSizeMb parameter

```cmd
curl -d "{ "MaxBufferSizeMB": 100 }" -H "Content-Type: application/json" -X PATCH "http://localhost:5590/api/v1/configuration/system/buffering"
```

`204 No Content` response indicates success.

## REST URLs

| Relative URL | HTTP verb | Action               |
| ------------ |---------- |----------------------|
| api/v1/configuration/system/buffering | GET       | Gets the buffering configuration |
| api/v1/configuration/system/buffering | PUT       | Replaces the existing buffering configuration |
| api/v1/configuration/system/buffering | PATCH     | Update parameter, partial configuration |
