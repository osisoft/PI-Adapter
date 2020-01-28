---
uid: MessageLoggingConfiguration
---

# Message logging configuration

### Logger Schema Definition

Below is the full schema definition for logger configuration:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "LoggerConfiguration",
  "SchemaVersion": "1.0.0",
  "definitions": {
    "LogLevel": {
      "type": "string",
      "description": "",
      "x-enumNames": [
        "Trace",
        "Debug",
        "Information",
        "Warning",
        "Error",
        "Critical",
        "None"
      ],
      "enum": [
        "Trace",
        "Debug",
        "Information",
        "Warning",
        "Error",
        "Critical",
        "None"
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
      "$ref": "#/definitions/EdgeConfigurationBase"
    },
    {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "LogLevel": {
          "$ref": "#/definitions/LogLevel"
        },
        "LogFileSizeLimitBytes": {
          "type": [
            "integer",
            "null"
          ],
          "format": "int64"
        },
        "LogFileCountLimit": {
          "type": [
            "integer",
            "null"
          ],
          "format": "int32"
        }
      }
    }
  ]
}
```
