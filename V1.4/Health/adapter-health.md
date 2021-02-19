---
uid: AdapterHealth1-4
---

# Adapter health

PI Adapters produce different kinds of health data that can be egressed to different health endpoints.

To egress health related data, you have to configure an adapter health endpoint first. See [Health endpoint configuration](xref:HealthEndpointConfiguration1-4).

## Available health data

Dynamic data is sent every minute to configured health endpoints.

The following health data is available:

- [Device status](xref:DeviceStatus1-4)
- [Next Health Message Expected](xref:NextHealthMessageExpected1-4)

## AF structure

With a health endpoint configured to a PI server, you can use PI System Explorer to view the health of a given adapter. The element hierarchy is shown in the following image.

![Health data](../images/health-data.PNG)