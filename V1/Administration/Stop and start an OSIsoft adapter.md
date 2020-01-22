---
uid: StopAndStartAnOSIsoftAdapter
---

# Stop and start an OSIsoft adapter

You can stop and start OSIsoft adapters. By default, all currently configured OSIsoft adapters are started and remain running until the product shuts down.

## Stop an OSIsoft adapter

- To stop an individual OSIsoft adapter, use any REST client and make a request using the following:

    ```http
    Method: POST
    Endpoint: http://localhost:5590/api/v1/administration/OSIsoft adapterId/Stop
    Header: Content-Type application/json
    ```

    Example using cURL:

    ```bash
    curl -v -d "" http://localhost:5590/api/v1/Administration/OSIsoft adapterId/Stop
    ```

    **Note:** Replace _OSIsoft adapterId_ with the ID of the OSIsoft adapter you want to stop.

    An HTTP status 204 message indicates success.

## Start an OSIsoft adapter

- To start an individual OSIsoft adapter, use any REST client and make a request using the following:

    ```http
    Method: POST
    Endpoint: http://localhost:5590/api/v1/administration/OSIsoft adapterId/Start
    Header: Content-Type application/json
    ```

    Example using cURL:

    ```bash
    curl -v -d "" http://localhost:5590/api/v1/Administration/OSIsoft adapterId/Start
    ```

    **Note:** Replace _OSIsoft adapterId_ with the ID of the OSIsoft adapter you want to start.

    An HTTP status 204 message indicates success.
