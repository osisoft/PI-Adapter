---
uid: StartAndStopAnAdapter1-4
---

# Start and stop an adapter

Complete the procedure appropriate for your operating system to start or stop an adapter service:

## Windows

1. Open Windows services.

2. Select **PI Adapter for _AdapterName_**, for example, PI Adapter for Modbus.

    **Note:** This is an example; it does not necessarily represent the adapter that you are currently using.

3. Depending on whether your adapter is running or not, click either **Start** or **Stop**.

## Linux

1. Open command line.

2. Depending on whether your adapter is running or not, type one of the following commands:

    Example:

    _Start_ PI Adapter for OPC UA

    ```cmdline
    sudo systemctl start pi.adapter.opcua
    ```

    Example:

    _Stop_ PI Adapter for Modbus TCP
  
      ```cmdline
      sudo systemctl stop pi.adapter.modbus
      ```

      **Note:** These commands are examples; they do not necessarily represent the adapter that you are currently using.
  
3. Press Enter.
