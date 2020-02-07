---
uid: SystemComponentsConfiguration
---

# System components configuration

OSIsoft adapters use JSON configuration files in a protected directory on Windows and Linux to store configuration that is read on startup. While the files are accessible to view, OSIsoft recommends that you use REST or the edgecmd command line tool for any changes you make to the files. 

As part of making adapters as secure as possible, any passwords or secrets that you configure are stored in encrypted form (with cryptographic key material stored separately in a secure location.) If you edit the files directly, the adapter may not work as expected.

**Note:** You can edit any single component or facet of the system using REST, but also configure the system as a whole with a single REST call.

## Configure system components

The default _System_Components.json_ file for the System component contains the following information. 

```json
[
  {
    "ComponentId": "OmfEgress",
    "ComponentType": "OmfEgress"
  }
]
```

 **Note:** The OmfEgress component is required for this initial release for adapters to run. You can add additional components if you want, but only a single OmfEgress component is supported. 

Complete the following to add a new component:

1. Using any text editor, create a file that contains the system components configuration in JSON form.
	- For content structure, see [System components example](#system-components-example).

	The following example adds a Modbus TCP adapter. 

    ```json
      {
        "ComponentId": "Modbus1",
        "ComponentType": "Modbus"
      }
    ```
    
    **Note:** A unique ComponentId is necessary for each component in the system. This example uses the ComponentId Modbus1 since it is the first Modbus TCP adapter:

2. Save the file, for example as *AddComponent.json*.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/components`

	Example using curl (run this command from the same directory where the file is located):

   	```bash
   	curl -i -d "@AddComponent.json" -H "Content-Type: application/json" http://localhost:5590/api/v1/configuration/system/components
   	```

	After the curl command completes successfully, you can configure or use the new component.

### Delete a system component

Complete the following to delete an existing component:

1. Start any tool capable of making HTTP requests.
2. Execute a DELETE command to the following endpoint, replacing `<ComponentId To Delete>` with the ID of the component that you want to delete, for example OpcUa1: `http://localhost:5590/api/v1/configuration/system/components/<ComponentId_To_Delete>/`

	Example using curl:

	```bash
	curl -X DELETE http://localhost:5595/api/v1/configuration/system/components/{ComponentId_To_Delete}/
	```

	All the logs and configurations files for the deleted components will be moved to the corresponding _logs/Removed_ or _Configuration/Removed_ folder.
	
## System components schema

The following table defines the basic behavior of the *System_Components_schema.json* file.

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             |

The full schema definition for the system components configuration is in the *System_Components_schema.json* located here:

Windows: *%Program Files%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*


## System components parameters

The following parameters are available for configuring system components.

| Parameters     | Required | Type    | Nullable | Description |
| -------------- | -------- | --------| ---------|-------------|
| **ComponentId**    | Required |`string` | Yes      | The ID of the component. It can be any alphanumeric string, for example OmfEgress.|
| **ComponentType**  | Required |`string` | Yes      | The type of the component, for example OmfEgress. There are two types of components: OmfEgress and the adapter. |

## System components example

```json
[
  {
                "componentId": "Modbus1",
                "componentType": "Modbus"
            },
            {
                "componentId": "Modbus2",
                "componentType": "Modbus"
            },
            {
                "ComponentId": "OmfEgress",
                "ComponentType": "OmfEgress"
   }
]
```
