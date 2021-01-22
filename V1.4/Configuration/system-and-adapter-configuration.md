---
uid: SystemAndAdapterConfiguration1-4
---

# System and adapter configuration

You can configure the system component and adapter component together using a single file.

## Change system and adapter configuration

Change the system and adapter configuration by importing the JSON file using a REST client:

1. Using any text editor, create a file that contains the System and adapter configuration in the JSON format.

    - For content structure, see [Example](#example).

2. Save the file. For example,  `ConfigureSystemAndAdapter.json`.

3. Use any of the [Configuration Tools](xref:ConfigurationTools1-4) capable of making HTTP requests and run a PUT command with the contents of the file to the following endpoint: `http://localhost:5590/api/v1/configuration`

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using `curl`:

    **Note:** Run this command from the same directory where the file is located.

    ```bash
    curl -d "@ConfigureSystemAndAdapter.json" -H "Content-Type: application/json" -X  PUT "http://localhost:5590/api/v1/configuration"
    ```

    **Note:** In order for some of the adapter specific configurations to take effect, you have to restart the adapter.

    If the operation fails due to errors in the configuration, the count of the error and suitable error messages are returned in the result.

## Example

For an example system and adapter configuration, see the Configuration examples topic.

## REST URLs

| Relative URL          | HTTP verb | Action                                            |
| --------------------- | --------- | ------------------------------------------------- |
| api/v1/configuration/ | PUT       | Replaces the configuration for the entire adapter |
