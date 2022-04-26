# Connect to an Image Builder<a name="managing-image-builders-connect"></a>

You can connect to an image builder by doing either of the following: 
+ Using the AppStream 2\.0 console \(for web connections only\)
+ Creating a streaming URL \(for web or AppStream 2\.0 client connections\)

**Note**  
If the image builder that you want to connect to is joined to an Active Directory domain and your organization requires smart card sign in, you must [create a streaming URL](#managing-image-builders-connect-streaming-URL) and use the AppStream 2\.0 client for the connection\.

**Topics**
+ [AppStream 2\.0 Console \(Web Connection\)](#managing-image-builders-connect-console)
+ [Streaming URL \(AppStream 2\.0 Client or Web Connection\)](#managing-image-builders-connect-streaming-URL)

## AppStream 2\.0 Console \(Web Connection\)<a name="managing-image-builders-connect-console"></a>

To use the AppStream 2\.0 console to connect to an image builder through a web browser, complete the following steps\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. In the list of image builders, choose the image builder to which you want to connect\. Verify that the status of the image builder is **Running**, and choose **Connect**\.

   For this step to work, you might need to configure your browser to allow pop\-ups from https://stream\.<aws\-region>\.amazonappstream\.com/\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is Windows\-based and not joined to an Active Directory domain, on the **Local User** tab, choose one of the following:
     + **Administrator** — Choose **Administrator** to install your applications on the image builder and create an image, or to perform any other tasks that require local administrator permissions\.
     + **Template User** — Choose **Template User** to create default application and Windows settings\.
     + **Test User** — Choose **Test User** to open your applications and verify their settings\.
   + If your image builder is Windows\-based and joined to an Active Directory domain and you require access to resources that are managed by Active Directory to install your applications, choose the **Directory User** tab, and enter the credentials for a domain user account that has local administrator permissions on the image builder\.
**Note**  
Smart card sign in isn't supported for connections through a web browser\. Instead, you must create a streaming URL and use the AppStream 2\.0 client\. For information about smart card sign in, see [Smart Cards](client-system-requirements-feature-support.md#feature-support-USB-devices-qualified-smart-cards)\.
   + If your image builder is Linux\-based, you are automatically logged in as

     the **ImageBuilderAdmin** user in the Amazon Linux GNOME desktop and have root admin privileges\.

## Streaming URL \(AppStream 2\.0 Client or Web Connection\)<a name="managing-image-builders-connect-streaming-URL"></a>

You can create a streaming URL to connect to an image builder through a web browser or the AppStream 2\.0 client\. Unlike a streaming URL that you create to enable user access to a fleet instance, which is valid for a maximum of seven days, by default, a streaming URL that you create to access an image builder expires after one hour\. To set a different expiration time, you must generate the streaming URL by using the [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action\.

If the image builder that you want to connect to is joined to an Active Directory domain and your organization requires smart card sign in, you must create a streaming URL and use the AppStream 2\.0 client for the connection\.

**Note**  
Native application mode is not supported for AppStream 2\.0 client connections to image builders\. If you use the AppStream 2\.0 client to connect to an image builder and the **Start in native application mode** check box is selected, an AppStream 2\.0 error notification displays, stating that your session was switched to classic mode\.

You can create a streaming URL in any of the following ways:
+ AppStream 2\.0 console
+ The [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action 
+ The [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) AWS CLI command

To create a streaming URL and connect to the image builder by using the AppStream 2\.0 console, complete the steps in the following procedure\.

**To create a streaming URL and connect to the image builder by using the AppStream 2\.0 console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Builder**\.

1. In the list of image builders, choose the image builder to which you want to connect\. Verify that the status of the image builder is **Running**\.

1. Choose **Actions**, **Create streaming URL**\.

1. Do one of the following:
   + To save the streaming URL to connect to the image builder later, choose **Copy Link** to copy the URL, then save it to an accessible location\.
   + To connect to the image builder through the AppStream 2\.0 client, choose **Launch in Client**\. When you choose this option, the AppStream 2\.0 client sign\-in page is prepopulated with the streaming URL\.
   + To connect to the image builder through a web browser, choose **Launch in Browser**\. When you choose this option, a web browser opens with the address bar prepopulated with the streaming URL\.

1. After you create the streaming URL and connect to the image builder, log in to the image builder by doing either of the following:
   + If your image builder is Windows\-based and not joined to an Active Directory domain, on the **Local User** tab, choose one of the following:
     + **Administrator** — Choose **Administrator** to install your applications on the image builder and create an image, or to perform any other tasks that require local administrator permissions\.
     + **Template User** — Choose **Template User** to create default application and Windows settings\.
     + **Test User** — Choose **Test User** to open your applications and verify their settings\.
   + If your image builder is Windows\-based and joined to an Active Directory domain and you require access to resources that are managed by Active Directory to install your applications, choose the **Directory User** tab, and enter the credentials for a domain user account that has local administrator permissions on the image builder\.
**Note**  
If you're using the AppStream 2\.0 client, you can enter either your Active Directory domain password and choose **Password sign in**, or select **Choose a smart card** and provide your smart card PIN when prompted\.  
If you're using a web browser, you must enter your Active Directory domain password\. Smart card sign in is supported only for AppStream 2\.0 client connections to streaming instances\.
   + If your image builder is Linux\-based, you are automatically logged in as

     the **ImageBuilderAdmin** user in the Amazon Linux GNOME desktop and have root admin privileges\.