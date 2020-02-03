---
uid: HealthAndDiagnosticsConfiguration
---

# Health and diagnostics configuration

### Diagnostics Schema Definition

Below is the full schema definition for the system components configuration.

File: *System_Diagnostics_schema.json*

```c#
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "EdgeDiagnosticsConfiguration",
  "SchemaVersion": "1.0.0",
  "definitions": {
    "EdgeConfigurationBase": {
      "type": "object",
      "x-abstract": true,
      "additionalProperties": false
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/EdgeConfigurationBase"
    },
    {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "EnableDiagnostics": {
          "type": "boolean"
        }
      }
    }
  ]
}
```

### Health Endpoints Schema Definition

Below is the full schema definition for the health endpoints configuration.

File: *System_HealthEndpoints_schema.json*

```c#
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "OmfHealthEndpointConfiguration",
  "SchemaVersion": "1.1.0",
  "definitions": {
    "EndpointConfigurationBase": {
      "allOf": [
        {
          "$ref": "#/definitions/EdgeConfigurationBase"
        },
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "Endpoint"
          ],
          "properties": {
            "Id": {
              "type": [
                "null",
                "string"
              ]
            },
            "Endpoint": {
              "type": "string",
              "minLength": 1
            },
            "UserName": {
              "type": [
                "null",
                "string"
              ]
            },
            "Password": {
              "type": [
                "null",
                "string"
              ]
            },
            "ClientId": {
              "type": [
                "null",
                "string"
              ]
            },
            "ClientSecret": {
              "type": [
                "null",
                "string"
              ]
            },
            "TokenEndpoint": {
              "type": [
                "null",
                "string"
              ]
            },
            "ValidateEndpointCertificate": {
              "type": "boolean"
            }
          }
        }
      ]
    },
    "EdgeConfigurationBase": {
      "type": "object",
      "x-abstract": true,
      "additionalProperties": false
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/EndpointConfigurationBase"
    },
    {
      "type": "object",
      "additionalProperties": false
    }
  ]
}
```