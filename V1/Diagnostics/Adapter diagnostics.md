---
uid: AdapterDiagnostics
---

# Adapter diagnostics

To egress diagnostics related data, you have to configure an adapter health endpoint first. See [Health and diagnostics configuration](xref:HealthAndDiagnosticsConfiguration).

For diagnostics data related examples, see [Examples](#examples).

## Diagnostics schema

The full schema definition for the diagnostics configuration is in the *System_Diagnostics_schema.json* here:

Windows: %Program Files%\OSIsoft\Adapters\AdapterName\Schemas

Linux: /opt/OSIsoft/Adapters/AdapterName/Schemas

## Diagnostics parameters

The Diagnostics.System dynamic type includes the following values which are logged in a stream with the id System.Diagnostics.
This diagnostic stream contains system level information related to the host platform that the adapter is running on.

| Parameter                           | Type       | Description                                                                       |
| ----------------------------------- | ---------- | --------------------------------------------------------------------------------- |
| timestamp                           | **string** | Timestamp of event                                                                |
| ProcessIdentifier                   | **int**    | Process id of the host process                                                    |
| StartTime                           | **string** | Time at which the host process started                                            |
| WorkingSet                          | **long**   | Amount of physical memory in bytes, allocated for the host process                |
| TotalProcessorTime (uom=s)          | **double** | Total processor time for the host process expressed in seconds                    |
| TotalUserProcessorTime (uom=s)      | **double** | User processor time for the host process expressed in seconds                     |
| TotalPrivilegedProcessorTime (uom=s)|**double**  | Privileged processor time for the host process expressed in seconds               |
| ThreadCount                         | **int**    | Number of threads in the host process                                             |
| HandleCount                         | **int**    | Number of handles opened by the host process                                      |
| ManagedMemorySize (uom=MB)          | **double** | Number of bytes currently thought to be allocated in managed memory               |
| PrivateMemorySize (uom=MB)          | **double** | Amount of paged memory, in bytes, allocated for the host process                  |
| PeakPagedMemorySize (uom=MB)        | **double** | Maximum amount of memory in the virtual memory paging file, in bytes, used by the host process.|
| StorageTotalSize (uom=MB)           | **double** | Total size of the storage medium in use by the system                             |
| StorageFreeSpace (uom=MB)           | **double** | Free space available                                                              |

Each adapter component produces its own diagnostics streams.

## Examples

### Retrieve the diagnostics configuration

Example using curl:

```
curl -X GET  http://localhost:{port}/api/v1/configuration/system/diagnostics
```

Sample output:

```
{
    "enableDiagnostics": true
}
```

### Configure diagnostics

Example using curl:

```
curl -X PUT  http://localhost:{port}/api/v1/configuration/system/diagnostics  -H 'Content-Type: application/json' -d '{ "enableDiagnostics": true }'
```

In the previous examples, _port_ refers to the configured port for the adapter to run on.

If successful, the methods returns a `204 No Content` response code.



## REST URLs

| Relative URL                            | HTTP verb | Action                                          |
| --------------------------------------- | --------- | ----------------------------------------------- |
| `api/v1/configuration/system/diagnostics` | `GET`       | Gets the diagnostics configuration              |
| `api/v1/configuration/system/diagnostics` | `PUT`       | Replaces the existing diagnostics configuration |

## AF structure

After running diagnostics with a health endpoint configured to a PI server, you can use _**PI System Explorer**_ to view the diagnostics for a given adapter. The element hierarchy is shown in the following image. 

![System.Diagnostics](../images/Diagnostics_System.jpg)

**Note:**

- The_**Elements**_ root contains a link to an _**Adapters**_ node. This is the root note for all adapter instances.
- Below _**Adapters**_ there will be one or more adapter nodes. Each node's title is defined by the node's corresponding computer name and service name in this format: `_**{ComputerName}.{ServiceName}**_`. For example, in the following image, **_RGRALAK5530_** is the computer name, and _**SignalGenerator**_ is the service name.
- To see the **System.Diagnostics** values, clicking on an adapter node and set the tab to _**Attributes**_. Example values are shown in the image.
