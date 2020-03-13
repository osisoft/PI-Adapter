---
uid: EgressDiagnostics
---

# Egress diagnostics

The Egress component of the adapter produces the following diagnostics streams.

## IO rate

The Diagnostics.Egress.IORate dynamic type includes these values, which are logged in a stream with the id {machineName}.{serviceName}.OmfEgress.{EndpointId}.IORate. IO rate includes only sequential data successfully sent to an egress.

| Property  | Type   | Description                                            |
| --------- | ------ | -------------------------------------------------------|
| timestamp | `string` | Timestamp of event                                   |
| IORate    | `double` | 1-minute rolling average of data rate (streams/second)|
