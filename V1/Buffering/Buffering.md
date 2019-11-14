---
uid: BufferingConfiguration
---

# Overview
***Note***
This section talks about the global parameters used for on-disk buffering configuration. For enabling or disabling buffering at the individual egress endpoint level using the *bufferingEnabled* field please refer to: <</INSERT LINK HERE>>

The parameters for on-disk buffering for the adapters that can be configured are

| Parameter | Required | Type | Description |
| ----------|:--------:| ----:| :-----------|
| OnDiskMaxBufferSizeMB | Yes | Integer | Defines the maximum size of the buffer file that will be persisted on disk. The unit is specified in MB (Mebibyte 1 MiB = 1048576 bytes). The capacity and type of the storage medium must be taken into account before determining an alternate value for this parameter. If you do not wish to specify a maximum file size then a value of -1 indicates that the file size is restricted only by the available free disk space. <br> Allowed values: -1 or [1, 2147483647]. <br> Default: -1 | 
| OnDiskBufferLocation | Optional | String | This parameter defines the maximum size of the buffer file that will be persisted on disk. The unit is specified in MB (Mebibyte 1 MiB = 1048576 bytes). The capacity and type of the storage medium must be taken into account before determining an alternate value for this parameter. If you do not want to specify the any maximum file size then a value of -1 indicates that the buffer size is restricted only by the available free disk space. <br> Allowed Value: Path to an existing folder location in the file system. <br> Default: %ProgramData%\Adapters\Data (Windows OS) <br> /usr/share/OSIsoft/Adapters/Data (Linux OS) <br> ***Note*** It is strongly recommended *against modifying* the default buffer location value |

### Retrieving the buffering configuration via REST client
```
curl -X GET  http://localhost:{port}/api/v1/configuration/egress/buffering
```
Sample output:

```
{
    "onDiskBufferLocation": "C:\\ProgramData\\OSIsoft\\Adapters\\Data",
    "onDiskMaxBufferSizeMB": 10
}
```

### Configuring buffer via REST client
```
curl -X PUT  http://localhost:{port}/api/v1/configuration/egress/buffering  -H 'Content-Type: application/json' -d '{ "onDiskMaxBufferSizeMB": 25,
"onDiskBufferLocation": "C:\\ProgramData\\OSIsoft\\Data"
}'
```
In the above samples *port* refers to configured port for the Adapter to run.
