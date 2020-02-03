---
uid: StartAndStopAnAdapter
---

# Start and stop an adapter

By default, all currently configured OSIsoft adapters are started.

## Start an OSIsoft adapter

Complete the following to start an individual OSIsoft adapter:

1. Start any configuration tool capable of making HTTP requests.
2. Execute a POST command to the following endpoint, replacing `<OSIsoft adapterId>` with the adapter that you want to start: `http://localhost:5590/api/v1/administration/OSIsoft adapterId/Start`
    
    Example **Start the OpcUa1 adapter** using curl:

    ```bash
    curl -v -d "" http://localhost:5590/api/v1/Administration/OpcUa1/Start
    ```

    An HTTP status 204 message indicates success.

## Stop an OSIsoft adapter

Complete the following to stop an individual OSIsoft adapter:

1. Start any configuration tool capable of making HTTP requests.
2. Execute a POST command to the following endpoint, replacing `<OSIsoft adapterId>` with the adapter that you want to stop: `http://localhost:5590/api/v1/administration/OSIsoft adapterId/Stop`

    Example **Stop the Modbus1 adapter** using cURL:

    ```bash
    curl -v -d "" http://localhost:5590/api/v1/Administration/Modbus1/Stop
    ```

    An HTTP status 204 message indicates success.
