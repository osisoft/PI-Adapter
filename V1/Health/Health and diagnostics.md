---
uid: HealthAndDiagnostics
---

# Health and Diagnostics

PI Adapters produce various types of health data. You can use health data to ensure that your adapters are running properly and that data flows to the configured OMF endpoints. For more information on available health data, see [Adapter health](xref:AdapterHealth).

PI Adapters also produce diagnostic data. You can use diagnostic data to find more information about a particular adapter instance. Diagnostic data lives alongside the health data and you can egress it using a Health Endpoint and setting `EnableDiagnostics` to`true`. For more information on available diagnostics data, see [Adapter diagnostics](xref:AdapterDiagnostics).
