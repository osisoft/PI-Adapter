@@ -0,0 +1,41 @@
---
uid: AdapterDiagnostics
---

# Adapter Diagnostics

OSIsoft Adapters produce diagnostic data which can be used to find more information about a particular adapter instance. This data lives alongside the health data and can be egressed using a Health Endpoint and setting EnableDiagnostics = true. 

For configuration of health endpoints, see </Health/Health.md>.

## AF Hierarchy

When PI Web API is used as a health endpoint, an AF hierarchy is created containing both the diagnostics and health data and metadata. Currently, OSIsoft Cloud Services does not have a way to store static metadata and will only contain the dynamic streams. For more information or to see an example of this hierarchy, see </Health/Health.md>.

## Stream Count

The stream count indicates the number of streams and associated types being produced and sent data for a particular Adatper instance.

| Type         | Property |  Description     |
|--------|--------------|-----------------------------------|
| string | Timestamp | Timestamp of event |
| int | StreamCount | Overall number of streams created by the adapter instance |
| int | TypeCount | Overall number of types created by the adapter instance |

## IO Rate

The IO Rate indicates the running average number of streams per second being produced by an adapter instance.

| Type         | Property |  Description     |
|--------|--------------|-----------------------------------|
| string | Timestamp | Timestamp of event |
| double | IORate | Average data rate (streams/second) |

## Error Rate

The error rate indicates the average number of errors per second occurring for a particular adapter instance.

| Type         | Property |  Description     |
|--------|--------------|-----------------------------------|
| string | Timestamp | Timestamp of event |
| double | ErrorRate | Average error rate (streams/second)