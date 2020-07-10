---
uid: EgressEndpointsConfiguration
---

# Egress endpoints configuration

Adapters can egress dynamic data to destinations that you supply through OMF. OSIsoft Cloud Services (OCS), PI servers through PI Web API, and Edge Data Store (EDS) are supported destinations.

An egress endpoint represents a destination to which data is sent. You can specify multiple endpoints. Every egress endpoint is run independently of all other egress endpoints and is expected to accept OMF messages. An egress endpoint is comprised of the properties specified under [Egress endpoint parameters](#egress-endpoint-parameters).

## Configure egress endpoints

**Note:** You cannot add egress configurations manually because some parameters are encrypted when stored to disk. You must use the REST endpoints to add or edit egress configuration. For additional endpoint configurations, see [REST URLs](#rest-urls).

Complete the following steps to configure egress endpoints:

1. Using any text editor, create a file that contains one or more egress endpoints in the JSON format.
    - For content structure, see [Examples](#examples).
    - For a table of all available parameters, see [Egress endpoint parameters](#egress-endpoint-parameters).

2. Save the file. For example, _OmfEgress_DataEndpoints.json_.

3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests and run the appropriate command with the contents of the file to the following endpoint: `http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/`

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    Examples using `curl`:

    **Note:** Run the commands from the same directory where the file is located.

    - _Add endpoints_

        ```bash
        curl -d "@OmfEgress_DataEndpoints.json" -H "Content-Type: application/json" -X POST    "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints"
        ```

        ```bash
        curl -d "@OmfEgress_DataEndpoints.json" -H "Content-Type: application/json" -X PUT   "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/{Id}"
        ```

    - _Delete an endpoint_

        ```bash
        curl -X DELETE "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/{Id}"
        ```

    - _Update an endpoint_

        ```bash
        curl -d "@OmfEgress_DataEndpoints.json" -H "Content-Type: application/json" -X UPDATE     "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/{Id}"
        ```

    - _View endpoints_

        ```bash
        curl -X GET "http://localhost:5590/api/v1/configuration/OmfEgress/DataEndpoints"
        ```

## Egress endpoint configuration schema

The full schema definition for the egress endpoint configuration is in the `OmfEgress_DataEndpoints_schema.json`  file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas`

Linux: `/opt/OSIsoft/Adapters/AdapterName/Schemas`

## Egress endpoint parameters

The following parameters are available for configuring egress endpoints:

| Parameter                       | Required                  | Type      | Description                                        |
|---------------------------------|---------------------------|-----------|-------------|
| **Id**                          | Optional                  | `string`    | Unique identifier<br><br>Allowed value: any string identifier<br>Default value: new GUID |
| **Endpoint**                    | Required                  | `string`    | Destination that accepts OMF v1.1 messages. Supported destinations include OCS, PI Server, and EDS.<br><br>Allowed value: well-formed http or https endpoint string<br>Default: `null` |
| **Username**                    | Required for PI server and EDS endpoint  | `string`    | Basic authentication to the PI Web API OMF or EDS endpoint <br><br>_PI server:_<br>Allowed value: any string<br>Default: `null`<br><br>_EDS:_<br>Allowed value: `eds` |
| **Password**                    | Required for PI server and EDS endpoint  | `string`    | Basic authentication to the PI Web API OMF or EDS endpoint <br><br>_PI server:_<br>Allowed value: any string<br>Default: `null`<br><br>_EDS:_<br>Allowed value: `eds` |
| **ClientId**                    | Required for OCS endpoint | `string`    | Authentication with the OCS OMF endpoint <br><br>Allowed value: any string<br>Default: `null`|
| **ClientSecret**                | Required for OCS endpoint | `string`    | Authentication with the OCS OMF endpoint <br><br>Allowed value: any string<br>Default: `null`|
| **TokenEndpoint**               | Optional for OCS endpoint | `string`    | Retrieves an OCS token from an alternative endpoint <br><br>Allowed value: well-formed http or https endpoint string <br>Default value: `null` |
| **ValidateEndpointCertificate** | Optional                  | `boolean`   | Disables verification of destination certificate. **Note:** Only use for testing with self-signed certificates. <br><br>Allowed value: `true` or `false`<br>Default value: `true` |

## Examples

The following examples are valid egress configurations:

### Egress data to OCS

```json
[{
     "Id": "OCS",
     "Endpoint": "https://<OCS OMF endpoint>",
     "ClientId": "<clientid>",
     "ClientSecret": "<clientsecret>"
}]
```

### Egress data to PI Web API

```json
[{
     "Id": "PI Web API",
     "Endpoint": "https://<pi web api server>/piwebapi/omf/",
     "UserName": "<username>",
     "Password": "<password>"
}]
```

### Egress data to EDS

```json
[{
     "Id": "EDS",
     "Endpoint": "http://localhost:<port_number>/api/v1/tenants/default/namespaces/default/omf",
     "UserName": "eds",
     "Password": "eds"
}]
```


## REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/omfegress/DataEndpoints      | GET       | Gets all configured egress endpoints |
| api/v1/configuration/omfegress/DataEndpoints      | DELETE    | Deletes all configured egress endpoints |
| api/v1/configuration/omfegress/DataEndpoints      | POST      | Adds an array of egress endpoints or a single endpoint. Fails if any endpoint already exists |
| api/v1/configuration/omfegress/DataEndpoints      | PUT       | Replaces all egress endpoints |
| api/v1/configuration/omfegress/DataEndpoints      | PATCH     | Allows partial updating of configured endpoints.<br>**Note:** The request must be an array containing one or more endpoints. Each endpoint in the array must include its *Id*. |
| api/v1/configuration/omfegress/DataEndpoints/{Id} | GET       | Gets configured endpoint by *Id* |
| api/v1/configuration/omfegress/DataEndpoints/{Id} | DELETE    | Deletes configured endpoint by *Id* |
| api/v1/configuration/omfegress/DataEndpoints/{Id} | PUT       | Updates or creates a new endpoint with the specified *Id* |
| api/v1/configuration/omfegress/DataEndpoints/{Id} | PATCH     | Allows partial updating of configured endpoint by *Id* |

## Egress execution details

- After configuring an egress endpoint, egress is immediately run for that endpoint. Egress is handled individually per configured endpoint. On first execution, types and containers are egressed. After that only new or changed types or containers are egressed. Type creation must be successful in order to create containers. Container creation must be successful in order to egress data.
- If you delete an egress endpoint, data flow immediately stops for that endpoint. Buffered data in a deleted endpoint is permanently lost.
- Type, container, and data items are batched into one or more OMF messages when egressing. As per the requirements defined in OMF, a single message payload will not exceed 192KB in size. Compression is automatically applied to outbound egress messages. On the egress destination, failure to add a single item results in the message failing. Types, containers, and data are egressed as long as the destination continues to respond to HTTP requests.
