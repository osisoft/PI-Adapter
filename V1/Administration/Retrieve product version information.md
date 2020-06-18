---
uid: RetrieveProductVersionInformation
---

# Retrieve product version information

The product version information includes the application version, the version of the underlying .NET Core framework, and the operating system that the adapter is running on.

Complete the following steps to retrieve the product version information of a PI adapter:

1. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests.
2. Run a `GET` command to the following endpoint: `http://localhost:5590/api/v1/Diagnostics/ProductInformation`

   **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

   Example using `curl`:

   **Get product information for adapter hosted on port 5590**

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
