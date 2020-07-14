---
uid: HealthEndpointConfiguration
---

# Health endpoint configuration

You can configure PI adapters to produce and store health data at a designated health endpoint. You can use health data to ensure that your adapters are running properly and that data flows to the configured OMF endpoints.

For more information about adapter health, see [Adapter health](xref:AdapterHealth).

## Configure health endpoint

A health endpoint designates an OMF endpoint where adapter health information is sent. You can configure multiple health endpoints.

1. Using any text editor, create a file that contains one or more health endpoints in the JSON format.
    - For content structure, see [Examples](#examples).
    - For a table of all available health endpoint parameters, see [Health endpoint parameters](#health-endpoint-parameters).
2. Save the file. For example, *HealthEndpoints.json*.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to run either a `POST` or `PUT` command to their appropriate endpoint.

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    - **POST** endpoint: `http://localhost:5590/api/v1/configuration/system/healthendpoints`

        Example using `curl`:

        **Note:** Run this command from the same directory where the file is located.

        ```bash
        curl -d "@HealthEndpoints.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/system/healthendpoints"
        ```

    - **PUT** endpoint: `http://localhost:5590/api/v1/configuration/system/healthendpoints/{Id}`
  
        Example using `curl`:

        **Note:** Run this command from the same directory where the file is located.

        ```bash
        curl -d "@HealthEndpoints.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/system/healthendpoints/OCS"
        ```

## Health endpoints schema

The full schema definition for the health endpoint configuration is in the `System_HealthEndpoints_schema.json` file located in one of the following folders:

Windows: `*%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas`

Linux: `/opt/OSIsoft/Adapters/AdapterName/Schemas`

## Health endpoint parameters

The following parameters are available for configuring health endpoints:

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| **Id**                          | Optional                            | `string`    | Uniquely identifies the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. <br><br>Allowed value: any string identifier<br>Default value: new GUID|
| **Endpoint**                    | Required                            | `string`    | The URL of the OMF endpoint to receive this health data <br><br>Allowed value: well-formed http or https endpoint string<br>Default: `null`|
| **Username**                    | Required for PI Web API and EDS endpoints   | `string`    | The username used to authenticate with a PI Web API OMF or EDS endpoint <br><br>_PI server:_<br>Allowed value: any string<br>Default: `null`<br><br>_EDS:_<br>Allowed value: any string, but cannot be `null`|
| **Password**                    | Required for PI Web API endpoints   | `string`    | The password used to authenticate with a PI Web API OMF or EDS endpoint <br><br>PI server:_<br>Allowed value: any string<br>Default: `null`<br><br>_EDS:_<br>Allowed value: any string, but cannot be `null` |
| **ClientId**                    | Required for OCS endpoints          | `string`    | The client ID used for authentication with an OSIsoft Cloud Services OMF endpoint <br><br>Allowed value: any string<br>Default: `null` |
| **ClientSecret**                | Required for OCS endpoints          | `string`    | The client secret used for authentication with an OSIsoft Cloud Services OMF endpoint <br><br>Allowed value: any string<br>Default: `null`|
| **TokenEndpoint** | Optional for OCS endpoints | `string` | Retrieves an OCS token from an alternative endpoint <br><br>Allowed value: well-formed http or https endpoint string <br>Default value: `null` |
| **ValidateEndpointCertificate** | Optional                            | `boolean`      | Disables verification of destination security certificate. Use for testing only with self-signed certificates; OSIsoft recommends keeping this set to the default, true, in production environments. <br><br>Allowed value: `true` or `false`<br>Default value: `true`|

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
| api/v1/configuration/system/healthEndpoints      | GET       | Gets all configured health endpoints |
| api/v1/configuration/system/healthEndpoints      | DELETE    | Deletes all configured health endpoints |
| api/v1/configuration/system/healthEndpoints      | POST      | Adds an array of health endpoints or a single endpoint. Fails if any endpoint already exists |
| api/v1/configuration/system/healthEndpoints      | PUT       | Replaces all health endpoints. **Note:** Requires an array of endpoints |
| api/v1/configuration/system/healthEndpoints     | PATCH     | Allows partial updating of configured health endpoints<br>**Note:** The request must be an array containing one or more health endpoints. Each health endpoint in the array must include its *Id*.  |
| api/v1/configuration/system/healthEndpoints/*Id* | GET       | Gets configured health endpoint by *Id* |
| api/v1/configuration/system/healthEndpoints/*Id*| DELETE     | Deletes configured health endpoint by *Id* |
| api/v1/configuration/system/healthEndpoints/*Id* | PUT       | Updates or creates a new health endpoint with the specified *Id* |
| api/v1/configuration/system/healthEndpoints/*Id* | PATCH     | Allows partial updating of configured health endpoint by *Id* |

**Note:** Replace *Id* with the Id of the health endpoint.
