---
uid: StartAndStopAnAdapter
---

# Start and stop an adapter

Complete the procedure appropriate for your operating system to start or stop an adapter service:

## Windows

1. Open Windows services.

2. Select **PI Adapter for _AdapterName_**, for example, PI Adapter for Modbus.

3. Depending on whether your adapter is running or not, click either **Start** or **Stop**.

## Linux

1. Open command line.

2. Depending on whether your adapter is running or not, type one of the following commands:

    Example:

    **Start** PI Adapter for OPC UA

    ```cmdline
    systemctl start PI Adapter for OPC UA
    ```

    Example:

    **Stop** PI Adapter for Modbus TCP
  
      ```cmdline
      systemctl stop PI Adapter for Modbus
      ```
  
3. Press Enter.
