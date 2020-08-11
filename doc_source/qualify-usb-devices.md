# Qualify USB Devices for Use with Streaming Applications<a name="qualify-usb-devices"></a>

To qualify your users' USB devices so that the devices can be used with streaming applications, perform these steps\. 

1. If you haven't already done so, install the AppStream 2\.0 client\. For information, see [Install and Configure the AppStream 2\.0 Client](install-configure-client.md)\.

1. Connect the USB device that you want to qualify to your computer\.

1. Navigate to **C:\\Users\\<logged\-in\-user>\\AppData\\Local\\AppStreamClient**, and double\-click **dcvusblist\.exe**\.

1. In the **DCV \- USB devices** dialog box, the list of USB devices that are connected to your local computer displays\. The **Filter** column displays the filter string for every USB device\. Right\-click the list entry for a USB device that you want to enable, and choose **Copy filter string**\. 

1. On your desktop, choose the Windows **Start** button, and search for Notepad\. Double\-click **Notepad** to open a new file, copy the filter string to the file, and save it\. Later, you'll use the filter string to qualify the USB device\.

1. Launch a new image builder\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

1. After your image builder is in the **Running** state, perform the following steps to create a streaming URL and connect to the image builder by using the AppStream 2\.0 client\.

   1. With your image builder selected in the list, choose **Actions**, **Create streaming URL**\.

   1. In the **Create streaming URL** dialog box, choose **Copy link**, and copy and paste the web address into a separate file for later use\. You'll use this URL to reconnect to the image builder in step 12\.

   1. Choose **Launch in Client**\.

   1. If the **Launch Application** dialog box opens and prompts you to choose the application to use when opening the link, choose **Amazon AppStream**, **Open link**\. To prevent this dialog box from displaying the next time you perform this step to connect to an image builder, select the **Remember my choice for amazonappstream links** check box\.

   1. If the AppStream 2\.0 client displays links to the AWS Customer Agreement, AWS Service Terms, and the AWS Privacy Notice, and third\-party notices, review this information, and then choose **Finish**\. 

   1. If the client sign\-in page is displayed, the web address field is prepopulated with the streaming URL\. Choose **Connect**\. 

   1. If prompted, log in to the image builder as Administrator\. 

1. After you are connected to the image builder, if your USB device requires you to install drivers before you use it, download and install the drivers on the image builder\. For example, if you use the Connexion 3D mouse, you must download and install the required Connexion drivers on the image builder\. 

1. On your image builder desktop, choose the Windows **Start** button, and search for Notepad\. Right\-click **Notepad**, and choose **Run as Administrator**\.

1. Choose **File**, **Open**, and open the following file: `C:\ProgramData\Amazon\Photon\DCV\usb_device_whitelist.txt`\. You can also allow an entire category of devices or all devices from a specific manufacturer by using wildcard expressions in the `usb_device_whitelist.txt` file\. 

1. Copy the filter string from your local computer to the image builder\. The filter string for a specific USB device is a comma\-separated string of the following fields: **Name**, **Base Class**, **SubClass**, **Protocol**, **ID Vendor**, **ID Product**, **Support Autoshare**, and **Skip Reset**\. For detailed information about these strings, see [Working with USB Device Filter Strings](#USB-device-filter-strings)\.

1. Disconnect from your image builder, restart it, and reconnect to it by using the AppStream 2\.0 client\. To do so, open the AppStream 2\.0 client and paste the streaming URL that you created in step 7 into the client sign\-in web address field, and choose **Connect**\.

1. On the image builder, test your USB device to confirm that it works as expected\.

1. Before your users can use the USB device in an AppStream 2\.0 session, they must first share the device with their session\. For guidance that you can provide your users to help them perform this task, see [USB Devices](client-application-windows-user.md#client-application-share-usb-devices-with-session-user)\.

1. If the USB device works with the image builder as expected, create an image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

1. After you finish creating the image, update your AppStream 2\.0 fleet to use the new image\.

## Working with USB Device Filter Strings<a name="USB-device-filter-strings"></a>

This section describes the filter strings that are available for qualifying USB devices for AppStream 2\.0 streaming sessions\. It also provides guidance for working with these strings\. The following filter strings are available:
+ `Name` — By default, the value for this filter string is the name of the device, but you can specify your own value\.
+ `Base Class,SubClass,Protocol` — The USB class code for the device\. For more information, see [Defined Class Codes](https://www.usb.org/defined-class-codes)\.
+ `ID Vendor (VID)` — A unique identifier that is assigned by the USB organization to the manufacturer of the USB device\.
+ `ID Product (PID)` — A unique identifier that assigned by the manufacturer to the USB device\. 
+ `Support Autoshare` — Lets the AppStream 2\.0 client automatically share the device when a streaming session starts\. Set this value to `1` to allow automatic device sharing\. Set this value to `0` to not allow automatic device sharing\.
+ `Skip Reset` — By default, when a USB device is shared by AppStream 2\.0 with a streaming session, the device is reset to ensure that it functions correctly\. However, some USB devices don’t function correctly during the streaming session if they are reset\. To prevent this problem from occurring, set the value for this filter string to `1` to instruct the AppStream 2\.0 client not to reset the device while it is shared with a streaming session\. To ensure that the device is reset while it is shared with a streaming session, set this value to `0`\. When you set a value for `Skip Reset`, make sure that you set the value for `Support Autoshare` to `0` or `1`\.

 The filter string that is copied from the local computer is specific to a USB device\. In some cases, you might want to allow an entire class of devices instead of allowing every possible USB device\. For example, you might want to allow your users to use any kind of Wacom design tablets or use any USB mass storage device\. In such scenarios, you can provide wildcard characters for specific filter string fields\. If you don’t know the VID and PID for your USB devices, you can search for this information in the [USB ID database](https://www.the-sz.com/products/usbid/index.php)\. 

The following examples show how to configure filter strings for USB device sharing during streaming sessions:
+ Allow all mass storage devices automatically on starting a streaming session — "Mass storage, 8, \*, \*, \*, \*,1,0"
+ Allow all Wacom devices automatically on starting a streaming session — "Wacom tablets, 3, \*, \*, 1386, \*,1,0"
+ Allow all devices that provide an audio interface — "Audio, 1, \*, \*, \*, \*,1,0"
+ Allow device X, but don't reset it while the device is shared\. Don’t share the device automatically on starting a streaming session — "X, Y, \*, \*, 1386, \*,0,1" 