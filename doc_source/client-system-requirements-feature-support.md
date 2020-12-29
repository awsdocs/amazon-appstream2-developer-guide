# System Requirements and Feature Support \(AppStream 2\.0 Client\)<a name="client-system-requirements-feature-support"></a>

This topic provides information to help you understand the requirements for the AppStream 2\.0 client and supported features\.

## System Requirements and Considerations<a name="client-system-requirements"></a>

The AppStream 2\.0 client requires the following:
+ Operating system — Windows 7, Windows 8, or Windows 10 \(32\-bit or 64\-bit\)
+ Microsoft Visual C\+\+ 2015 Redistributable or later\. For information about the latest Visual C\+\+ redistributable packages for Visual Studio 2015, 2017, and 2019, see [The latest supported Visual C\+\+ downloads](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads) in the Microsoft Support documentation\.
+ RAM — 2 GB minimum
+ Hard drive space — 200 MB minimum
+ Local administrator rights — Used if you want to install the AppStream 2\.0 USB driver for USB driver support\.
+ An AppStream 2\.0 image that uses the latest AppStream 2\.0 agent or agent versions published on or after November 14, 2018\. For information about AppStream 2\.0 agent versions, see [AppStream 2\.0 Agent Release Notes](agent-software-versions.md)\.

**Note**  
We recommend an internet connection for AppStream 2\.0 client installation\. In some cases, the client can't be installed on a PC that is not connected to the internet, or USB devices might not work with applications streamed from AppStream 2\.0\. For more information, see [Troubleshooting AppStream 2\.0 User Issues](troubleshooting-client.md)\.

## Feature and Device Support<a name="client-feature-support"></a>

The AppStream 2\.0 client supports the following features and devices\.

**Topics**
+ [Native Application Mode](#feature-support-native-application-mode)
+ [Automatic and On\-Demand Diagnostic Log Uploads](#feature-support-diagnostic-log-upload)
+ [Peripheral Devices](#feature-support-peripheral-devices)

### Native Application Mode<a name="feature-support-native-application-mode"></a>

Native application mode provides a familiar experience for your users during their AppStream 2\.0 streaming sessions\. When your users connect to AppStream 2\.0 in this mode, they can work with their remote streaming applications in much the same way that they work with applications that are installed on their local PC\. Each streaming application in native application mode opens in its own window, and application icons appear on the taskbar on your users' local PC\.

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
With certain exceptions, USB redirection is required for the AppStream 2\.0 client to support USB devices\. When USB redirection is required for a device, the device must be qualified before it can be used with AppStream 2\.0 streaming sessions\. For more information, see [USB Redirection](#feature-support-USB-devices-qualified)\.

**Topics**
+ [Multiple Monitors](#feature-support-multiple-monitors)
+ [Real\-Time Audio\-Video](#feature-support-real-time-av)
+ [USB Redirection](#feature-support-USB-devices-qualified)
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

#### Real\-Time Audio\-Video<a name="feature-support-real-time-av"></a>

AppStream 2\.0 supports real\-time audio\-video \(AV\) by redirecting local webcam video input to AppStream 2\.0 streaming sessions\. This capability enables your users to use their local webcam for video and audio conferencing within an AppStream 2\.0 streaming session\. With real\-time AV and support for real\-time audio, your users can collaborate by using familiar video and audio conferencing applications without having to leave their AppStream 2\.0 streaming session\.

When a user starts a video conference from within an AppStream 2\.0 streaming session, AppStream 2\.0 compresses the webcam video and microphone audio input locally before transmitting this data over a secure channel to a streaming instance\. During their streaming sessions, users can enable audio and video input by using the AppStream 2\.0 toolbar\. If users have more than one webcam \(for example, if they have a USB webcam that is connected to their local computer and a built\-in webcam\), they can also choose which webcam to use during their streaming session\.

To enable this feature for your users, you must:
+ Use an AppStream 2\.0 image that uses a version of the AppStream 2\.0 agent released on or after December 17, 2020\.
+ Ensure that version 1\.1\.257 or later of the AppStream 2\.0 client is installed on your users' computers\. To use this feature, users must connect to their streaming session by using the AppStream 2\.0 client\.

  For guidance that you can provide to your users to help them use real\-time AV, see [Video and Audio Conferencing](client-application-windows-user.md#client-application-windows-how-to-use-local-webcam-user)\.

Local webcam video input redirection is already enabled by default when the AppStream 2\.0 client is installed\. Because USB redirection isn't used for this feature, you don't need to qualify webcams, and users don't need to share these devices with AppStream 2\.0 to use them during streaming sessions\.

#### USB Redirection<a name="feature-support-USB-devices-qualified"></a>

USB redirection is required for most local USB devices to be used during AppStream 2\.0 streaming sessions\. When USB redirection is required, you must [qualify the device](qualify-usb-devices.md) before your users can use it during their AppStream 2\.0 streaming sessions\. After you qualify the device, users must [share the device with AppStream 2\.0](client-application-windows-user.md#client-application-windows-how-to-share-usb-devices-user)\. With USB redirection, during AppStream 2\.0 streaming sessions, users' devices are not accessible for use with local applications\. In other cases, USB devices are already enabled for use with AppStream 2\.0 and no further configuration is required\.

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