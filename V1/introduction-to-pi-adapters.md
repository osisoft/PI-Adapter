---
uid: IntroductionToPIAdapters
---

# Introduction to PI Adapters

PI Adapters is an edge data collection technology that provides access to time-series data previously isolated on remote assets or in secondary networks. Available for Windows and Linux devices, PI Adapters pull real-time data from IIoT gateways and sensor-enabled equipment and securely route the data to EDS for additional edge applications, to on-premises PI Server, or to OSIsoft's cloud-hosted data management service OCS.

PI Adapters offer the following generic capabilities:

- Connection to inbound data sources from common industrial protocols
- Real-time data transfer to PI Server, OCS, and EDS with optional data filtering to manipulate data on the outbound side
- Buffering to overcome network and system disruptions
- Administration functions for simplified management and scalable installation and configuration

## Capabilities in detail

The following capabilities are available for every PI Adapter. A specific PI Adapter might or might not include additional capabilities such as network proxy support or data source auto discovery.

### Inbound data

PI Adapters provide connections to a variety of inbound data sources from common industrial protocols. Currently available protocols include OPC UA, Modbus TCP, DNP3, and BACnet. Protocols in progress include MQTT, Azure Event Hubs, RDBMS, and Structured Data Files.

The optional stream metadata capability provides the option to set the amount of metadata to provide meaningful metadata that differs for every adapter type.

For more information, see [Data source configuration](xref:DataSourceConfiguration) and [Data selection configuration](xref: DataSelectionConfiguration).

### Data transfer

PI Adapters allow you to transfer real-time data to PI Server, OSIsoft Cloud Services (OCS), and Edge Data Store (EDS). The data filtering capability improves the configuration flexibility by manipulating data on the outbound side and minimizes network bandwidth consumption through exception reporting capabilities.

For more information, see [Egress configuration](xref:EgressConfiguration).

### Buffering

PI Adapters incorporate robust data collection through buffering for data egressed from the adapter to egress endpoints or health endpoints. Buffering helps to overcome network and system disruptions that often result in data loss.

For more information, see [Buffering configuration](xref:BufferingConfiguration).

### Administration

PI Adapters provide administrative functions such as starting and stopping of an adapter or ingress component, or deleting an adapter component. Administrative functions simplify management and make installation and configuration scalable.

For more information, see [Administration](xref:Administration).
