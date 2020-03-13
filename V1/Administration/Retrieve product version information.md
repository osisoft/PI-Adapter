---
uid: RetrieveProductVersionInformation
---

# Retrieve product version information

The product version information includes the application version, the version of the underlying .NET Core Framework, and the operating system that the adapter is running on.

Complete the following procedure to retrieve the product version information of an OSIsoft adapter:

1. Start any configuration tool capable of making HTTP requests.
2. Execute a GET command to the following endpoint: `http://localhost:5590/api/v1/Diagnostics/ProductInformation`

   **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

   Example using curl **Get product information for adapter hosted on port 5590**:

   ```bash
   curl -d "" -X GET "http://localhost:5590/api/v1/Diagnostics/ProductInformation
   ```

   Example result:

    ```code
    {
        "Application Version": "1.1.0.30",
        ".Net Core Version": ".NET Core 3.1.1",
        "Operating System": "Microsoft Windows 10.0.17134"
    }
    ```
