---
uid: AdapterHealth
---

# Health

PI Adapters produce different kinds of health data that can be egressed to different health endpoints.

To egress health related data, you have to configure an adapter health endpoint first. See [Health endpoint configuration](xref:HealthEndpointConfiguration).

## Available health data

Dynamic data is sent every minute to configured health endpoints.

The following health data is available:

- [Device status](xref:DeviceStatus)
- [Next Health Message Expected](xref:NextHealthMessageExpected)

## AF structure

With a health endpoint configured to a PI server, you can use PI System Explorer to view the health of a given adapter. The element hierarchy is shown in the following image.

![Health data](../images/health-data.png)