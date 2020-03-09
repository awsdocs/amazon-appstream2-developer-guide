# System Requirements and Feature Support<a name="client-system-requirements-feature-support"></a>

This topic provides information to help you understand the requirements for the AppStream 2\.0 client and supported features\.

## System Requirements<a name="client-system-requirements"></a>

The AppStream 2\.0 client requires the following:
+ Operating system — Windows 7, Windows 8, or Windows 10 \(32\-bit or 64\-bit\)
+ RAM — 2 GB minimum
+ Hard drive space — 200 MB minimum
+ Local administrator rights — Used if you want to install the AppStream 2\.0 USB driver for USB driver support
+ An AppStream 2\.0 image that uses the latest AppStream 2\.0 agent or agent versions published on or after November 14, 2018\. For information about AppStream 2\.0 agent versions, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.

## Feature Support<a name="client-feature-support"></a>

The AppStream 2\.0 client supports the following features\.

**Topics**
+ [Multiple Monitors \(up to 2K Resolution\)](#feature-support-multiple-monitors-2K)
+ [Multiple Monitors \(up to 4K Resolution\)](#feature-support-multiple-monitors-4K)
+ [USB Devices Qualified by AppStream 2\.0](#feature-support-USB-devices-qualified)
+ [Native Application Mode](#feature-support-native-application-mode)
+ [Uploading Diagnostic Logs](#feature-support-diagnostic-log-upload)
+ [Keyboard Shortcuts](#feature-support-keyboard-shortcuts)
+ [Relative Mouse Offset](#feature-support-relative-mouse-offset)

### Multiple Monitors \(up to 2K Resolution\)<a name="feature-support-multiple-monitors-2K"></a>

The following AppStream 2\.0 instance types support up to 4 monitors and a maximum display resolution of 2560x1440 pixels per monitor: General Purpose, Memory Optimized, Compute Optimized, Graphics Design, and Graphics Pro\.

### Multiple Monitors \(up to 4K Resolution\)<a name="feature-support-multiple-monitors-4K"></a>

The following AppStream 2\.0 instance types support up to 2 monitors and a maximum display resolution of 4096x2160 pixels per monitor: Graphics Design and Graphics Pro\.

### USB Devices Qualified by AppStream 2\.0<a name="feature-support-USB-devices-qualified"></a>

All categories of the Connexion 3D Mouse are already qualified by AppStream 2\.0\. By default, all USB devices are disabled\. To enable your users to use other USB devices with AppStream 2\.0, you must qualify the devices\. For more information, see [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)\.

### Native Application Mode<a name="feature-support-native-application-mode"></a>

Native application mode provides a familiar experience for your users during their AppStream 2\.0 streaming sessions\. When your users connect to AppStream 2\.0 in this mode, they can work with their remote streaming applications in much the same way that they work with applications that are installed on their local PC\. Each streaming application in native application mode opens in its own window, and application icons appear on the taskbar on your users' local PC\.

If you want your users to connect to AppStream 2\.0 in classic mode only, you can configure the **NativeAppModeDisabled** registry value to disable native application mode\. For more information, see [Choose Whether to Disable Native Application Mode](install-client-configure-settings.md#disable-native-application-mode-client)\.

For more information about native application mode and classic mode, and for guidance that you can provide to your users, see [AppStream 2\.0 Client Connection Modes](client-application-windows-user.md#client-application-windows-connection-modes-user)\.

**Requirements**

To enable this feature for your users, you must use an image that uses a [version of the AppStream 2\.0 agent](agent-software-versions.md) released on or after February 19, 2020\. In addition, version 1\.1\.129 or later of the AppStream 2\.0 client must be installed on your users' PCs\. For more information about client versions, see [AppStream 2\.0 Client Version History](client-release-versions.md)\.

If AppStream 2\.0 client version 1\.1\.129 or later is installed on your users' PC, but you are not using an image that uses an agent version released on or after February 19, 2020, the client falls back to classic mode—even if native application mode is selected\.

**Known Issues**

When users try to dock or undock tabs in one browser window into separate windows during a streaming session in native application mode, their remote streaming browser doesn't work the same way as a local browser\. To perform this task during a streaming session in native application mode, users must press the Alt key until their browser tabs are docked into separate browser windows\. 

### Uploading Diagnostic Logs<a name="feature-support-diagnostic-log-upload"></a>

To help with troubleshooting issues that your users may experience when using the AppStream 2\.0 client, you or your users can configure the AppStream 2\.0 client to upload diagnostic logs to AWS automatically\. Alternatively, your users can upload diagnostic logs manually, on an as\-needed basis\. Diagnostic log uploads can be enabled in the following ways:
+ You can enable automatic uploads of diagnostic logs when you install the AppStream 2\.0 client on user PCs that you manage\. For more information, see [Configure Additional AppStream 2\.0 Client Settings for Your Users](install-client-configure-settings.md#configure-client)\.
+ Your users can enable automatic uploads of diagnostic logs when they install the AppStream 2\.0 client on their PCs\. For guidance that you can provide your users to help them perform this task, see [Setup](client-application-windows-user.md#client-application-windows-installation-user)\.
+ Your users can enable automatic uploads of diagnostic logs after they install the client on their PCs by selecting the **Send Diagnostic Logs** link on the bottom of the AppStream 2\.0 client sign\-in page\. For guidance that you can provide your users to help them perform this task, see [Logging](client-application-windows-user.md#client-application-windows-how-to-enable-diagnostic-logging-user)\.
+ Your users can upload diagnostic logs on an as\-needed basis, if they experience an issue during an AppStream 2\.0 streaming session\. To do so, they choose the **Profiles** icon in the upper right of the AppStream 2\.0 session window, and then choose **Send Diagnostic Logs**\. For guidance that you can provide your users to help them perform this task, see [Logging](client-application-windows-user.md#client-application-windows-how-to-enable-diagnostic-logging-user)\.

Diagnostic logs do not contain sensitive information\. You can disable automatic diagnostic log uploads on user PCS that you manage, or your users can disable this feature themselves\. 

### Keyboard Shortcuts<a name="feature-support-keyboard-shortcuts"></a>

Most operating system keyboard shortcuts are supported\. Supported keyboard shortcuts include Alt \+ Tab, Clipboard shortcuts \(Ctrl \+ X, Ctrl \+ C, Ctrl\+ V\), Esc, and Alt \+ F4

### Relative Mouse Offset<a name="feature-support-relative-mouse-offset"></a>

This feature can be used with applications such as Minecraft\.