---
uid: HealthAndDiagnosticsConfiguration
---

# Health and diagnostics configuration

The following sections provide an overview on how to configure health endpoints to which health and diagnostics data can be sent.

## Health

Adapters produce various types of health data. You can use this information to ensure that your adapters are running properly and data is flowing to the configured OSIsoft OMF endpoints. This section provides information on how to configure your OSIsoft adapters so that this health data is produced and stored at a designated endpoint and what types of health data are available. For more information about adapter health, see [Adapter health](xref:AdapterHealth).

### Configure health endpoint

A health endpoint designates an OSIsoft OMF endpoint where adapter health information should be sent. You can configure multiple health endpoints. 

1. Using any text editor, create a file that contains one or more health endpoints in JSON form.
    - For a table of all available health endpoint parameters, see [Health endpoint parameters](#health-endpoint-parameters).
2. Save the file.
3. Use any tool capable of making HTTP requests and execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/healthendpoints/`

### Health endpoints schema definition

The full schema definition for the health endpoint configuration is in the *System_HealthEndpoints_schema.json* here:

Windows: %Program Files%\OSIsoft\Adapters\AdapterName\Schemas

Linux: /opt/OSIsoft/Adapters/AdapterName/Schemas

### Health endpoint parameters

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| **Id**                          | Optional                            | `string`    | Uniquely identifies the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. |
| **Endpoint**                    | Required                            | `string`    | The URL of the OMF endpoint to receive this health data. |
| **ClientId**                    | Required for OCS endpoints          | `string`    | The Client Id used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoints          | `string`    | The Client Secret used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **Username**                    | Required for PI Web API endpoints   | `string`    | The username used to authenticate with a PI Web API OMF endpoint. |
| **Password**                    | Required for PI Web API endpoints   | `string`    | The password used to authenticate with a PI Web API OMF endpoint. |
| **BufferingEnabled**            | Optional                            | `boolean`      | Enables or disables buffering to this endpoint. By default, buffering is enabled ("true"). |
| **ValidateEndpointCertificate** | Optional                            | `boolean`      | Disables verification of destination security certificate. Use for testing only with self-signed certificates; OSIsoft recommends setting this to true in production environments. Defaults to true. |

## Diagnostics

The adapter and its components produce diagnostics data which is sent to all health endpoints. The _System_Diagnostics.json_ file contains a flag which determines whether Diagnostics are enabled. You can change this at runtime through REST calls or the EdgeCmd utility. Diagnostics data are collected by default. To egress diagnostics related data, you have to configure an adapter health endpoint. For more information about adapter diagnostics, see [Adapter diagnostics](xref:AdapterDiagnostics).

### Diagnostics schema definition

The full schema definition for the diagnostics configuration is in the *System_Diagnostics_schema.json* here:

Windows: %Program Files%\OSIsoft\Adapters\AdapterName\Schemas

Linux: /opt/OSIsoft/Adapters/AdapterName/Schemas
