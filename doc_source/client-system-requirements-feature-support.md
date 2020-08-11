# System Requirements and Feature Support<a name="client-system-requirements-feature-support"></a>

This topic provides information to help you understand the requirements for the AppStream 2\.0 client and supported features\.

## System Requirements and Considerations<a name="client-system-requirements"></a>

The AppStream 2\.0 client requires the following:
+ Operating system — Windows 7, Windows 8, or Windows 10 \(32\-bit or 64\-bit\)
+ RAM — 2 GB minimum
+ Hard drive space — 200 MB minimum
+ Local administrator rights — Used if you want to install the AppStream 2\.0 USB driver for USB driver support\.
+ An AppStream 2\.0 image that uses the latest AppStream 2\.0 agent or agent versions published on or after November 14, 2018\. For information about AppStream 2\.0 agent versions, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.

**Note**  
We recommend an internet connection for AppStream 2\.0 client installation\. In some cases, the client can't be installed on a PC that is not connected to the internet, or USB devices might not work with applications streamed from AppStream 2\.0\. For more information, see [Troubleshooting AppStream 2\.0 User Issues](troubleshooting-client.md)\.

## Feature and Device Support<a name="client-feature-support"></a>

The AppStream 2\.0 client supports the following features and peripheral devices\.

**Topics**
+ [Native Application Mode](#feature-support-native-application-mode)
+ [Automatic and On\-Demand Diagnostic Log Uploads](#feature-support-diagnostic-log-upload)
+ [Peripheral Devices](#feature-support-peripheral-devices)

### Native Application Mode<a name="feature-support-native-application-mode"></a>

Native application mode provides a familiar experience for your users during their AppStream 2\.0 streaming sessions\. When your users connect to AppStream 2\.0 in this mode, they can work with their remote streaming applications in much the same way that they work with applications that are installed on their local PC\. Each streaming application in native application mode opens in its own window, and application icons appear on the taskbar on your users' local PC\.

If you want your users to connect to AppStream 2\.0 in classic mode only, you can configure the `NativeAppModeDisabled` registry value to disable native application mode\. For more information, see [Choose Whether to Disable Native Application Mode](install-client-configure-settings.md#disable-native-application-mode-client)\.

For more information about native application mode and classic mode, and for guidance that you can provide to your users, see [AppStream 2\.0 Client Connection Modes](client-application-windows-user.md#client-application-windows-connection-modes-user)\.

**Requirements**

To enable this feature for your users, you must use an image that uses a [version of the AppStream 2\.0 agent](agent-software-versions.md) released on or after February 19, 2020\. In addition, version 1\.1\.129 or later of the AppStream 2\.0 client must be installed on your users' PCs\. For more information about client versions, see [AppStream 2\.0 Client Version History](client-release-versions.md)\.

If AppStream 2\.0 client version 1\.1\.129 or later is installed on your users' PC, but you are not using an image that uses an agent version released on or after February 19, 2020, the client falls back to classic mode even if native application mode is selected\.

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

The AppStream 2\.0 client provides the following support for peripheral devices such as monitors, mice, keyboards, and drawing tablets\.

**Note**  
With certain exceptions, USB redirection is required for the AppStream 2\.0 client to support USB devices\. When USB redirection is required for a device, the device must be qualified before it can be used with AppStream 2\.0 streaming sessions\. For more information, see [USB Devices Qualified by AppStream 2\.0](#feature-support-USB-devices-qualified)\.

**Topics**
+ [Multiple Monitors \(up to 2K Resolution\)](#feature-support-multiple-monitors-2K)
+ [Multiple Monitors \(up to 4K Resolution\)](#feature-support-multiple-monitors-4K)
+ [USB Devices Qualified by AppStream 2\.0](#feature-support-USB-devices-qualified)
+ [Drawing Tablets](#feature-support-drawing-tablets)
+ [Keyboard Shortcuts](#feature-support-keyboard-shortcuts)
+ [Relative Mouse Offset](#feature-support-relative-mouse-offset)

#### Multiple Monitors \(up to 2K Resolution\)<a name="feature-support-multiple-monitors-2K"></a>

The following AppStream 2\.0 instance types support up to 4 monitors and a maximum display resolution of 2560x1600 pixels per monitor: General Purpose, Memory Optimized, Compute Optimized, Graphics Design, and Graphics Pro\.

#### Multiple Monitors \(up to 4K Resolution\)<a name="feature-support-multiple-monitors-4K"></a>

The following AppStream 2\.0 instance types support up to 2 monitors and a maximum display resolution of 4096x2160 pixels per monitor: Graphics Design and Graphics Pro\.

#### USB Devices Qualified by AppStream 2\.0<a name="feature-support-USB-devices-qualified"></a>

With certain exceptions, USB redirection is required for the AppStream 2\.0 client to support USB devices\. When USB redirection is required for a device, you must qualify it before your users can use the device during their AppStream 2\.0 streaming sessions\.

For drawing tablets, USB redirection might not be required\. However, if your users are streaming an application such as the Gnu Image Manipulation Program \(GIMP\), which requires USB redirection to support pressure sensitivity, you must qualify the device\. For step\-by\-step guidance, see [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)\.

#### Drawing Tablets<a name="feature-support-drawing-tablets"></a>

Drawing tablets, also known as pen tablets, are computer input devices that let users draw with a stylus \(pen\)\. With AppStream 2\.0, your users can connect a drawing tablet, such as a Wacom drawing tablet, to their local computer and use the tablet with their streaming applications\.

Following are requirements and considerations for enabling your users to use drawing tablets with their streaming applications\.
+ To enable your users to use this feature, you must configure your AppStream 2\.0 fleet to use an image that runs Windows Server 2019\.
+ To use this feature, users must access AppStream 2\.0 by using the AppStream 2\.0 client, or through the Google Chrome or Mozilla Firefox browsers only\.
+ Streaming applications must support Windows Ink technology\. For more information, see [Pen interactions and Windows Ink in Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/input/pen-and-stylus-interactions)\.
+ Some applications, such GIMP, must detect drawing tablets on the streaming instance to support pressure sensitivity\. If this is the case, your users must use the AppStream 2\.0 client to access AppStream 2\.0 and stream these applications\. In addition, you must qualify your users' drawing tablets, and users must share their drawing tablets with AppStream 2\.0 every time they start a new streaming session\.
+ This feature is not supported on Chromebooks\.

To get started with using drawing tablets during application streaming sessions, users connect their drawing tablet to their local computer with USB, share the device with AppStream 2\.0 if required for pressure sensitivity detection, and then use the AppStream 2\.0 client or a [supported web browser](access-through-web-browser-admin.md#drawing-tablet-support-web-access-admin) to start an AppStream 2\.0 streaming session\.

#### Keyboard Shortcuts<a name="feature-support-keyboard-shortcuts"></a>

Most operating system keyboard shortcuts are supported\. Supported keyboard shortcuts include Alt \+ Tab, Clipboard shortcuts \(Ctrl \+ X, Ctrl \+ C, Ctrl\+ V\), Esc, and Alt \+ F4

#### Relative Mouse Offset<a name="feature-support-relative-mouse-offset"></a>

This feature can be used with applications such as Minecraft\.