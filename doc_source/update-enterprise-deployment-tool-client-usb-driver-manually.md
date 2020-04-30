# Update the AppStream 2\.0 Enterprise Deployment Tool, Client, and USB Driver Manually<a name="update-enterprise-deployment-tool-client-usb-driver-manually"></a>

By default, the AppStream 2\.0 client and USB driver are updated automatically when a new client version is released\. However, if you used the Enterprise Deployment Tool to install the AppStream 2\.0 client for your users and you disabled automatic updates, you must update the AppStream 2\.0 Enterprise Deployment Tool, client, and USB driver manually\. To do so, perform the following steps to run the required PowerShell commands on users’ computers\. 

**Note**  
To run these commands, you must either be logged in to the applicable computer as Administrator, or you can run the script remotely under the SYSTEM account on startup\.

1. Uninstall the AppStream 2\.0 Enterprise Deployment Tool silently:

   ```
   Start-Process msiexec.exe -Wait -ArgumentList '/x AmazonAppStreamClientSetup_<existing_version>.msi /quiet'
   ```

1. Uninstall the AppStream 2\.0 USB driver silently:

   ```
   Start-Process -Wait AmazonAppStreamUsbDriverSetup_<existing_version>.exe -ArgumentList '/uninstall /quiet /norestart'
   ```

1. Uninstall the AppStream 2\.0 client silently:

   ```
   Start-Process "$env:LocalAppData\AppStreamClient\Update.exe" -ArgumentList '--uninstall'
   ```
**Note**  
This process also removes the registry keys that are used to configure the AppStream 2\.0 client\. After you reinstall the AppStream 2\.0 client, you must recreate these keys\.

1. Clean the application installation directory:

   ```
   Remove-Item -Path $env:LocalAppData\AppStreamClient -Recurse -Confirm:$false –Force 
   ```

1. Restart the computer:

   ```
   Restart-computer
   ```

1. Install the latest version of the AppStream 2\.0 Enterprise Deployment Tool silently:

   ```
   Start-Process msiexec.exe -Wait -ArgumentList '/i AmazonAppStreamClientSetup_<new_version>.msi /quiet'
   ```

1. Install the latest version of the AppStream 2\.0 USB driver silently:

   ```
   Start-Process AmazonAppStreamUsbDriverSetup_<new_version>.exe -Wait -ArgumentList '/quiet'
   ```