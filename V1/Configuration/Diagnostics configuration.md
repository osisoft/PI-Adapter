---
uid: DiagnosticsConfiguration
---

# Diagnostics configuration

This section provides information on how to configure your OSIsoft adapters so that diagnostics data is produced and stored at the designated health endpoint.

For more information about adapter diagnostics, see [Adapter diagnostics](xref:AdapterDiagnostics).

## Configure diagnostics

1. Using any text editor, create a file that contains the diagnostics configuration in JSON form.
   - For content structure, see [Example - Retrieve the diagnostics configuration](#example).
   - For a table of all available parameters, see [Diagnostics parameters](#diagnostics-parameters).
3. Save the file.
4. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests and execute a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/diagnostics`

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

## Diagnostics schema

The full schema definition for the diagnostics configuration is in the *System_Diagnostics_schema.json* here:

Windows: *%Program Files%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Diagnostics parameters

| Parameter             | Required | Type    | Description |
| ---------             | -------- | ------- | ----------- |
| **EnableDiagnostics** | Yes      | `boolean` | Determines whether Diagnostics are enabled. |

## Example

**Configure diagnostics**

Example using curl:

```
curl -X PUT -H "Content-Type:application/json" -d '{"enableDiagnostics":true }' http://localhost:{port}/api/v1/configuration/system/diagnostics
```

If successful, the methods returns a `204 No Content` response code.

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
