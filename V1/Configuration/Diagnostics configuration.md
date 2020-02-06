---
uid: DiagnosticsConfiguration
---

# Diagnostics configuration

This section provides information on how to configure your OSIsoft adapters so that diagnostics data is produced and stored at the designated health endpoint.

For more information about adapter diagnostics, see [Adapter diagnostics](xref:AdapterDiagnostics).

## Configure diagnostics

1. Using any text editor, create a file that contains a flag which determines whether Diagnostics are enabled in JSON form.
    - For a table of all available diagnostics parameters, see [Diagnostics parameters](#diagnostics-parameters).
2. Save the file.
3. Use any tool capable of making HTTP requests and execute a PUT command with the contents of that file to the following endpoint: `http://localhost:{port}/api/v1/configuration/system/diagnostics`

    **Note:** _port_ refers to the configured port for the adapter to run on.
    
    Example using curl:

    ```
    curl -X PUT  http://localhost:{port}/api/v1/configuration/system/diagnostics  -H 'Content-Type: application/json' -d '{ "enableDiagnostics": true }'
    ```

    If successful, the methods returns a `204 No Content` response code.

## Diagnostics schema

The full schema definition for the diagnostics configuration is in the *System_Diagnostics_schema.json* here:

Windows: *%Program Files%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

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

## Example

**Retrieve the diagnostics configuration**

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

## REST URLs

| Relative URL                            | HTTP verb | Action                                          |
| --------------------------------------- | --------- | ----------------------------------------------- |
| `api/v1/configuration/system/diagnostics` | `GET`       | Gets the diagnostics configuration              |
| `api/v1/configuration/system/diagnostics` | `PUT`       | Replaces the existing diagnostics configuration |
