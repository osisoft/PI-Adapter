---
uid: Health
---

# Adapter Health

Adapters produce various types of health data. This information can be used to ensure that your adapters are running properly and data is flowing to the configured OSIsoft OMF endpoints. This section details how to configure your adapters so that this health data is produced and stored at a designated endpoint as well as what types of health data are available.

## Configure Health Endpoints

A health endpoint designates an OSIsoft OMF endpoint where adapter health information should be sent. Multiple health endpoints can be configured. The configuration for a health endpoint is essentially the same as the configuration for a typical OMF egress endpoint. 

Table 1. Configuration parameters for adapter health endpoints

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| **Id**                          | Optional                            | string    | Used to uniquely identify the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. |
| **Endpoint**                    | Required                            | string    | The URL of the OMF endpoint to receive this health data. |
| **ClientId**                    | Required for OCS endpoints          | string    | The Client Id used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoints          | string    | The Client Secret used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **Username**                    | Required for PI Web API endpoints   | string    | The username used to authenticate with a PI Web API OMF endpoint. |
| **Password**                    | Required for PI Web API endpoints   | string    | The password used to authenticate with a PI Web API OMF endpoint. |
| **BufferingEnabled**            | Optional                            | bool      | Enables or disables buffering to this endpoint. By default, buffering is enabled ("true"). |
| **ValidateEndpointCertificate** | Optional                            | bool      | Used to disable verification of destination security certificate. Use for testing only with self-signed certificates; OSIsoft recommends setting this to true in production environments. Defaults to true. |

## Available Health Data
Each individual adapter data component produces a few different pieces of health data. Dynamic data is sent every minute to configured health endpoints.

### Device Status
The device status indicates the health of this component and whether or not it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type. During healthy steady-state operation, a value of "Good" is expected.

| Property                          | Type                                 | Description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                          | string                               | Timestamp of the event.        |
| **DeviceStatus**                  | string                               | The value of the DeviceStatus. |

The possible statuses are:

| Status                            | Meaning                               |
|-----------------------------------|---------------------------------------|
| **Good**                          | The component is connected to the data source and collecting data. |
| **ConnectedNoData**               | The component is connected to the data source but is not receiving data from it. |
| **AttemptingFailover**            | The adapter is attempting to failover. |
| **Starting**                      | The component is currently in the process of starting up and is not yet connected to the data source. |
| **DeviceInError**                 | The component encountered an error either while connecting to the data source or attempting to collect data. |
| **Shutdown**                      | The component is either in the process of or has finished shutting down. |

### Next Health Message Expected
This property is similar to a heartbeat. A new value for NextHealthMessageExpected will be sent by an individual adapter data component on a periodic basis while it is functioning properly. This value will be a timestamp indicating when the next value should be received. When monitoring, if the next value is not received by the indicated time, this likely means an issue has arisen. This could be an issue with the adapter, adapter component, network connection between the health endpoint and the adapter, etc.

| Property                          | Type                                 | Description                            |
|-----------------------------------|--------------------------------------|----------------------------------------|
| **Time**                          | string                               | Timestamp of the event.                |
| **NextHealthMessageExpected**     | string                               | Timestamp when next value is expected. |

## Health Endpoint Differences - PI Web API vs. OSIsoft Cloud Services

As noted above, currently two different OMF endpoints are supported for adapter health data - That hosted by PI Web API and that hosted by OSIsoft Cloud Services. There are a few differences in how these two systems treat the associated health data. 

PI Web API parses the information and sends it configured PI Systems for the OMF endpoint. The static data is used to create a hierarchy on a PI AF server similar to the following:

[AdapterHealthAFHierarchy]: https://github.com/osisoft/OSIsoft-Adapter/tree/master/V1/Adapter%20administration/AdapterHealthAFHierarchy.png "Adapter Health AF Hierarchy"

The dynamic health data is actually time-series data that is stored in PI points on a PI Data Archive and can be seen in the AF hierarchy as PI Point Data Reference attributes.

OSIsoft Cloud Services currently does not have a way to store the static metadata. For OCS-based adapter health endpoints, only the dynamic data will be stored. Each value will be its own stream with the timestamp property as the single index.