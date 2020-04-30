# AppStream 2\.0 Client Application for Windows<a name="client-application-windows-user"></a>

The following information helps you use the AppStream 2\.0 client for Windows to connect to AppStream 2\.0 and stream applications\.

**Topics**
+ [Features](#client-application-windows-features-user)
+ [Requirements](#client-application-windows-requirements-user)
+ [Setup](#client-application-windows-installation-user)
+ [Connect to AppStream 2\.0](#client-application-windows-start-streaming-session-user)
+ [USB Devices](#share-usb-devices-with-session-user)
+ [Monitors and Display Resolution](#client-application-monitors-display-resolution-user)
+ [Logging](#client-application-windows-how-to-enable-diagnostic-logging-user)

## Features<a name="client-application-windows-features-user"></a>

The AppStream 2\.0 client for Windows is an application that you install on your Windows PC\. This application provides additional capabilities that are not available when you access AppStream 2\.0 by using a web browser\. For example, the AppStream 2\.0 client lets you do the following:
+ Use more than two monitors or 4K resolution\.
+ Use your USB devices with applications streamed through AppStream 2\.0\.
+ Use keyboard shortcuts during your streaming sessions\.
+ Access your local drives and folders during your streaming sessions\.
+ Interact with your remote streaming applications in much the same way as you interact with locally installed applications\.

## Requirements<a name="client-application-windows-requirements-user"></a>

The AppStream 2\.0 client for Windows must be installed on a PC that meets the following requirements:
+ Operating system — Windows 7, Windows 8, or Windows 10 \(32\-bit or 64\-bit\)
+ RAM — 2 GB minimum
+ Hard drive space — 200 MB minimum

In addition, to install the AppStream 2\.0 USB driver for USB driver support, you must have local administrator rights on your PC\.

## Setup<a name="client-application-windows-installation-user"></a>

Follow these steps to install the client\.

1. On the PC where you want to install the AppStream 2\.0 client, download the AppStream 2\.0 client for Windows application from [AppStream 2\.0 supported clients](https://clients.amazonappstream.com)\.

1. Navigate to the location where you downloaded the application \.exe file, and then double\-click the file to begin the installation\.
**Important**  
Contact your network administrator if nothing happens when you double\-click the file or if an error message is displayed\. Your organization might be using antivirus software that prevents the AppStream 2\.0 client installation program from running\.

1. If a message notifies you that Windows Defender SmartScreen prevented an unrecognized app from starting, choose the **More info** link\. For **App**, verify that **AmazonAppStreamClientSetup\_**<*version\-number*>**\.exe** is displayed, and then choose **Run anyway**\.

1. The installation wizard displays links to the AWS Customer Agreement, AWS Service Terms, and the AWS Privacy Notice, and third\-party notices\. Review this information, and then choose **Next**\.

1. On the **Client Diagnostics** page, to enable the AppStream 2\.0 client to automatically upload device logs to help with troubleshooting issues, keep **Client logging** selected, and then choose **Next**\.

1.  On the **Optional Components** page, to enable your USB devices to be used with streaming applications, select the **AppStream 2\.0 Client USB Driver** check box, and then choose **Finish**\.

1. If the **AppStream 2\.0 USB driver** wizard setup wizard opens, choose **Install**\.

1. If prompted by User Account Control to choose whether to allow the app to make changes to your device, choose **Yes**\.

1. When a message notifies you that the USB driver installation is complete, choose **Close**\. 

   The AppStream 2\.0 sign\-in page opens\. For information about how to connect to AppStream 2\.0 and start an application streaming session, see [How to Connect to AppStream 2\.0](#client-application-windows-how-to-connect-user)\.

## Connect to AppStream 2\.0<a name="client-application-windows-start-streaming-session-user"></a>

After the AppStream 2\.0 client for Windows is installed on your PC, you can use it to connect to AppStream 2\.0\.

### AppStream 2\.0 Client Connection Modes<a name="client-application-windows-connection-modes-user"></a>

The AppStream 2\.0 client provides two connection modes: *Native application mode* and *classic mode*\. The connection mode that you choose determines the options that are available to you during application streaming, and how your streaming applications function and display\.

**Native application mode**

Native application mode lets you work with remote streaming applications in much the same way that you work with applications that are installed on your local PC\. 

When you connect to AppStream 2\.0 in native application mode, the AppStream 2\.0 Application Launcher window opens and displays the list of applications that are available for you to stream\. When you open a streaming application in this mode, the AppStream 2\.0 Application Launcher window remains open, and the application opens in its own window\. During your streaming session, the remote streaming application functions in much the same way as a locally installed application\. The application icon is displayed in the taskbar of your local PC, just as the icons do for your local applications\. Unlike the icons for your local applications, the icons for your streaming applications in native application mode include the AppStream 2\.0 logo\.

During your AppStream 2\.0 streaming session, you can switch quickly between your locally installed applications and your remote streaming applications by clicking the taskbar icon of the remote or local application you want to work with\. You can also switch AppStream 2\.0 connection modes\. If you want to work in classic mode instead, you can switch from native application mode to classic mode\.

**Classic mode**

When you use classic application mode, you work with remote streaming applications in the AppStream 2\.0 session window\. If your administrator has made more than one application available to you, you can open multiple applications during your session\. All applications that you open are displayed in the same AppStream 2\.0 session window\. 

When you connect to AppStream 2\.0 in classic mode, the AppStream 2\.0 Application Launcher window opens and displays the list of applications that are available for you to stream\. When you open a streaming application in this mode, the Application Launcher window closes, and the application opens in the AppStream 2\.0 session window\.

If your administrator has not disabled native application mode, you can switch from classic mode to native application mode\. For more information, see [How to Switch AppStream 2\.0 Connection Modes](#client-application-windows-how-to-switch-connection-modes-user)\.

### How to Connect to AppStream 2\.0<a name="client-application-windows-how-to-connect-user"></a>

Follow these steps to connect to AppStream 2\.0 and start an application streaming session\.

1. On your local PC where the AppStream 2\.0 client is installed, in the lower left of your screen, choose the Windows search icon on the taskbar, and enter **AppStream** in the Search box\. 

1. In the search results, select ** Amazon AppStream** to start the AppStream 2\.0 client\. 

1. On the AppStream 2\.0 sign\-in page, do either of the following:
   + To use native application mode, keep the **Start in native application mode** check box selected\. 
   + To use classic mode, clear the **Start in native application mode** check box\. 

1. If your AppStream 2\.0 administrator has provided you with a web address \(URL\) to use to connect to AppStream 2\.0 for application streaming, enter the URL, and choose **Connect**\. 

If you want to use your USB devices with streaming applications, you must first share your device with AppStream 2\.0\. For more information, see [USB Devices](#share-usb-devices-with-session-user)\.

### How to Switch AppStream 2\.0 Connection Modes<a name="client-application-windows-how-to-switch-connection-modes-user"></a>

If your administrator has not disabled native application mode for your streaming sessions, you can switch between native application mode and classic mode\.

**To switch from native application mode to classic mode**

1. In the upper left of the AppStream 2\.0 Application Launcher window, choose the **Settings** icon, and then choose **Switch to classic mode**\. 

1. When you switch to classic mode, the Application Launcher window closes and the AppStream 2\.0 session window opens\. Any application that you are streaming in native application mode opens in the AppStream 2\.0 session window\.

Follow these steps to switch from classic mode to native application mode\.

**To switch from classic mode to native application mode**

1. In the upper left of the AppStream 2\.0 session window, choose the **Settings** icon, and then choose **Switch to native application mode**\.

1. When you switch from classic mode back to native application mode, the AppStream 2\.0 session window closes and the AppStream 2\.0 Application Launcher window opens\. Any application that you are streaming in classic mode opens in a separate window\.

## USB Devices<a name="share-usb-devices-with-session-user"></a>

To use a USB device with streaming applications, you must share the device with AppStream 2\.0 every time you start a new streaming session\. 

1. Use the AppStream 2\.0 client to start a streaming session\.

1. In the top left area, choose the **Settings** icon, and then choose **USB Devices**\.

1. If your USB device is connected to your computer, the USB device name appears in the dialog box\. If your USB device is not detected, contact your AppStream 2\.0 administrator for assistance\.

1. Switch the **Share** toggle key next to the name of the USB device that you want to share with the streaming session\.

   Your USB device is now available for use with your streaming applications\.
**Important**  
USB devices can't be simultaneously used between local and remote applications\. So after you share a USB device with a streaming session, you can't use it with applications on your local computer\. To use your USB device on your local computer, switch the **Share** toggle key next to the name of the USB device that you want to use locally\. This disables sharing with the streaming session\. 

1. You can also enable your USB device to automatically connect when a new streaming session starts\. To do so, select the option next to the toggle key for the USB device that you want to connect\. After you enable this option, when your next streaming session starts, the USB device is connected automatically\. 

## Monitors and Display Resolution<a name="client-application-monitors-display-resolution-user"></a>

The AppStream 2\.0 client supports the following:
+ Multiple monitors \(up to 2K resolution\) — Up to 4 monitors and a maximum display resolution of 2560x1440 pixels per monitor
+ Multiple monitors \(4K resolution\) — Up to 2 monitors and a maximum display resolution of 4096x2160 pixels per monitor

## Logging<a name="client-application-windows-how-to-enable-diagnostic-logging-user"></a>

To help with troubleshooting if an issue with the AppStream 2\.0 client occurs, you can enable diagnostic logging\. The log files that are sent to AppStream 2\.0 \(AWS\) include detailed information about your device and connection to the AWS network\. You can enable automatic log uploads so that these files are sent to AppStream 2\.0 \(AWS\) automatically\. You can also upload log files on an as\-needed basis, before or during an AppStream 2\.0 streaming session\.

**Automatic logging**

You can enable automatic logging when you install the AppStream 2\.0 client\. For information about how to enable automatic logging when you install the AppStream 2\.0 client, see step 5 in [Setup](#client-application-windows-installation-user)\. 

**On\-demand logging**

If an issue occurs during an AppStream 2\.0 streaming session, you can also send log files on an as\-needed basis\. If an issue occurs that causes the AppStream 2\.0 client to stop responding, a notification prompts you to choose whether to send an error report and the associated log files to AppStream 2\.0 \(AWS\)\.

The following procedures describe how to send log files before you sign in to an AppStream 2\.0 streaming session and during an AppStream 2\.0 streaming session\.

**To send log files before an AppStream 2\.0 streaming session**

1. On your local PC where the AppStream 2\.0 client is installed, in the lower left of your screen, choose the Windows search icon on the taskbar, and enter **AppStream** in the Search box\. 

1. In the search results, select ** Amazon AppStream** to start the AppStream 2\.0 client\. 

1. At the bottom of the AppStream 2\.0 sign\-in page, choose the **Send Diagnostic Logs** link\.

1. To continue connecting to AppStream 2\.0, if your AppStream 2\.0 administrator has provided you with a web address \(URL\) to use to connect to AppStream 2\.0 for application streaming, enter the URL, and then choose **Connect**\. 

**To send log files during an AppStream 2\.0 streaming session**

1. If you are not already connected to AppStream 2\.0 and streaming an application, use the AppStream 2\.0 client to start a streaming session\.

1. In the upper right of the AppStream 2\.0 session window, choose the **Profiles** icon, and then choose **Send Diagnostic Logs**\. 