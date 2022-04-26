# System Requirements and Feature Support \(AppStream 2\.0 Client\)<a name="client-system-requirements-feature-support"></a>

This topic provides information to help you understand the requirements for the AppStream 2\.0 client and supported features\.

## System Requirements and Considerations<a name="client-system-requirements"></a>

The AppStream 2\.0 client requires the following:
+ Follow the principle of least privilege when launching the AppStream 2\.0 client\. The client should only run with the level of privilege required to complete a task\. 
+ Operating system — Windows 7, Windows 8, or Windows 10 \(32\-bit or 64\-bit\)
+ Microsoft Visual C\+\+ 2015 Redistributable or later\. For information about the latest Visual C\+\+ redistributable packages for Visual Studio 2015, 2017, and 2019, see [The latest supported Visual C\+\+ downloads](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads) in the Microsoft Support documentation\.
+ RAM — 2 GB minimum
+ Hard drive space — 200 MB minimum
+ Local administrator rights — Used if you want to install the AppStream 2\.0 USB driver for USB driver support\.
+ An AppStream 2\.0 image that uses the latest AppStream 2\.0 agent or agent versions published on or after November 14, 2018\. For information about AppStream 2\.0 agent versions, see [AppStream 2\.0 Agent Release Notes](agent-software-versions.md)\.

**Note**  
We recommend an internet connection for AppStream 2\.0 client installation\. In some cases, the client can't be installed on a computer that is not connected to the internet, or USB devices might not work with applications streamed from AppStream 2\.0\. For more information, see [Troubleshooting AppStream 2\.0 User Issues](troubleshooting-user-issues.md)\.

## Feature and Device Support<a name="client-feature-support"></a>

The AppStream 2\.0 client supports the following features and devices\.

