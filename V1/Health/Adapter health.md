---
uid: AdapterHealth
---

# Adapter health

PI Adapters produce different kinds of health data that can be egressed to different health endpoints. 

## Available health data

Dynamic data is sent every minute to configured health endpoints.

The following health data is available:

- [Device status](xref:DeviceStatus)
- [Next Health Message Expected](xref:NextHealthMessageExpected)

## Health endpoint differences

Two OMF endpoints are currently supported for adapter health data:

- PI Web API
- OSIsoft Cloud Services

There are a few differences in how these two systems treat the associated health data.

- PI Web API parses the information and sends it to configured PI servers for the OMF endpoint. The static data is used to create a hierarchy on a PI AF server similar to the following example:

  ![AdapterHealthAFHierarchy](../images/AdapterHealthAFHierarchy.PNG)

  The dynamic health data is time-series data that is stored in PI points on a PI Data Archive. You can see it in the AF hierarchy as PI point data reference attributes.

- OSIsoft Cloud Services does not currently provide a way to store the static metadata. For OCS-based adapter health endpoints, only the dynamic data is stored. Each value is its own stream with the timestamp property as the single index.
