---
uid: AdapterMetadata
---

# Adapter metadata

The adapter streams will have metadata if the option to send metadata is set to true in the [general configuration](xref:GeneralConfiguration). If enabled, all created streams created by the ingress components will have the included metadata. 
```code
  Datasource: {ComponentId}
  AdapterType: {ComponentType}
```

The componentId corresponds to the adapter components' componentIds configured in the [components configuration](xref:SystemComponentsConfiguration). The ComponentType corresponds to the adapter's type (e.g. Modbus, OpcUa).

If a health endpoint is configured and metadata is enabled, metadata will also be included in the health streams with the same metadata as above.

If EnableDiagnostics is also set to true in [general configuration](xref:GeneralConfiguration), metadata will also be included in the diagnostics streams with the same metadata as above.

The adapter may also send its own stream metadata. See the user guide for your adapter to see what custom metadata is included in each stream.

Note: Metadata is only sent for streams created by the ingress components.
Note: Currently, the only endpoint that persists sent metadata is OCS (OSIsoft Cloud Services).

![Metadata in OCS](../images/Metadata.png)