---
uid: DiagnosticsConfiguration
---

# Diagnostics configuration

OSIsoft adapters can be configured to produce and store diagnostics data at a designated health endpoint.
For more information about available diagnostics data, see [Adapter diagnostics](xref:AdapterDiagnostics).

## Configure diagnostics

1. Start any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests.
2. Execute a PUT command to the following endpoint, setting the `enableDiagnostics` parameter to either **true** or **false**: `http://localhost:5590/api/v1/configuration/system/diagnostics`

   **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

   Example using curl:

   ```bash
   curl -d "{ "enableDiagnostics":true }" -H "Content-Type:application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/diagnostics"
   ```

## Diagnostics schema

The full schema definition for the diagnostics configuration is in the *System_Diagnostics_schema.json* here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Diagnostics parameters

The following parameters are available for configuring diagnostics:

| Parameter             | Required | Type    | Description |
| ---------             | -------- | ------- | ----------- |
| **EnableDiagnostics** | Required | `boolean` | Determines whether Diagnostics are enabled. |

## Example

### Retrieve the diagnostics configuration

Example using curl:

```bash
curl -X GET "http://localhost:{port}/api/v1/configuration/system/diagnostics"
```

Sample output:

```code
{
    "enableDiagnostics": true
}
```

## REST URLs

| Relative URL                            | HTTP verb | Action                                          |
| --------------------------------------- | --------- | ----------------------------------------------- |
| api/v1/configuration/system/diagnostics | GET       | Gets the diagnostics configuration.              |
| api/v1/configuration/system/diagnostics | PUT       | Replaces the existing diagnostics configuration. |
