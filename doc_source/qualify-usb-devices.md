# Qualify USB Devices for Use with Streaming Applications<a name="qualify-usb-devices"></a>

To qualify your USB devices so that they can be used with streaming applications, perform these steps\. 

1. If you haven't already done so, install the AppStream 2\.0 client\. For information, see [Install and Configure the AppStream 2\.0 Client](install-configure-client.md)\.

1. Connect the USB device that you want to qualify to your computer\.

1. Navigate to C:\\Users\\<logged\-in\-user>\\AppData\\Local\\AppStreamClient, and double\-click **dcvusblist\.exe**\.

1. In the **DCV \- USB devices** dialog box, the list of USB devices that are connected to your local computer displays\. The **Filter** column displays the filter string for every USB device\. Right\-click the list entry for a USB device that you want to enable, and choose **Copy filter string**\. 

1. On your desktop, choose the Windows **Start** button, and search for Notepad\. Double\-click Notepad to open a new file, copy the filter string to the file, and save it\. Later, you'll use the filter string to qualify the USB device\.

1. Launch a new image builder\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

1. Create a streaming URL for your image builder, and use it to connect to the image builder with the AppStream 2\.0 client\. 

1. Log in as **Administrator**\. 

1. If your USB device requires you to install drivers before you use it, download and install the drivers on the image builder\. For example, if you use the Connexion 3D mouse, you must download and install the required Connexion drivers on the image builder\. 

1. On your image builder desktop, choose the Windows **Start** button, and search for Notepad\. Right\-click **Notepad**, and choose **Run as Administrator**\.

1. Choose **File**, **Open**, and open the following file: C:\\ProgramData\\Amazon\\Photon\\DCV\\usb\_device\_whitelist\.txt\. You can also whitelist an entire category of devices or all devices from a specific manufacturer by using wildcard expressions in the usb\_device\_whitelist\.txt file\. 

1. Copy the filter string from your local computer to the image builder, add it to **usb\_device\_whitelist\.txt**, and save the file\. You can configure USB devices to connect automatically when a new streaming session starts\. By default, this feature is disabled for all USB devices\. To enable this feature, append ",1" at the end of the filter string that you copy for a device\. 

1. Disconnect from your image builder, restart it, and reconnect to it by using the AppStream 2\.0 client application\. 

1. On the image builder, test your USB device to confirm that it works as expected\.

1. To use the USB device in an AppStream 2\.0 session, you must share the device with the session first\. For more information, see [Share a USB Device with an AppStream 2\.0 Streaming Session](share-usb-devices-with-session.md)\. After you finish testing, you can provide the information in the *Guidance for Users* section of this topic to your users\.

1. If the USB device works with the image builder as expected, create an image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image](tutorial-image-builder.md)\.

1. After you finish creating the image, update your AppStream 2\.0 fleet to use the new image\.