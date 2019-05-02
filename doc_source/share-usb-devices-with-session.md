# Share a USB Device with an AppStream 2\.0 Streaming Session<a name="share-usb-devices-with-session"></a>

Before users share their USB devices with an AppStream 2\.0 session, the USB devices must be qualified\. Otherwise, when users start a streaming session, their USB device is not detected by AppStream 2\.0 and cannot be shared with the session\. For more information, see [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)\. 

To help your users understand how to share their USB devices with AppStream 2\.0 streaming sessions, you can provide them with the following information\. 

**Guidance for Users**

To use a USB device with streaming applications, you must share the device with AppStream 2\.0 every time when you start a new streaming session\. 

1. Use the AppStream 2\.0 client to start a streaming session\.

1. In the top left area, choose the **Settings** icon, and then choose **USB Devices**\.

1. If your USB device is connected to your computer, the USB device name appears in the dialog box\. If your USB device is not detected, contact your network administrator for assistance\.

1. Switch the **Share** toggle key next to the name of the USB device that you want to share with the streaming session\.

   Your USB device is now available for use with your streaming applications\.
**Important**  
USB devices can't be simultaneously used between local and remote applications\. So after you share a USB device with a streaming session, you can't use it with applications on your local computer\. To use your USB device on your local computer, switch the **Share** toggle key next to the name of the USB device that you want to use locally\. This disables sharing with the streaming session\. 

1. You can also enable your USB device to automatically connect when a new streaming session starts\. To do so, select the option next to the toggle key for the USB device that you want to connect\. After you enable this option, when your next streaming session starts, the USB device is automatically connected\. 