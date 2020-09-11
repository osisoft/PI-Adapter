---
uid: AdapterMetadata1-3
---

# Adapter metadata

If the metadataLevel is set to `Low` or higher in the [General configuration](xref:GeneralConfiguration1-3), adapter streams created by the ingress components include the following metadata:

```code
  Datasource: {ComponentId}
  AdapterType: {ComponentType}
```

`ComponentId` corresponds to the adapter components' data source configured in the [Components configuration](xref:SystemComponentsConfiguration1-3). `ComponentType` corresponds to the adapter type. For example, Modbus or OpcUa.

## Metadata for health and diagnostics streams

If you configure a health endpoint and enable metadata, they are included in the health streams ([Device status](xref:DeviceStatus1-3) and [Next health message expected](xref:NextHealthMessageExpected1-3)) together with `ComponentId` and `ComponentType`.

If you enable diagnostics in [General configuration](xref:GeneralConfiguration1-3), metadata are included in the diagnostics streams ([Stream count](xref:StreamCount1-3), [IO rate](xref:IORate1-3), [Error rate](xref:ErrorRate1-3)) together with `ComponentId` and `ComponentType`.

The adapter may also send its own stream metadata not including health and diagnostics streams. For more information about what custom metadata is included in each stream, see the user guide for your adapter.

**Note:**

- Metadata is only sent for streams created by the ingress components.
- Currently, the only endpoint that persists sent metadata is OCS (OSIsoft Cloud Services).
