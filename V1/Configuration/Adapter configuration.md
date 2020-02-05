---
uid: AdapterConfiguration
---

# Adapter configuration

You can configure OSIsoft System and adapter components entirely using a single call for replacing the existing configuration.

## Import configuration

### Import full adapter configuration using REST client

Complete the following to import the full adapter configuration using REST client:

1. Start any tool capable of making HTTP requests.
2. Execute a PUT command with the contents of the JSON file to the following endpoint: `http://localhost:5590/api/v1/configuration -d '{JSON file name}'`

	Example using curl:
	
	```cmdline
	curl -X http://localhost:5590/api/v1/configuration -d '{JSON file name}'
	```

	**Note:** In order for some of the adapter specific configurations to take effect, you have to restart the adapter.

	If the operation fails due to errors in the configuration, the count of the error and suitable error message(s) are returned in the result.

### REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/     | PUT       | Replaces the configuration for the entire adapter  |

### Sample configuration file for OPC UA

The following sample includes configuration of System components along with an OPC UA adapter. 

```json
{
    "OpcUa1": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataSource": {
            "EndpointUrl": "opc.tcp://OPCUAServerEndpoint/OPCUA/Server",
            "UseSecureConnection": false,
	    "StreamPrefix": "OPC_Prefix_",
            "UserName": null,
            "Password": null,
            "RootNodeIds": null,
            "IncomingTimestamp": "Source",
            "applyPrefixToStreamId": true
        },
        "DataSelection": [
            {
                "Selected": true,
                "Name": "Sawtooth",
                "NodeId": "ns=3;s=Sawtooth",
                "StreamId": "SawtoothStream"
            }
        ]
    },
    "System": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "HealthEndpoints": [
        ],
        "Components": [
            {
                "componentId": "Egress",
                "componentType": "OmfEgress"
            },
		    {
                "componentId": "OpcUa1",
                "componentType": "OpcUa"
            }
        ]
    },
    "Egress": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataEndpoints": [
            {
                "id": "WebAPI EndPoint",
                "endpoint": "https://PIWEBAPIServer/piwebapi/omf",
                "userName": "USERNAME",
                "password": "PASSWORD"
            },
            {
                "id": "OCS Endpoint",
                "endpoint": "https://OCSEndpoint/omf",
                "clientId": "CLIENTID",
                "clientSecret": "CLIENTSECRET"
            }
        ],
        "Buffering": {
            "BufferLocation": "C:\\ProgramData\\OSIsoft\\Adapters\\OpcUa\\OpcUa\\Buffers",
            "MaxBufferSizeMB": -1,
	    "EnableBuffering": true
        }
    }
}
```
 
