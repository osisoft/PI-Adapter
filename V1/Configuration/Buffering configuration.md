---
uid: BufferingConfiguration
---

# Configure buffering

The the data egressed from the Adapter to endpoints can be buffered and this is configured through the buffering configuration parameters in the system configuration.

> **Note:** OSIsoft recommends that you do not modify the default buffering location unless necessary. The changes to the buffering configuration parameters take effect only during Adapter service startup.

System buffering configuration parameters:

 Parameter | Type | Description |
| ----------|:-----:| :-----------|
| EnableBuffering | Boolean | Enables or disables buffering.  <br> Default: True |
| MaxBufferSizeMB | Integer | Defines the maximum size of the buffer file that will be persisted on disk. The unit is specified in MB (1 Mebibyte = 1048576 bytes). Take into account the capacity and type of the storage medium to determine a suitable value for this parameter. A value of -1 indicates that the buffer file size is restricted only by the available free disk space. <br> Allowed values: -1 or [1, 2147483647]. <br> Default: -1 |
| BufferLocation | String | Defines the location of the buffer files. Absolute paths are required. Take into account access-control list (ACL) when setting this parameter <br> Allowed value: Valid path to a folder location in the file system. <br> Default: **Windows:** _%ProgramData%\OSIsoft\Adapters\\{AdapterType}\\{AdapterInstance}\Data_ <br> **Linux:** _/usr/share/OSIsoft/Adapters/{AdatpterType}/{AdapterInstance}/Data_ |

## REST URIs

| Relative URI                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/system/buffering      | GET       | Gets the buffering configuration |
|       | PUT       | Replaces the existing buffering configuration |
| | PATCH | Update parameter, partial configuration |

## Examples
### Retrieve the buffering configuration through curl REST client
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

### Configure buffering through curl REST client
```
curl -X PUT "http://localhost:{port}/api/v1/configuration/system/buffering" -H "Content-Type: application/json" -d "{ "MaxBufferSizeMB": 50, "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/NewBuffers", "EnableBuffering": true }"
```
`204 No Content` response indicates success.


### Update MaxBuferSizeMb parameter through curl REST client
```
curl -X PATCH "http://localhost:{port}/api/v1/configuration/system/buffering" -H "Content-Type: application/json" -d "{ "MaxBufferSizeMB": 100 }"
```
`204 No Content` response indicates success.

In the previous examples, *port* refers to the configured port that the adapter runs on.
