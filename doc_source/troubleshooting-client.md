# Troubleshooting AppStream 2\.0 User Issues<a name="troubleshooting-client"></a>

The following are possible issues that might occur for AppStream 2\.0 users\.

**Topics**
+ [My users' AppStream 2\.0 client installations fail, and they're getting a message stating that \.NET Framework 4\.6 is required\.](#troubleshooting-client-no-internet-net-framework-462-fails)
+ [My users' USB driver installations fail when they install the AppStream 2\.0 client, and now they can't use their USB devices with AppStream 2\.0\.](#troubleshooting-client-no-internet-usb-driver-install-fails)
+ [My AppStream 2\.0 client users are getting disconnected from their AppStream 2\.0 session after every 60 minutes\.](#troubleshooting-client-users-disconnected-every-60-minutes)
+ [My users' drawing tablets are not working with the streaming applications I deployed\.](#troubleshooting-client-users-drawing-tablets-not-working)

## My users' AppStream 2\.0 client installations fail, and they're getting a message stating that \.NET Framework 4\.6 is required\.<a name="troubleshooting-client-no-internet-net-framework-462-fails"></a>

When users install the AppStream 2\.0 client, AppStream 2\.0 also installs \.NET Framework version 4\.6\.2, if that version or a later version is not already installed\. If the PC on which the client is being installed is not connected to the internet, \.NET Framework can't be installed\. In this case, a message prompts users to install \.NET Framework version 4\.6 manually\. However, when users choose **Install**, an error message is displayed stating that the installation failed\. Users are then prompted to try installing the latest version of the \.NET Framework manually\. When they choose **Close**, they exit the installation\.

To resolve this issue, users must establish an internet connection from the PC on which they plan to install the client, and then download and install \.NET Framework version 4\.6\.2 or later on the same PC\. For a list of the \.NET Framework versions available for download, see [Download \.NET Framework](https://dotnet.microsoft.com/download/dotnet-framework)\.

**Note**  
Users who have version 1\.1\.156 of the AppStream 2\.0 client installed must have \.NET Framework version 4\.7\.2 or later installed on the same PC\.

## My users' USB driver installations fail when they install the AppStream 2\.0 client, and now they can't use their USB devices with AppStream 2\.0\.<a name="troubleshooting-client-no-internet-usb-driver-install-fails"></a>

When users install the AppStream 2\.0 client, they choose whether to install the AppStream 2\.0 USB driver\. The driver is required to use USB devices with applications streamed through AppStream 2\.0\. However, the USB driver installation fails if both of the following occur:
+ The root certificate used to sign the `AppStreamUsbDriver.exe` file is not present in the Windows certificate store\.
+ The PC on which the client is being installed is not connected to the internet\. 

In this case, the certificate for the Amazon AppStream USB driver can't be validated, and an error message notifies users that the USB driver installation failed\. When users choose **OK**, the AppStream 2\.0 client installation is completed without the USB driver\. Although users can still use the AppStream 2\.0 client for application streaming, their USB devices won't work with applications streamed through AppStream 2\.0\. 

To resolve this issue, users must establish an internet connection from the PC on which they plan to install the AppStream 2\.0 client, and reinstall the client\.

## My AppStream 2\.0 client users are getting disconnected from their AppStream 2\.0 session after every 60 minutes\.<a name="troubleshooting-client-users-disconnected-every-60-minutes"></a>

If you have configured identity federation using SAML 2\.0 for access to AppStream 2\.0, depending on your identity provider \(IdP\), you may need to configure the information that the IdP passes as SAML attributes to AWS as part of the authentication response\. This includes configuring the **Attribute** element with the `SessionDuration` attribute set to `https://aws.amazon.com/SAML/Attributes/SessionDuration`\.

`SessionDuration` specifies the maximum amount of time that a federated streaming session for a user can remain active before reauthentication is required\. Although `SessionDuration` is an optional attribute, we recommend that you include it in the SAML authentication response\. If you do not specify this attribute, the session duration is set to a default value of 60 minutes\.

To resolve this issue, configure your SAML\-compatible IdP to include the `SessionDuration` value in the SAML authentication response, and set the value as required\. For more information, see [Step 5: Create Assertions for the SAML Authentication Response](external-identity-providers-setting-up-saml.md#external-identity-providers-create-assertions)\.

**Note**  
If your users access their streaming applications in AppStream 2\.0 by using the AppStream 2\.0 client, their sessions are disconnected after their session duration expires\. If your users access their streaming applications in AppStream 2\.0 by using a web browser, after the users' session duration expires and they refresh their browser page, their sessions are disconnected\.

## My users' drawing tablets are not working with the streaming applications I deployed\.<a name="troubleshooting-client-users-drawing-tablets-not-working"></a>

If your users' drawing tablets are not working with streaming applications, make sure that you meet the requirements and understand additional considerations for enabling this feature\. Following are the requirements and considerations for enabling your users to use drawing tablets during AppStream 2\.0 streaming sessions\. 

**Note**  
Drawing tablets are supported for users who access AppStream 2\.0 by using the AppStream 2\.0 client, or through a supported web browser\.
+ To enable your users to use this feature, you must configure your AppStream 2\.0 fleet to use an image that runs Windows Server 2019\.
+ To use this feature, users must access AppStream 2\.0 by using the AppStream 2\.0 client, or through the Google Chrome or Mozilla Firefox browsers only\.
+ Streaming applications must support Windows Ink technology\. For more information, see [Pen interactions and Windows Ink in Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/input/pen-and-stylus-interactions)\.
+ Some applications, such GIMP, must detect drawing tablets on the streaming instance to support pressure sensitivity\. If this is the case, your users must use the AppStream 2\.0 client to access AppStream 2\.0 and stream these applications\. In addition, you must qualify your users' drawing tablets, and users must share their drawing tablets with AppStream 2\.0 every time they start a new streaming session\.
+ This feature is not supported on Chromebooks\.