---
uid: HealthEndpointConfiguration
---

# Health endpoint configuration

OSIsoft adapters can be configured to produce and store health data at a designated health endpoint.
For more information about adapter health, see [Adapter health](xref:AdapterHealth).

## Configure health endpoint

A health endpoint designates an OMF endpoint where adapter health information should be sent. You can configure multiple health endpoints.

1. Using any text editor, create a file that contains one or more health endpoints in JSON form.
    - For content structure, see [Examples](#examples).
    - For a table of all available health endpoint parameters, see [Health endpoint parameters](#health-endpoint-parameters).
2. Save the file, for example as *HealthEndpoints.json*.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute either a POST or PUT command to their appropriate endpoint.

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.
    
    - **POST** endpoint: `http://localhost:5590/api/v1/configuration/system/healthendpoints`

        Example using curl (run this command from the same directory where the file is located):

        ```bash
        curl -d "@HealthEndpoints.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/system/healthendpoints"
        ```
    - **PUT** endpoint: `http://localhost:5590/api/v1/configuration/system/healthendpoints/{id}`
    
        Example using curl (run this command from the same directory where the file is located):

        ```bash
        curl -d "@HealthEndpoints.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/system/healthendpoints/OCS"
         ```
    

## Health endpoints schema

The full schema definition for the health endpoint configuration is in the *System_HealthEndpoints_schema.json* here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Health endpoint parameters

The following parameters are available for configuring health endpoints:

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| **Id**                          | Optional                            | `string`    | Uniquely identifies the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. |
| **Endpoint**                    | Required                            | `string`    | The URL of the OMF endpoint to receive this health data. |
| **Username**                    | Required for PI Web API endpoints   | `string`    | The username used to authenticate with a PI Web API OMF endpoint. |
| **Password**                    | Required for PI Web API endpoints   | `string`    | The password used to authenticate with a PI Web API OMF endpoint. |
| **ClientId**                    | Required for OCS endpoints          | `string`    | The Client Id used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoints          | `string`    | The Client Secret used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **TokenEndpoint** | Optional for OCS endpoints | `string` | Retrieves an OCS token from an alternative endpoint. |
| **ValidateEndpointCertificate** | Optional                            | `boolean`      | Disables verification of destination security certificate. Use for testing only with self-signed certificates; OSIsoft recommends keeping this set to the default, true, in production environments.|

## Examples

### OCS endpoint

```code
{
    "Id": "OCS",
    "Endpoint": "https://<OCS OMF endpoint>",
    "ClientId": "<clientid>",
    "ClientSecret": "<clientsecret>"
}
```

### PI Web API endpoint

```code
{
    "Id": "PI Web API",
    "Endpoint": "https://<pi web api server>/piwebapi/omf/",
    "UserName": "<username>",
    "Password": "<password>"
}
```

## REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/system/healthEndpoints      | GET       | Gets all configured health endpoints. |
| api/v1/configuration/system/healthEndpoints      | DELETE    | Deletes all configured health endpoints. |
| api/v1/configuration/system/healthEndpoints      | POST      | Adds an array of health endpoints or a single endpoint. Fails if any endpoint already exists. |
| api/v1/configuration/system/healthEndpoints      | PUT       | Replaces all health endpoints. **Note:** Requires an array of endpoints. |
| api/v1/configuration/system/healthEndpoints/*id* | GET       | Gets configured health endpoint by *id*. |
| api/v1/configuration/system/healthEndpoints/*id*| DELETE     | Deletes configured health endpoint by *id*. |
| api/v1/configuration/system/healthEndpoints/*id* | PUT       | Replaces health endpoint by *id*. Creates new health endpoint if it does not exist.|
| api/v1/configuration/system/healthEndpoints/*id* | PATCH     | Allows partial updating of configured health endpoint by *id*. |

**Note:** Replace *id* with the Id of the health endpoint.
