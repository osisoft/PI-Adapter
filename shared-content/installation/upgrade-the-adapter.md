---
uid: UpgradeTheAdapter
---

# Upgrade the adapter

When a new version of the adapter is released, you can upgrade it by running the new binaries.

## Windows upgrade

Complete the following steps to upgrade a PI adapter on a Windows computer:

1. Download the latest Windows .msi file from the [OSIsoft Customer Portal](https://customers.osisoft.com/s/products).

    **Note:** Customer login credentials are required to access the portal.

2. Run the .msi file.

3. Follow the setup wizard.

    You can change the installation folder or port number during upgrade. The default port number is `5590`.

4. Optional: To verify the upgrade, run the following `curl` command with the port number that you specified when completing the wizard:

   ```powershell
   curl -X GET "http://localhost:5590/api/v1/Diagnostics/ProductInformation"
   ```

   Upon successful upgrade, the JSON response lists the updated product version:

   ```json
   {
    "Application Version": "1.1.0.128",                 // upgraded version
    ".Net Core Version": ".NET Core 3.1.15",
    "Operating System": "Microsoft Windows 10.0.19041"
   }
   ```

   If you receive an error, wait a few seconds and try the script again. If the installation was successful, a JSON copy of the default system configuration is returned.

## Linux upgrade

Complete the following steps to upgrade a PI adapter on a Linux computer:

1. Download the appropriate Linux distribution file from the [OSIsoft Customer Portal](https://customers.osisoft.com/s/products).

    **Note:** Customer login credentials are required to access the portal.

2. Open a terminal session.

3. Change directory to the original install location and run the `sudo apt install` command.

    * **Linux ARM Debian:** `sudo apt install ./{AdapterName}_linux-arm.deb`
    * **Linux x64:** `sudo apt install ./{AdapterName}_linux-x64.deb`<br><br>

4. Optional: To verify the upgrade, run the following `curl` command with the port number that you specified:

   ```bash
   curl -X GET "http://localhost:5590/api/v1/Diagnostics/ProductInformation"
   ```

   Upon successful upgrade, the JSON response lists the updated product version:

   ```json
   {
    "Application Version": "1.1.0.128",                 // upgraded version
    ".Net Core Version": ".NET Core 3.1.15",
    "Operating System": "Microsoft Windows 10.0.19041"
   }
   ```

   If you receive an error, wait a few seconds and try the script again. If the installation was successful, a JSON copy of the default system configuration is returned.