**Topics**
+ [Native Application Mode](#feature-support-native-application-mode)
+ [Automatic and On\-Demand Diagnostic Log Uploads](#feature-support-diagnostic-log-upload)
+ [Peripheral Devices](#feature-support-peripheral-devices)

### Native Application Mode<a name="feature-support-native-application-mode"></a>

**Note**  
Native application mode is not available when streaming from Linux instances\.

Native application mode provides a familiar experience for your users during their AppStream 2\.0 streaming sessions\. When your users connect to AppStream 2\.0 in this mode, they can work with their remote streaming applications in much the same way that they work with applications that are installed on their local computer\. Each streaming application in native application mode opens in its own window, and application icons appear on the taskbar on your users' local PC\.

If you want your users to connect to AppStream 2\.0 in classic mode only, you can configure the `NativeAppModeDisabled` registry value to disable native application mode\. For more information, see [Choose Whether to Disable Native Application Mode](install-client-configure-settings.md#disable-native-application-mode-client)\.

For more information about native application mode and classic mode, and for guidance that you can provide to your users, see [AppStream 2\.0 Client Connection Modes](client-application-windows-user.md#client-application-windows-connection-modes-user)\.

**Note**  
Native application mode is not available if your fleet is enabled for the **Desktop** stream view\. For information about how to configure the **Desktop** stream view, see [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

**Requirements**

To enable this feature for your users, you must use an image that uses a [version of the AppStream 2\.0 agent](agent-software-versions.md) released on or after February 19, 2020\. In addition, version 1\.1\.129 or later of the AppStream 2\.0 client must be installed on your users' PCs\. For more information about client versions, see [AppStream 2\.0 Client Release Notes](client-release-versions.md)\.

If AppStream 2\.0 client version 1\.1\.129 or later is installed on your users' computer, but you are not using an image that uses an agent version released on or after February 19, 2020, the client falls back to classic mode even if native application mode is selected\.

**Known Issues**

When users try to dock or undock tabs in one browser window into separate windows during a streaming session in native application mode, their remote streaming browser doesn't work the same way as a local browser\. To perform this task during a streaming session in native application mode, users must press the Alt key until their browser tabs are docked into separate browser windows\. 

### Automatic and On\-Demand Diagnostic Log Uploads<a name="feature-support-diagnostic-log-upload"></a>

To help with troubleshooting issues that might occur when your users are using the AppStream 2\.0 client, you can enable automatic or on\-demand diagnostic log uploads, or let your users do so themselves\. 

**Note**  
Diagnostic logs do not contain sensitive information\. You can disable automatic and on\-demand diagnostic log uploads on user PCs that you manage, or allow your users to disable these features themselves\.

**Automatic diagnostic log uploads **

When you install the client on PCs that you manage, you can configure the AppStream 2\.0 client to upload diagnostic logs automatically\. That way, when a client issue occurs, the logs are sent to AppStream 2\.0 \(AWS\) without user interaction\. For more information, see [Configure Additional AppStream 2\.0 Client Settings for Your Users](install-client-configure-settings.md#configure-client)\.

Or, you can let your users choose whether to enable automatic diagnostic log uploads when they install the AppStream 2\.0 client, or after client installation\. For guidance that you can provide your users to help them perform this task, see [Setup](client-application-windows-user.md#client-application-windows-installation-user)\.

**On\-demand diagnostic log uploads **

If you require more control over logging, you can disable automatic logging and enable on\-demand diagnostic log uploads\. If you let your users upload diagnostic logs on demand, they can also choose whether to send minidumps \(error reports\) to AppStream 2\.0 \(AWS\) if an exception occurs or the client stops responding\.

 For guidance that you can provide your users to help them perform these tasks, see [Logging](client-application-windows-user.md#client-application-windows-how-to-enable-diagnostic-logging-user)\.

### Peripheral Devices<a name="feature-support-peripheral-devices"></a>

The AppStream 2\.0 client provides the following support for peripheral devices such as monitors, webcams, mice, keyboards, and drawing tablets\.

**Note**  
With certain exceptions, USB redirection is required for the AppStream 2\.0 client to support USB devices\. And in most cases, when USB redirection is required for a device, you must qualify the device before it can be used with AppStream 2\.0 streaming sessions\. For more information, see [USB Redirection](#feature-support-USB-devices-USB-redirection)\.

**Topics**
+ [Multiple Monitors](#feature-support-multiple-monitors)
+ [Real\-Time Audio\-Video \(Client for Windows\)](#feature-support-real-time-av)
+ [USB Devices](#feature-support-USB-devices-qualified)
+ [Drawing Tablets](#feature-support-drawing-tablets)
+ [Keyboard Shortcuts](#feature-support-keyboard-shortcuts)
+ [Relative Mouse Offset](#feature-support-relative-mouse-offset)

#### Multiple Monitors<a name="feature-support-multiple-monitors"></a>

AppStream 2\.0 supports the use of multiple monitors during streaming sessions, including monitors that have different resolutions\. To help ensure an optimal streaming experience, we recommend that users who have monitors with different resolutions set the display scale for their monitors to 100 percent\.

**Note**  
For AppStream 2\.0 streaming sessions that use [native application mode](#feature-support-native-application-mode), monitors with up to 2K resolution are supported\. If higher\-resolution monitors are used for streaming sessions, the AppStream 2\.0 client falls back to classic mode\. In this scenario, the AppStream 2\.0 classic mode streaming view occupies 2K of the screen, and the remaining portion of the screen is black\.

##### Multiple Monitors \(up to 2K Resolution\)<a name="feature-support-multiple-monitors-2K"></a>

The following AppStream 2\.0 instance types support up to 4 monitors and a maximum display resolution of 2560x1600 pixels per monitor: General Purpose, Memory Optimized, Compute Optimized, Graphics Design, and Graphics Pro\.

##### Multiple Monitors \(up to 4K Resolution\)<a name="feature-support-multiple-monitors-4K"></a>

The following AppStream 2\.0 instance types support up to 2 monitors with a maximum display resolution of 4096x2160 pixels per monitor: Graphics Design and Graphics Pro\. 

**Note**  
Non\-graphics instance types \(General Purpose, Memory Optimized, and Compute Optimized\) support a maximum display resolution of 2560x1600 pixels per monitor\.

#### Real\-Time Audio\-Video \(Client for Windows\)<a name="feature-support-real-time-av"></a>

AppStream 2\.0 supports real\-time audio\-video \(AV\) by redirecting local webcam video input to AppStream 2\.0 streaming sessions\. This capability enables your users to use their local webcam for video and audio conferencing within an AppStream 2\.0 streaming session\. With real\-time AV and support for real\-time audio, your users can collaborate by using familiar video and audio conferencing applications without having to leave their AppStream 2\.0 streaming session\.

When a user starts a video conference from within an AppStream 2\.0 streaming session, AppStream 2\.0 compresses the webcam video and microphone audio input locally before transmitting this data over a secure channel to a streaming instance\. During their streaming sessions, users can enable audio and video input by using the AppStream 2\.0 toolbar\. If users have more than one webcam \(for example, if they have a USB webcam that is connected to their local computer and a built\-in webcam\), they can also choose which webcam to use during their streaming session\.

To configure and test support for real\-time AV, complete the following steps\.

**Configure and test support for real\-time AV**

1. Create a new image builder or connect to an existing image builder that meets the following requirements:
   + The image builder must run Windows Server 2016 or Windows Server 2019\.
   + The image builder must use a version of the AppStream 2\.0 agent released on or after June 1, 2021\.
   + For AppStream 2\.0 agents released on or after May 17, 2021, real\-time AV is enabled by default\. To create a streaming URL for testing, you can skip steps 3 through 6 and disconnect from the image builder\. If you need to disable real\-time AV, complete all of the steps, and disable webcam permissions in step 4\.
   + The image builder must use a version of the AppStream 2\.0 agent released on or after June 24, 2021 to support video when connecting using web browser access\. For more information about supported web browsers, see [Web Browser Access](web-browser-user.md)\.

   For information about how to create an image builder, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

1. Connect to the image builder that you want to use and sign in as Administrator\. To connect to the image builder, do either of the following:
   + [Use the AppStream 2\.0 console](managing-image-builders-connect.md#managing-image-builders-connect-console) \(for web connections only\)
   + [Create a streaming URL](managing-image-builders-connect.md#managing-image-builders-connect-streaming-URL) \(for web or AppStream 2\.0 client connections\)
**Note**  
If the image builder that you want to connect to is joined to an Active Directory domain and your organization requires smart card sign in, you must create a streaming URL and use the AppStream 2\.0 client for the connection\. For information about smart card sign in, see [Smart Cards](#feature-support-USB-devices-qualified-smart-cards)\.

1. On the image builder, open Registry Editor\. To do so, on the image builder desktop, in the search box on the taskbar, type **regedit**\. Then, select the top result for **Registry Editor**\.

1. Under **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Amazon\\AppStream\\**, create a new registry value that has the following type, name, and value data:
   + Registry value type: DWORD
   + Registry value name: WebcamPermission
   + Registry value data \(Hexademical\): 1 to enable or 0 to disable webcam permissions

1. After you create the registry value, switch to **Template User** or to a domain user account that does not have administrator permissions on the image builder\. To switch to **Template User**, in the toolbar on the top right of the session window, choose **Admin Commands**, **Switch User**, **Template User**\.

1. Switch back to **Administrator**\.

1. Disconnect from the image builder and create a streaming URL for the image builder\. To do so:

   1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

   1. In the navigation pane, choose **Images**, then choose **Image Builder**\.

   1. Select the image builder from which you just disconnected, and choose **Actions**, **Create streaming URL**\.

   1. Choose **Copy Link** and save the link to a secure and accessible location\. You will use the link in the next step to connect to the image builder\.

1. Using the streaming URL that you just created, connect to the image builder by using the AppStream 2\.0 client or web browser access\.

1. Test the real\-time AV experience on the image builder by following the steps in [Video and Audio Conferencing \(Client for Windows\)](client-application-windows-user.md#client-application-windows-how-to-use-local-webcam-user)\.

1. After you verify that real\-time AV is working as expected, disconnect from your streaming session, reconnect to the image builder and follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

After you finish configuring your image builder and creating an image that supports real\-time AV, you can make this feature available to your users on AppStream 2\.0 fleets\. Ensure that version 1\.1\.257 or later of the AppStream 2\.0 client is installed on your users' computers\.

**Note**  
To use real\-time AV with the AppStream 2\.0 client, your AppStream 2\.0 base image and agent version should be June 1, 2021 or later\. We recommend using the latest AppStream 2\.0 client\. For guidance that you can provide to your users to help them use real\-time AV, see [Video and Audio Conferencing \(Client for Windows\)](client-application-windows-user.md#client-application-windows-how-to-use-local-webcam-user)\.  
To use real\-time AV with web browser access, your AppStream 2\.0 image must use a version of the AppStream 2\.0 agent released on or after June 24, 2021\. For more information on supported web browsers, see [Web Browser Access](web-browser-user.md)\.





#### USB Devices<a name="feature-support-USB-devices-qualified"></a>

The following sections provide information about AppStream 2\.0 support for USB devices\.

**Topics**
+ [USB Redirection](#feature-support-USB-devices-USB-redirection)
+ [Smart Cards](#feature-support-USB-devices-qualified-smart-cards)

##### USB Redirection<a name="feature-support-USB-devices-USB-redirection"></a>

USB redirection is required for most local USB devices to be used during AppStream 2\.0 streaming sessions\. When USB redirection is required, you must [qualify the device](qualify-usb-devices.md) before your users can use it during their AppStream 2\.0 streaming sessions\. After you qualify the device, users must [share the device with AppStream 2\.0](client-application-windows-user.md#client-application-windows-how-to-share-usb-devices-user)\. With USB redirection, during AppStream 2\.0 streaming sessions, users' devices are not accessible for use with local applications\.

In other cases, USB devices are already enabled for use with AppStream 2\.0 and no further configuration is required\. For example, smart card redirection is already enabled by default when the AppStream 2\.0 client is installed\. Because USB redirection isn't used when this feature is enabled, you don't need to qualify smart card readers, and users don't need to share these devices with AppStream 2\.0 to use them during streaming sessions\.

**Note**  
USB redirection is currently not supported for Linux\-based fleet instances\.

##### Smart Cards<a name="feature-support-USB-devices-qualified-smart-cards"></a>

AppStream 2\.0 supports using a smart card for Windows sign in to Active Directory\-joined streaming instances and in\-session authentication for streaming applications\. Because smart card redirection is enabled by default, users can use smart card readers that are connected to their local computer and their smart cards without USB redirection\.

**Topics**
+ [Windows Sign In and In\-Session Authentication](#feature-support-USB-devices-qualified-smart-cards-windows-signin-in-session-auth)
+ [Smart Card Redirection](#feature-support-USB-devices-qualified-smart-cards-support)

##### Windows Sign In and In\-Session Authentication<a name="feature-support-USB-devices-qualified-smart-cards-windows-signin-in-session-auth"></a>

AppStream 2\.0 supports the use of Active Directory domain passwords or smart cards such as [Common Access Card \(CAC\)](https://www.cac.mil/Common-Access-Card) and [Personal Identity Verification \(PIV\)](https://piv.idmanagement.gov/) smart cards for Windows sign in to AppStream 2\.0 streaming instances \(fleets and image builders\)\. Your users can use smart card readers connected to their local computer and their smart cards to sign in to an AppStream 2\.0 streaming instance that is joined to a Microsoft Active Directory domain\. They can also use their local smart card readers and smart cards to sign in to applications within their streaming session\.

To ensure that your users can use their smart cards for Windows sign in to Active Directory\-joined streaming instances and for in\-session authentication for streaming applications, you must:
+ Use an image that meets the following requirements:
  + The image must be created from a base image published by AWS on or after December 28, 2020\. For more information, see [AppStream 2\.0 Base Image and Managed Image Update Release Notes](base-image-version-history.md)\.
  + The image must use a version of the AppStream 2\.0 agent released on or after January 4, 2021\. For more information, see [AppStream 2\.0 Agent Release Notes](agent-software-versions.md)\.
+ Enable **Smart card sign in for Active Directory** on the AppStream 2\.0 stack that your users access for streaming sessions, as described in this section\.
**Note**  
This setting controls only the authentication method that can be used for Windows sign in to an AppStream 2\.0 streaming instance \(fleet or image builder\)\. It doesn't control the authentication method that can be used for in\-session authentication, after a user signs in to a streaming instance\.
+ Ensure that your users have AppStream 2\.0 client version 1\.1\.257 or later installed\. For more information, see [AppStream 2\.0 Client Release Notes](client-release-versions.md)\.

By default, password sign in for Active Directory is enabled on AppStream 2\.0 stacks\. You can enable smart card sign in for Active Directory by performing the following steps in the AppStream 2\.0 console\.

**To enable smart card sign in for Active Directory by using the AppStream 2\.0 console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**\.

1. Choose the stack for which you want to enable smart card authentication for Active Directory\.

1. Choose the **User Settings** tab, and then expand the **Clipboard, file transfer, print to local device, and authentication permissions** section\.

1. For **Smart card sign in for Active Directory**, choose **Enabled**\.

   You can also enable **Password sign in for Active Directory**, if it's not already enabled\. At least one authentication method must be enabled\.

1. Choose **Update**\.

Alternatively, you can enable smart card sign in for Active Directory by using the AppStream 2\.0 API, an AWS SDK, or the AWS Command Line Interface \(AWS CLI\)\.

##### Smart Card Redirection<a name="feature-support-USB-devices-qualified-smart-cards-support"></a>

When the AppStream 2\.0 client is installed, smart card redirection is enabled by default\. When this feature is enabled, users can use smart card readers that are connected to their local computer and their smart cards during AppStream 2\.0 streaming sessions without USB redirection\. During AppStream 2\.0 streaming sessions, users' smart card readers and smart cards remain accessible for use with local applications\. The AppStream 2\.0 client redirects the smart card API calls from users’ streaming applications to their local smart card\. 

**Note**  
Smart card redirection is currently not supported for Linux\-based fleet instances\.

**Note**  
If your smart card requires middleware software to operate, the middleware software must be installed on both the user’s device, and the AppStream 2\.0 streaming instance\.

You can disable smart card redirection during client installation on managed devices\. For more information, see [Choose Whether to Disable Smart Card Redirection](install-client-configure-settings.md#disable-local-smart-card-support-client)\. If you disable smart card redirection, your users can't use their smart card reader and smart card during an AppStream 2\.0 streaming session without USB redirection\. In this case, you must [qualify the device](qualify-usb-devices.md)\. After you qualify the device, users must [share the device with AppStream 2\.0](client-application-windows-user.md#client-application-windows-how-to-share-usb-devices-user)\. When smart card redirection is disabled, during users' AppStream 2\.0 streaming sessions, their smart card reader and smart card are not accessible for use with local applications\.

#### Drawing Tablets<a name="feature-support-drawing-tablets"></a>

Drawing tablets, also known as pen tablets, are computer input devices that let users draw with a stylus \(pen\)\. With AppStream 2\.0, your users can connect a drawing tablet, such as a Wacom drawing tablet, to their local computer and use the tablet with their streaming applications\.

Following are requirements and considerations for enabling your users to use drawing tablets with their streaming applications\.
+ To enable your users to use this feature, you must configure your AppStream 2\.0 fleet to use an image that runs Windows Server 2019\.
+ To use this feature, users must access AppStream 2\.0 by using the AppStream 2\.0 client, or through the Google Chrome or Mozilla Firefox browsers only\.
+ Streaming applications must support Windows Ink technology\. For more information, see [Pen interactions and Windows Ink in Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/input/pen-and-stylus-interactions)\.
+ Some applications, such GIMP, must detect drawing tablets on the streaming instance to support pressure sensitivity\. If this is the case, your users must use the AppStream 2\.0 client to access AppStream 2\.0 and stream these applications\. In addition, you must qualify your users' drawing tablets, and users must share their drawing tablets with AppStream 2\.0 every time they start a new streaming session\. For more information, see [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)\.
+ This feature is not supported on Chromebooks\.

To get started with using drawing tablets during application streaming sessions, users connect their drawing tablet to their local computer with USB, share the device with AppStream 2\.0 if required for pressure sensitivity detection, and then use the AppStream 2\.0 client or a [supported web browser](requirements-and-features-web-browser-admin.md#drawing-tablet-support-web-access-admin) to start an AppStream 2\.0 streaming session\.

#### Keyboard Shortcuts<a name="feature-support-keyboard-shortcuts"></a>

Most operating system keyboard shortcuts are supported\. Supported keyboard shortcuts include Alt \+ Tab, Clipboard shortcuts \(Ctrl \+ X, Ctrl \+ C, Ctrl\+ V\), Esc, and Alt \+ F4

#### Relative Mouse Offset<a name="feature-support-relative-mouse-offset"></a>

By default, during users' streaming sessions, AppStream 2\.0 transmits information about mouse movements to the streaming instance by using absolute coordinates and rendering the mouse movements locally\. For graphics\-intensive applications, such as computer\-aided design \(CAD\)/computer\-aided manufacturing \(CAM\) software or video games, mouse performance improves when relative mouse mode is enabled\. Relative mouse mode uses relative coordinates, which represent how far the mouse moved since the last frame, rather than the absolute x\-y coordinate values within a window or screen\. When relative mouse mode is enabled, AppStream 2\.0 renders the mouse movements remotely\.

Users can enable this feature during their AppStream 2\.0 streaming sessions by doing either of the following:
+ Pressing Ctrl\+Shift\+F8
+ Choosing **Relative Mouse Position \[Ctrl\+Shift\+F8\]** from the **Settings **menu on the AppStream 2\.0 toolbar in the top left area of their streaming session window\. This method works when they use classic mode or **Desktop View**\.