---
uid: SystemComponentsConfiguration1-3
---

# System components configuration

PI adapters use JSON configuration files in a protected directory on Windows and Linux to store configuration that is read on startup. While the files are accessible to view, OSIsoft recommends that you use REST or the EdgeCmd utility for any changes you make to the files.

As part of making adapters as secure as possible, any passwords or secrets that you configure are stored in encrypted form where cryptographic key material is stored separately in a secure location. If you edit the files directly, the adapter may not work as expected.

**Note:** You can edit any single component or facet of the system individually using REST, but you can also configure the system as a whole with a single REST call.

## Configure system components

The configuration of system components includes adding, updating, and deleting components.

### Add a system component

Complete the following steps to add a new component to the system:

**Note:** The examples in this procedure do not necessarily represent the adapter that your are currently using.

1. Using any text editor, create a file that contains the component to be added to the system in the JSON format.

    - For content structure, see [Examples](#examples).
    - For a table of all available parameters, see [System components parameters](#system-components-parameters).

    **Note:** The OmfEgress component is required for this initial release for adapters to run. You can add additional components, but only a single OmfEgress component is supported.

    The following example adds a Modbus TCP adapter:

      ```json
        {
          "ComponentId": "Modbus1",
          "ComponentType": "Modbus"
        }
      ```

    **Note:** A unique ComponentId is necessary for each component in the system. This example uses the ComponentId Modbus1 since it is the first Modbus TCP adapter to be added.

2. Save the file. For example, *AddComponent.json*.
3. Use any of the [Configuration tools](xref:ConfigurationTools1-3) capable of making HTTP requests to run either a `POST` or `PUT` command to their appropriate endpoint.

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    - **POST** endpoint: `http://localhost:5590/api/v1/configuration/system/components`

        Example using `curl`:

        **Note:** Run this command from the same directory where the file is located.

        ```bash
        curl -d "@AddComponent.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/system/components"
        ```

    - **PUT** endpoint: `http://localhost:5590/api/v1/configuration/system/components/<componentId>`

        Example using `curl`:

        **Note:** Run this command from the same directory where the file is located.

        ```bash
        curl -d "@AddComponent.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/components/Modbus1"
        ```

    After the curl command completes successfully, you can configure or use the new component.

### Update system components

Complete the following steps to update the components of the system, for example, by adding or deleting one or more adapter components.

1. Using any text editor, create a file that contains the current system components configuration. For information on how to retrieve the system components configuration, see [REST URLs](#rest-urls).

2. Delete or add components as you need.

    **Note:** You cannot delete the OmfEgress component.

3. Save the file. For example,  *UpdateComponents.json*

4. Use any of the [Configuration tools](xref:ConfigurationTools1-3) capable of making HTTP requests to run a `PUT` command with the contents of the file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/components`

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using `curl`:

    **Note:** Run this command from the same directory where the file is located.

    ```bash
    curl -d "@UpdateComponents.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/components"
    ```

### Delete a system component

Complete the following steps to delete a specific existing component:

1. Start any of the [Configuration tools](xref:ConfigurationTools1-3) capable of making HTTP requests.

2. Run a `DELETE` command to the following endpoint, replacing `<ComponentId>` with the ID of the component that you want to delete: `http://localhost:5590/api/v1/configuration/system/components/<ComponentId>/`

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using `curl`:

    **Note:** Run this command from the same directory where the file is located. <br>
    *Delete OpcUa1 component*
  
    ```bash
    curl -X DELETE "http://localhost:5590/api/v1/configuration/system/components/OpcUa1/"
    ```

    All the logs and configurations files for the deleted components are moved to the corresponding _logs/Removed_ or _Configuration/Removed_ folder.

## System components schema

The full schema definition for the system components configuration is in the `System_Components_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas`

Linux: `/opt/OSIsoft/Adapters/AdapterName/Schemas`

## System components parameters

You can configure the following parameters for system components:

| Parameters     | Required | Type    | Description |
| -------------- | -------- | --------| -------------|
| **ComponentId**    | Required |`string` | The ID of the component. It can be any alphanumeric string, for example, Modbus1. A properly configured ComponentID follows these rules:<br>Cannot contain leading or trailing space <br> Cannot use the following characters:<br> `>` `<` `/` `:` `?` `#` `[` `]` `@` `!` `$` `&` `*` `\` `"` `(` `)` `\\` `+` `,` `;` `=` `` \| `` `` ` `` `{` `}`<sup>1</sup>  |
| **ComponentType**  | Required |`string` | The type of the component, for example, Modbus. There are two types of components: OmfEgress and the adapter.<sup>1</sup> |
    
<sup>1</sup>**Note:** The OmfEgress component is required to run the adapter. Both its **ComponentId** and **ComponentType** are reserved and should not be modified.

## Examples

### Default system components configuration

The default _System_Components.json_ file for the System component contains the following information.

```json
[
  {
    "ComponentId": "OmfEgress",
    "ComponentType": "OmfEgress"
  }
]
```

### System components configuration with two adapter instances

**Note:** This is an example configuration; it does not necessarily include the adapter that you are currently using.

```json
[
  {
                "ComponentId": "Modbus1",
                "ComponentType": "Modbus"
            },
            {
                "ComponentId": "Modbus2",
                "ComponentType": "Modbus"
            },
            {
                "ComponentId": "OmfEgress",
                "ComponentType": "OmfEgress"
   }
]
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/system/components | GET | Retrieves  the system components configuration |
| api/v1/configuration/system/components | POST | Adds a new component to the system configuration |
| api/v1/configuration/system/components | PUT | Updates the system components configuration |
| api/v1/configuration/system/components/_componentId_ | DELETE | Deletes a specific component from the system components configuration |
| api/v1/configuration/system/components/_componentId_ | PUT | Creates a new component with the specified *componentId* in the system configuration
