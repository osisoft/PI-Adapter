---
uid: GeneralConfiguration
---

# General configuration

You can configure PI adapters to produce and store diagnostics data at a designated health endpoint, and to send metadata for created streams.
For more information about available diagnostics data, see [Adapter diagnostics](xref:AdapterDiagnostics) and [Egress diagnostics](xref:EgressDiagnostics).
For more information about available metadata and what metadata are sent per metadata level, see [Adapter Metadata](xref:AdapterMetadata).

## Configure general

Complete the following steps to configure diagnostics and metadata levels. Use the `PUT` method in conjunction with the `http://localhost:5590/api/v1/configuration/system/general` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for diagnostics and metadata levels into the file.

    For sample JSON, see [Example](#example).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [General parameters](#general-parameters).

4. Save the file. For example, as `ConfigureGeneral.json`.

5. Open a command line session. Change directory to the location of `ConfigureGeneral.json`.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the general configuration.

    ```bash
    curl -d "@ConfigureGeneral.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/general"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * For a list of other REST operations you can perform, like updating or replacing a general configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

## General schema

The full schema definition for the general configuration is in the `System_General_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\<AdapterName>\Schemas`

Linux: `/opt/OSIsoft/Adapters/<AdapterName>/Schemas`

## General parameters

The following parameters are available for configuring general:

| Parameter             | Required | Type    | Description |
| ---------             | -------- | ------- | ----------- |
| **EnableDiagnostics** | Optional | `boolean` | Determines if diagnostics are enabled<br><br>Allowed value: `true` or `false`<br>Default value: `true`<br>|
| **MetadataLevel** | Optional | `reference` | Defines amount of metadata sent to OMF endpoints.<br><br> Allowed value: `None`, `Low`, `Medium`, and `High`<br> Default value: `Medium` |

## Example

### Retrieve the general configuration

Example using `curl`:

```bash
curl -X GET "http://localhost:{port}/api/v1/configuration/system/general"
```

Sample output:

```code
{
  "EnableDiagnostics": true,
  "MetadataLevel": "Medium"
}
```

## REST URLs

| Relative URL                            | HTTP verb | Action                                          |
| --------------------------------------- | --------- | ----------------------------------------------- |
| api/v1/configuration/system/General  | GET       | Gets the general configuration             |
| api/v1/configuration/system/General  | PUT       | Replaces the existing general configuration |
| api/v1/configuration/system/General  | PATCH       | Allows partial updating of general configuration
