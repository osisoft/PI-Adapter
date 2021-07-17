---
uid: BufferingConfiguration
---

# Buffering

You can configure PI adapters to buffer data egressed from the adapter to egress and health endpoints. Buffering is configured through the buffering configuration parameters in the system configuration. You can configure buffering as memory only or on disk.

**Note:** OSIsoft recommends that you do not modify the default buffering location unless it is necessary. Changes to the buffering configuration parameters only take effect during adapter service startup.

## Configure buffering

Complete the following steps to configure buffering. Use the `PUT` method in conjunction with the `http://localhost:5590/api/v1/configuration/system/buffering` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for buffering into the file.

    For sample JSON, see [Examples - Retrieve the buffering configuration](#examples).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Buffering parameters](#buffering-parameters).

4. Save the file. For example, as `ConfigureBuffering.json`.

5. Open a command line session. Change directory to the location of `ConfigureBuffering.json`.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the buffering configuration.

    ```bash
    curl -d "@ConfigureBuffering.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/buffering"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * For a list of other REST operations you can perform, like updating or replacing a buffering configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

## Buffering schema

The full schema definition for the system buffering is in the `System_Buffering_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\<AdapterName>\Schemas`

Linux: `/opt/OSIsoft/Adapters/<AdapterName>/Schemas`

## Buffering parameters

The following parameters are available for configuring buffering:

| Parameter | Required | Type | Description |
| ----------| -------- | ---- | ----------- |
| **EnablePersistentBuffering**  | Optional |  `boolean` | Enables or disables on-disk buffering <br><br> Allowed value: `true` or `false`<br>Default value: `true` <br><br> **Note:** If you disable persistent buffering, in-memory buffering is used. In-memory buffering is limited by value in the MaxBufferSizeMB property. |
| **MaxBufferSizeMB**  | Optional     |`integer` | Defines the maximum size of the buffer files that are persisted on disk <sup>1</sup> or used in memory <sup>2</sup> when EnablePersistentBuffering is set to false per configured endpoint. The unit is specified in MB (1 Megabyte = 1048576 bytes). Consider the capacity and the type of storage medium to determine a suitable value for this parameter. <br><br>Minimum value: `1`<br>Maximum value:  `2147483647`<br> Default value: `1024`  |
| **BufferLocation**   | Required  | `string` | Defines the location of the buffer files. Absolute paths are required. Consider the access-control list (ACL) when you set this parameter. <br><br> Allowed value: Valid path to a folder location in the file system <br> Default value: <br> **Windows:** _%ProgramData%\OSIsoft\Adapters\\{AdapterInstance}\Buffers_ <br> **Linux:** _/usr/share/OSIsoft/Adapters/{AdapterInstance}/Buffers_ |

<sup>1</sup> **Buffering to disk** - disk is only used if required; <br> 
        - The MaxBufferSizeMB per an endpoint and buffer file is 20MB of storage.<br>
        - When MaxBufferSizeMB is reached, the oldest buffer file is deleted and a new buffer file created.<br>
        - When the buffer file of a MaxBufferSizeMB of 20MB fills, a new buffer file is created and the previous buffer file deleted.

**Note:** The following rules apply in case of an error when creating a new buffer file:

- Attempt to delete oldest buffer file and retry.
- If unable to buffer, errors are logged to indicate data loss.
- If a buffer file is corrupted, an attempt is made to recover individual records and any failure to recover records is logged.

<sup>2</sup> **Buffering only to memory**:<br>
        - The MaxBufferSizeMB of health endpoints is limited to 20MB of memory.<br>
        - When MaxBufferSizeMB is reached, only the oldest message in the memory buffer is removed. Depending on the size of a new message, several old messages are removed.<br>

## Examples

The following examples are buffering configurations made through the`curl` REST client.

### Retrieve the buffering configuration

```cmd
curl -X GET "http://localhost:5590/api/v1/configuration/system/buffering"
```

Sample output:

```code
{
    "bufferLocation": "C:/ProgramData/OSIsoft/Adapters/<AdapterName>/Buffers",
    "maxBufferSizeMB": 1024,
    "enablePersistentBuffering": true
}
```

`200 OK` response indicates success.

### Update MaxBufferSizeMb parameter

```cmd
curl -d "{ \"MaxBufferSizeMB\": 100 }" -H "Content-Type: application/json" -X PATCH "http://localhost:5590/api/v1/configuration/system/buffering"
```

`204 No Content` response indicates success.

## REST URLs

| Relative URL | HTTP verb | Action               |
| ------------ |---------- |----------------------|
| api/v1/configuration/system/buffering | GET       | Gets the buffering configuration |
| api/v1/configuration/system/buffering | PUT       | Replaces the existing buffering configuration |
| api/v1/configuration/system/buffering | PATCH     | Update parameter, partial configuration |
