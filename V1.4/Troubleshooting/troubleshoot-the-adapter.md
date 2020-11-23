---
uid: TroubleshootTheAdapter1-4
---

# Troubleshoot the adapter

To troubleshoot issues with the PI adapter, you can check the adapter's logs, read the related PI Web API and OCS documentation, and use Wireshark, as detailed in t he following sections. If you are unable to resolve issues with the adapter or need additional guidance, contact OSIsoft Technical Support.

**Note:** Make sure to check the troubleshooting information specific to your adapter.

## Check logs

1. Check both the System and the OmfEgress logs. By default, they are located here:
    Windows: `%ProgramData%\OSIsoft\Adapters\<AdapterName>\Logs`<br>
    Linux: `/usr/share/OSIsoft/Adapters/<AdapterName>/Logs`.
2. Optional: Change the log level of the adapter to receive more information and context. For more information, see [Logging configuration](xref:LoggingConfiguration).

### ASP .NET Core platform

This log provides information from the Kestrel web server that hosts the application. The log might be present in case EDS encounters heartbeat failures or if the adapter throughput is too high. When this happens, decrease the scan frequency or lower the amount of data selection items to spread the load among multiple adapters.

## PI Web API and OCS

Refer to the PI Web API and OCS documentation and their related troubleshooting information.

## Wireshark

Wireshark is a protocol-specific troubleshooting tool that supports all current adapter protocols. <br>Depending on the nature of the issue, use [Wireshark](https://www.wireshark.org/download.html) to capture traffic from the data source to the adapter or from the adapter to the OMF destination.

## Health and diagnostics egress to PI Web API

When the adapter sends health and diagnostics data to PI Web API, some conflicts may occur that are due to changes or perceived changes. For example, if you upgrade your adapter version and the PI points are not matching, you will see a `409 - Conflict` error message. However, data is continued to be sent and buffering only starts if no containers are created. To resolve the conflict, try the following:

1. Stop the adapter.
2. Delete the `Health` folder inside of the `Buffers` folder.
3. Stop PI Web API.
4. Delete the relevant adapter created AF structure.
5. Optional: Delete the associated health and diagnostics PI points on any or all PI Data Archives created by PI Web API.
6. Start PI Web API.
7. Start the adapter.
