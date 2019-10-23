# Install and Configure the AppStream 2\.0 Client<a name="install-configure-client"></a>

You can have your users install the AppStream 2\.0 client themselves, or you can install the AppStream 2\.0 client for them by running PowerShell scripts remotely\.

You must qualify the USB devices that you want to enable your users to use with their streaming session\. If their USB device is not qualified, it won't be detected by AppStream 2\.0 and can't be shared with the session\.

The following topics describe how to install and configure the AppStream 2\.0 client\.

**Topics**
+ [Have Your Users Install the AppStream 2\.0 Client Themselves](#user-install-client)
+ [Install the AppStream 2\.0 Client And Customize the Client Experience for Your Users](#install-client-configure-settings)
+ [Update the AppStream 2\.0 Enterprise Deployment Tool, Client, and USB Driver Manually](#update-enterprise-deployment-tool-client-usb-driver-manually)
+ [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)
+ [Use the AppStream 2\.0 Client to Start a Streaming Session](use-client-start-streaming-session.md)
+ [Share a USB Device with an AppStream 2\.0 Streaming Session](share-usb-devices-with-session.md)
+ [Redirect a Streaming Session from the Web Browser to the AppStream 2\.0 Client](redirect-streaming-session-from-web-to-client.md)
+ [Enable File System Redirection for Your AppStream 2\.0 Users](enable-file-system-redirection.md)

## Have Your Users Install the AppStream 2\.0 Client Themselves<a name="user-install-client"></a>

If you have your users install the client themselves, you can provide them with the following information\. If you qualify USB devices for use with AppStream 2\.0, you can also provide your users with the information in the *Guidance for Users* section in [Share a USB Device with an AppStream 2\.0 Streaming Session](share-usb-devices-with-session.md)\.

**Important**  
If your organization has deployed antivirus software that prevents users from running \.exe files, you must add an exception to allow your users to run the AppStream 2\.0 client installation \.exe program\. Otherwise, when users try to install the client, either nothing happens, or they receive an error after they start the installation program\. 

**Guidance for Users**

You can use the AppStream 2\.0 client to start streaming sessions\. To install the client, perform these steps\.

1. Download the AppStream 2\.0 client application from [AppStream 2\.0 supported clients](https://clients.amazonappstream.com)\.

1. Navigate to the location where you downloaded the application \.exe file, and double\-click the file to begin the installation\.
**Important**  
If nothing happens when you double\-click the file, or an error message displays, contact your network administrator\. Your organization may be using antivirus software that prevents the AppStream 2\.0 client installation program from running\.

1. The installation wizard displays links to the AWS Customer Agreement, AWS Service Terms, and the AWS Privacy Notice, and third\-party notices\. Review this information, and choose **Next**\.

1. On the **Client Diagnostics** page, to enable the AppStream 2\.0 client to automatically upload device logs to help with troubleshooting issues, choose **Client logging**, and choose **Next**\.

1.  On the **Optional Components** page, to enable your USB devices to be used with streaming applications, choose **AppStream 2\.0 Client USB Driver**, and choose **Finish**\.

1. The **AppStream 2\.0 USB driver** wizard setup wizard opens\. Choose **Install**\.

1. If prompted by User Account Control to choose whether to allow the app to make changes to your device, choose **Yes**\.

1. A message notifies you when the USB driver installation is complete\. Choose **Close**\. 

1. The AppStream 2\.0 sign\-in page opens\. If your administrator has provided you with a URL to use to connect to AppStream 2\.0 for application streaming, enter the URL, and choose **Connect**\. Otherwise, close the sign\-in page\. 

Next step: If you want to use your USB devices with streaming applications, you must first share your device with AppStream 2\.0\. For more information, see [Share a USB Device with an AppStream 2\.0 Streaming Session](share-usb-devices-with-session.md)\.

## Install the AppStream 2\.0 Client And Customize the Client Experience for Your Users<a name="install-client-configure-settings"></a>

The following sections describe how to install the AppStream 2\.0 client and customize the client experience for your users\. If you plan to download and install the client for your users, first download the Enterprise Deployment Tool\. You can then run PowerShell scripts to install the AppStream 2\.0 client and configure client settings remotely\.

**Topics**
+ [Download the Enterprise Deployment Tool](#install-client-use-remote-deployment-tool)
+ [Install the AppStream 2\.0 Client and USB Driver](#run-powershell-script-install-client-usb-driver-silently)
+ [Set the Start URL for AppStream 2\.0 Client Users](#set-start-url)
+ [Configure the AppStream 2\.0 Client to Connect to Start URLs in Trusted Domains](#set-trusted-url)
+ [Choose Whether to Disable Automatic Client Updates](#disable-automatic-updates-client)
+ [Configure Additional AppStream 2\.0 Client Settings for Your Users](#configure-client)
+ [Using Group Policy to Customize AppStream 2\.0 Client Experience](#configure-client-with-adm-template-group-policy)

### Download the Enterprise Deployment Tool<a name="install-client-use-remote-deployment-tool"></a>

The Enterprise Deployment Tool includes the AppStream 2\.0 client installation files and a Group Policy administrative template\.

1. To download the Enterprise Deployment Tool, on the bottom right of the [AppStream 2\.0 supported clients](https://clients.amazonappstream.com) page, select the **Enterprise Deployment Tool** link\. This link opens a \.zip file that contains the required files for the latest version of the tool\.

1. To extract the required files, navigate to the location where you downloaded the tool, right\-click the **AmazonAppStreamClient\_EnterpriseSetup\_<version>** folder, and choose **Extract All**\. The folder contains two installation programs and a Group Policy administrative template:
   + AppStream 2\.0 client installer \(AmazonAppStreamClientSetup\_<version>\.msi\) — Installs the AppStream 2\.0 client\.
   + AppStream 2\.0 USB driver installer \(AmazonAppStreamUsbDriverSetup\_<version>\.exe\) — Installs the AppStream 2\.0 USB driver that is required to use USB devices with applications streamed through AppStream 2\.0\.
   + AppStream 2\.0 client Group Policy administrative template \(as2\_client\_config\.adm\) – Lets you configure the AppStream 2\.0 client through Group Policy\.

### Install the AppStream 2\.0 Client and USB Driver<a name="run-powershell-script-install-client-usb-driver-silently"></a>

After you download the AppStream 2\.0 client installation files, run the following PowerShell script on users' computers to install the AppStream 2\.0 client and USB driver silently\. 

**Note**  
To run this script, you must be logged into the applicable computer with the local **Administrator** account\. You can also run the script remotely under the **System** account on startup\.

```
Start-Process msiexec.exe -Wait -ArgumentList  '/i AmazonAppStreamClientSetup_<version>.msi /quiet'

Start-Process AmazonAppStreamUsbDriverSetup_<version>.exe -Wait -ArgumentList  '/quiet'
```

After you install the Enterprise Deployment tool on users’ computers, the AppStream 2\.0 client is also installed automatically for current users\. For new users, the client is installed the first time that they log in to their computer\. However, if users uninstall the AppStream 2\.0 client, the client isn’t installed again until you update the AppStream 2\.0 Enterprise Deployment Tool\.

### Set the Start URL for AppStream 2\.0 Client Users<a name="set-start-url"></a>

By default, when users open the AppStream 2\.0 client, they can only enter URLs that include the AppStream 2\.0 domain\. However, you can use the **StartUrl** registry value to set a custom URL, such as the URL for your organization's login portal\. You can create this HKLM registry key while installing the client so that your users don’t need to specify the start URL the first time they launch the client\.

After the AppStream 2\.0 client is installed, you can run the following PowerShell script to create this registry key, or you can use the administrative template that is included in the AppStream 2\.0 client Enterprise Deployment Tool to configure the client through Group Policy\. Replace the **StartUrl** value with a URL for your identity provider \(IdP\)\. The URL must use a certificate that is trusted by the device\. The certificate must contain a SAN that includes the URL's domain name\.

**Note**  
To run this script, you must be logged into the applicable computer with the local **Administrator **account\. You can also run the script remotely under the **System** account on startup\. 

```
$registryPath="HKLM:\Software\Amazon\AppStream Client"
New-Item -Path "HKLM:\Software\Amazon" -Name "AppStream Client" -Force

New-ItemProperty -Path $registryPath -Name "StartUrl" -Value "https://www.example.com" -PropertyType String -Force | Out-Null
```

### Configure the AppStream 2\.0 Client to Connect to Start URLs in Trusted Domains<a name="set-trusted-url"></a>

By default, the AppStream 2\.0 client can connect to a start URL that belongs to the **appstream** domain or to a start url that you configure through the AppStream 2\.0 **StartURL** HKLM registry key\. You can also configure the AppStream 2\.0 client to connect to start URLs in trusted domains that you specify\. For example, you may want to let users connect to any start URL in your organizational domain \(for example, \*\.example\.com\) or to any URL in one or more of your identity provider \(IdP\) domains \(\*\.example\-idp\.com\)\. You can specify a list of trusted domains in a comma\-separated values \(\.csv\) format\. Add this list as a registry value to the AppStream 2\.0 **Trusted Domains** HKLM registry key\. We recommend that you create this registry key and specify the list of trusted domains when you install the AppStream 2\.0 client\. That way, your users can connect to a start URL in any trusted domain immediately after the client is installed\.

After the AppStream 2\.0 client is installed, you can run the following PowerShell script to create this registry key, or you can use the administrative template that is included in the AppStream 2\.0 client Enterprise Deployment Tool to configure the client through Group Policy\. Replace the **TrustedDomains** value with a \.csv list for one or more of your IdP domains\. The domains must use a certificate that is trusted by the device\. 

**Note**  
To run this script, you must be logged into the applicable computer with the local **Administrator **account\. You can also run the script remotely under the **System** account on startup\. 

```
$registryPath="HKLM:\Software\Amazon\AppStream Client"
New-Item -Path "HKLM:\Software\Amazon" -Name "AppStream Client" -Force

New-ItemProperty -Path $registryPath -Name "TrustedDomains" -Value "*.okta.com, *.pingone.com, aws.amazon.com" -PropertyType String -Force | Out-Null
```

Following are requirements and considerations for formatting trusted domain names\.
+ The following characters are supported: a\-z, 0\-9, \-, \*
+ DNS treats the \* character either as a wildcard or as an asterisk character \(ASCII 42\), depending on where it appears in the domain name\. Following are restrictions when using \* as a wildcard in the name of a DNS record:
  + The \* must replace the leftmost label in a domain name\. For example, \*\.example\.com or \*\.prod\.example\.com\. If you include \* in any other position, such as prod\.\*\.example\.com, DNS treats it as an asterisk character \(ASCII 42\), not as a wildcard\.
  + The \* must replace the entire label\. For example, you can't specify \*prod\.example\.com or prod\*\.example\.com\.
  + The \* applies to the subdomain level that includes the \*, and to all the subdomains of that subdomain\. For example, if an entry is named \*\.example\.com, the AppStream 2\.0 client allows zenith\.example\.com, acme\.zenith\.example\.com, and pinnacle\.acme\.zenith\.example\.com\.

### Choose Whether to Disable Automatic Client Updates<a name="disable-automatic-updates-client"></a>

By default, when a new version of the AppStream 2\.0 client is available, the client updates automatically to the latest version\. However, you can disable automatic updates by setting the value for the **AutoUpdateDisabled **registry key to **true**\. You can create this registry key when you install the AppStream 2\.0 client\. That way, the client is not updated automatically whenever a new version is available\. 

After the AppStream 2\.0 client is installed, you can run the following PowerShell script to create this registry key, or you can use the administrative template that is included in the AppStream 2\.0 client Enterprise Deployment Tool to configure the client through Group Policy\.

**Note**  
To run this script, you must be logged into the applicable computer with the local **Administrator **account\. You can also run the script remotely under the **System** account on startup\. 

```
$registryPath="HKLM:\Software\Amazon\AppStream Client"
New-Item -Path "HKLM:\Software\Amazon" -Name "AppStream Client" -Force

New-ItemProperty -Path $registryPath -Name "AutoUpdateDisabled" -Value "True" -PropertyType String -Force | Out-Null
```

### Configure Additional AppStream 2\.0 Client Settings for Your Users<a name="configure-client"></a>

The AppStream 2\.0 client uses registry keys to configure the following additional client settings:
+ AppStream 2\.0 client End\-User License Agreement \(EULA\) acceptance
+ AppStream 2\.0 client EULA version accepted
+ Diagnostic logging for the AppStream 2\.0 client
+ Automatic updates for the USB driver that is used to pass USB drivers to AppStream 2\.0
+ Enabling hardware rendering in the AppStream 2\.0 client
+ Setting custom folder paths for file system redirection in the AppStream 2\.0 client

The following table summarizes the registry values for additional client settings that you can use to customize the AppStream 2\.0 client experience for your users\. 

**Note**  
These values are case\-sensitive\.


| Value | Registry path | Type | Description | Data | 
| --- | --- | --- | --- | --- | 
| EULAAccepted | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to accept the AppStream 2\.0 client EULA on behalf of your users\. | true / false | 
| AcceptedEULAVersion | HKCU\\Software\\Amazon\\Appstream Client | String | The version of EULA that is accepted\. If the current version of the AppStream 2\.0 client EULA is different than the version of the EULA that is accepted, users are prompted to accept the current version of the EULA\. | 1\.0 | 
| DiagnosticInfoCollectionAllowed | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to enable AppStream 2\.0 to automatically send diagnostic logs from the AppStream 2\.0 client to AppStream 2\.0\. | true / false | 
| USBDriverOptIn | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to enable AppStream 2\.0 to automatically update the USB driver that is used to pass USB drivers to AppStream 2\.0\. | true / false | 
| HardwareRenderingEnabled | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to enable hardware rendering in the AppStream 2\.0 client\. | true / false | 
| FileRedirectionCustomDefaultFolders | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to include at least one folder path for file system redirection\. Separate multiple folder paths by using '\|'\. By default, the following folder paths are specified: %USERPROFILE%\\Desktop\|%USERPROFILE%\\Documents\|%USERPROFILE%\\Downloads | Valid folder path | 

After the AppStream 2\.0 client is installed, you can run the following PowerShell script to create these registry keys\. If you don’t want to create all of the registry keys, modify the script as needed to create only the registry keys that you want\. Alternatively, you can use the administrative template that is provided in the AppStream 2\.0 client Enterprise Deployment Tool to configure the client through Group Policy\.

**Note**  
You must set the following entries for each user\.

```
$registryPath="HKCU:\Software\Amazon\AppStream Client"
New-Item -Path "HKCU:\Software\Amazon" -Name "AppStream Client" -Force
New-ItemProperty -Path $registryPath -Name "EULAAccepted" -Value "true" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "AcceptedEULAVersion" -Value "1.0" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "DiagnosticInfoCollectionAllowed" -Value "true" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "USBDriverOptIn" -Value "true" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "HardwareRenderingEnabled" -Value "true" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "FileRedirectionCustomDefaultFolders" -Value "%USERPROFILE%\Desktop|%USERPROFILE%\Documents|%USERPROFILE%\Downloads" -PropertyType String -Force | Out-Null
```

### Using Group Policy to Customize AppStream 2\.0 Client Experience<a name="configure-client-with-adm-template-group-policy"></a>

You can use the administrative template that is provided in the AppStream 2\.0 client Enterprise Deployment Tool to configure the client through Group Policy\. To learn how to load administrative templates into the Group Policy Management Console, see [Recommendations for managing Group Policy administrative template \(\.adm\) files](https://support.microsoft.com/en-us/help/816662/recommendations-for-managing-group-policy-administrative-template-adm) in the Microsoft Support documentation\.

## Update the AppStream 2\.0 Enterprise Deployment Tool, Client, and USB Driver Manually<a name="update-enterprise-deployment-tool-client-usb-driver-manually"></a>

By default, the AppStream 2\.0 client and USB driver are updated automatically when a new client version is released\. However, if you used the Enterprise Deployment Tool to install the AppStream 2\.0 client for your users and you disabled automatic updates, you must update the AppStream 2\.0 Enterprise Deployment Tool, client, and USB driver manually\. To do so, perform the following steps to run the required PowerShell commands on users’ computers\. 

**Note**  
To run these commands, you must either be logged into the applicable computer as Administrator, or you can run the script remotely under the SYSTEM account on startup\.

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