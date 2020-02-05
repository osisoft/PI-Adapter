---
uid: HealthAndDiagnostics
---

# Health and Diagnostics

OSIsoft adapters produce various types of health data. You can use health data to ensure that your adapters are running properly and data is flowing to the configured OSIsoft OMF endpoints. For more information, see [Adapter health](xref:AdapterHealth).

OSIsoft adapters also produce diagnostic data. You can use diagnostic data to find more information about a particular adapter instance. Diagnostic data lives alongside the health data and you can egress it using a Health Endpoint and setting EnableDiagnostics = true. For more information, see [Adapter diagnostics](xref:AdapterDiagnostics).

The examples in the health and diagnostics topics use curl, a commonly available tool on both Windows and Linux. You can use the same operations with any programming language or tool that supports making REST calls. You can also configure OSIsoft adapters with the EdgeCmd utility. For more information, see [EdgeCmd utility](xref:EdgeCmdUtility). To validate successful configurations, you can accomplish data retrieval steps (GET commands) using a browser, if available on your device.

For more information on OSIsoft adapter configuration tools, see [Configuration tools](xref:ConfigurationTools).
