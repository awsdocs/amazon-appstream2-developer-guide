# Install and Configure the AppStream 2\.0 Client<a name="install-configure-client"></a>

You can have your users install the AppStream 2\.0 client themselves, or you can install the AppStream 2\.0 client for them by running PowerShell scripts remotely\.

You must qualify the USB devices that you want to enable your users to use with their streaming session\. If their USB device is not qualified, it won't be detected by AppStream 2\.0 and can't be shared with the session\.

The following topics describe how to install and configure the AppStream 2\.0 client\.

**Topics**
+ [Have Your Users Install the AppStream 2\.0 Client Themselves](#user-install-client)
+ [Install the AppStream 2\.0 Client for Your Users](#install-client-configure-settings)
+ [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)
+ [Use the AppStream 2\.0 Client to Start a Streaming Session](use-client-start-streaming-session.md)
+ [Share a USB Device with an AppStream 2\.0 Streaming Session](share-usb-devices-with-session.md)
+ [Redirect a Streaming Session from the Web Browser to the AppStream 2\.0 Client](redirect-streaming-session-from-web-to-client.md)
+ [AppStream 2\.0 Client Version History](client-release-versions.md)

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

## Install the AppStream 2\.0 Client for Your Users<a name="install-client-configure-settings"></a>

If you plan to download and install the client for your users, first download the Enterprise Deployment Tool\. You can then run PowerShell scripts to install the AppStream 2\.0 client and configure client settings remotely\.

### Use a Deployment Tool to Install the AppStream 2\.0 Client Remotely<a name="install-client-use-remote-deployment-tool"></a>

To install and configure the AppStream 2\.0 client for your users, download the installation files\.

1. On the bottom right of the [AppStream 2\.0 supported clients](https://clients.amazonappstream.com) page, select the **Enterprise Deployment Tool** link\. This link opens a \.zip file that contains the required files for the latest version of the tool\.

1. Navigate to the location where you downloaded the tool, right\-click the **AmazonAppStreamClient\_EnterpriseSetup\_<version>** folder, and choose **Extract All**\. The folder contains the following two installation programs:
   + AmazonAppStreamClientSetup\_<version>\.msi
   + AmazonAppStreamUsbDriverSetup\_<version>\.exe

### Run a PowerShell Script to Install the AppStream 2\.0 Client<a name="configure-start-url-remotely-use-powershell"></a>

After you download the AppStream 2\.0 client installation files, run the following PowerShell script on users' computers to silently install the AppStream 2\.0 client\. 

**Note**  
To run this script, you must be logged into the applicable computer with the local **Administrator** account\. You can also run the script remotely under the **System** account on startup\.

```
Start-Process msiexec.exe -Wait -ArgumentList  '/i AmazonAppStreamClientSetup_<version>.msi /quiet'

Start-Process AmazonAppStreamUsbDriverSetup_<version>.exe -Wait -ArgumentList  '/quiet'
```

### Configure the AppStream 2\.0 Client for Your Users<a name="configure-client"></a>

Before your users can start using the AppStream 2\.0 client, they must accept the End\-User License Agreement \(EULA\) and choose whether to enable diagnostic logging and USB driver updates\. Alternatively, you can define these preferences on behalf of your users\. By default, when users open the AppStream 2\.0 client, they can only enter URLs that include the AppStream 2\.0 domain\. However, you can set custom URLs by using the **StartUrl** registry value\. For example, you can set this value to the URL for your organization's login portal\. That way, users can sign into AppStream 2\.0 by using their existing credentials\. 

The following table lists the registry values that you can use to customize the AppStream 2\.0 client experience for your users\. 

**Note**  
The values are case\-sensitive\.


| Value | Registry path | Type | Description | Data | 
| --- | --- | --- | --- | --- | 
| EULAAccepted | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to accept the AppStream 2\.0 client EULA on behalf of your users\. | true / false | 
| AcceptedEULAVersion | HKCU\\Software\\Amazon\\Appstream Client | String | The version of EULA that is accepted\. If the current version of the AppStream 2\.0 client EULA is different than the version of the EULA that is accepted, users are prompted to accept the current version of the EULA\. | 1\.0 | 
| DiagnosticInfoCollectionAllowed | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to enable AppStream 2\.0 to automatically send diagnostic logs from the AppStream 2\.0 client to AppStream 2\.0\. | true / false | 
| USBDriverOptIn | HKCU\\Software\\Amazon\\Appstream Client | String | Set this value to true to enable AppStream 2\.0 to automatically update the USB driver that is used to pass USB drivers to AppStream 2\.0\. | true / false | 
| StartUrl | HKLM\\Software\\Amazon\\Appstream Client | String | Set this value to a URL that is pre\-populated when your users open the AppStream 2\.0 client\. The URL must use a certificate that is trusted by the device\. The certificate must contain a Subject Alternative Name \(SAN\) that includes the URL's domain name\. | Valid URL \(for example, https://www\.example\.com\) | 

#### Configure the AppStream 2\.0 Client through Group Policy<a name="configure-client-with-adm-template-group-policy"></a>

You can use the ADM template that is provided in the AppStream 2\.0 client Enterprise Deployment Tool to configure the client through Group Policy\. To learn how to load ADM templates into the Group Policy Management Console, see [Recommendations for managing Group Policy administrative template \(\.adm\) files](https://support.microsoft.com/en-us/help/816662/recommendations-for-managing-group-policy-administrative-template-adm) in the Microsoft documentation\.

#### Run a PowerShell Script to Create Registry Keys and Set User Preferences<a name="create-regkeys-configure-user-preference-settings"></a>

To create the registry keys and set values for user preferences for the AppStream 2\.0 client, run the following PowerShell script\.

**Note**  
You must set the following entries for each user\.

```
$registryPath="HKCU:\Software\Amazon\AppStream Client"
New-Item -Path "HKCU:\Software\Amazon" -Name "AppStream Client" -Force
New-ItemProperty -Path $registryPath -Name "EULAAccepted" -Value "true" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "AcceptedEULAVersion" -Value "1.0" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "DiagnosticInfoCollectionAllowed" -Value "true" -PropertyType String -Force | Out-Null
New-ItemProperty -Path $registryPath -Name "USBDriverOptIn" -Value "true" -PropertyType String -Force | Out-Null
```

#### Run a PowerShell Script to Set the Start URL<a name="set-start-url"></a>

To set a start URL, run the following PowerShell script\. Replace the **StartUrl** value with a URL for your identity provider \(IdP\)\. The URL must use a certificate that is trusted by the device\. The certificate must contain a SAN that includes the URL's domain name\.

**Note**  
To run this script, you must be logged into the applicable computer with the local **Administrator **account\. You can also run the script remotely under the **System** account on startup\. 

```
$registryPath="HKLM:\Software\Amazon\AppStream Client"
New-Item -Path "HKLM:\Software\Amazon" -Name "AppStream Client" -Force

New-ItemProperty -Path $registryPath -Name "StartUrl" -Value "https://www.example.com" -PropertyType String -Force | Out-Null
```