---
uid: BufferingConfiguration
---

# Configure buffering

You can configure buffering for data egressed from the adapter to endpoints through the buffering configuration parameters in the system configuration.

**Note:** OSIsoft recommends that you do not modify the default buffering location unless necessary. The changes to the buffering configuration parameters take effect only during adapter service startup.

## System buffering configuration parameters:

 Parameter | Type | Description |
| ----------|:-----:| :-----------|
| **EnableBuffering** | Boolean | Enables or disables buffering.  <br> Default: True |
| **MaxBufferSizeMB** | Integer | Defines the maximum size of the buffer file that will be persisted on disk. The unit is specified in MB (1 Mebibyte = 1048576 bytes). Take into account the capacity and type of the storage medium to determine a suitable value for this parameter. A value of -1 indicates that the buffer file size is restricted only by the available free disk space. <br><br> Allowed values: -1 or [1, 2147483647]. <br><br> Default: -1 |
| **BufferLocation** | String | Defines the location of the buffer files. Absolute paths are required. Take into account access-control list (ACL) when setting this parameter <br><br> Allowed value: Valid path to a folder location in the file system. <br><br> Default: <br> **Windows:** _%ProgramData%\OSIsoft\Adapters\\{AdapterType}\\{AdapterInstance}\Data_ <br> **Linux:** _/usr/share/OSIsoft/Adapters/{AdatpterType}/{AdapterInstance}/Data_ |

## REST URIs

The relative URI for all buffering configuration actions is `api/v1/configuration/system/buffering`.

| HTTP verb | Action               |
|-----------------------------------------------------------|-----------|
| GET       | Gets the buffering configuration |
| PUT       | Replaces the existing buffering configuration |
| PATCH | Update parameter, partial configuration |

## Examples

The following examples are buffering configurations made through curl REST client.

### Retrieve the buffering configuration

```
curl -X GET "http://localhost:{port}/api/v1/configuration/system/buffering"
```

Sample output:

```
{
    "bufferLocation": "C:/ProgramData/OSIsoft/Adapters/Modbus/Modbus/Buffers",
    "maxBufferSizeMB": -1,
    "enableBuffering": true
}
```

`200 OK` response indicates success.

### Configure buffering

```
curl -X PUT "http://localhost:{port}/api/v1/configuration/system/buffering" -H "Content-Type: application/json" -d "{ "MaxBufferSizeMB": 50, "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/NewBuffers", "EnableBuffering": true }"
```

`204 No Content` response indicates success.


### Update MaxBuferSizeMb parameter

```
curl -X PATCH "http://localhost:{port}/api/v1/configuration/system/buffering" -H "Content-Type: application/json" -d "{ "MaxBufferSizeMB": 100 }"
```

`204 No Content` response indicates success.

**Note:** In the previous examples, *port* refers to the configured port that the adapter runs on.

### System Buffering Schema Definition

Below is the full schema definition for the buffering configuration.

File: *System_Buffering_schema.json*

```c#
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "BufferingConfiguration",
  "SchemaVersion": "1.0.0",
  "definitions": {
    "EdgeConfigurationBase": {
      "type": "object",
      "x-abstract": true,
      "additionalProperties": false
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/EdgeConfigurationBase"
    },
    {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "BufferLocation": {
          "type": [
            "null",
            "string"
          ]
        },
        "MaxBufferSizeMB": {
          "type": "integer",
          "format": "int32"
        },
        "EnableBuffering": {
          "type": "boolean"
        }
      }
    }
  ]
}
```

