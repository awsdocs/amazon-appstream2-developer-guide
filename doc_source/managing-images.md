# Images<a name="managing-images"></a>

You can create Amazon AppStream 2\.0 images that contain applications you can stream to your users and default Windows and application settings to enable your users to get started with those applications quickly\. However, after you create an image, you can't change it\. To add other applications, update existing applications, or change image settings, you must start and reconnect to the image builder that you used to create the image\. If you deleted that image builder, launch a new image builder that is based on your image\. Then make your changes and create a new image\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md) and [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

Images that are available to you are listed in the **Image Registry** in the AppStream 2\.0 console\. They are categorized as public, private, or shared\. You can use any of these image types to launch an image builder and set up an AppStream 2\.0 fleet\. Shared images are owned by other AWS accounts and shared with you\. Permissions set on images that are shared with you may limit what you can do with those images\. For more information, see [Administer Your Amazon AppStream 2\.0 Images](administer-images.md)\.

**Topics**
+ [Default Application and Windows Settings and Application Launch Performance](customizing-appstream-images.md)
+ [Manage AppStream 2\.0 Agent Versions](base-images-agent.md)
+ [AppStream 2\.0 Agent Version History](agent-software-versions.md)
+ [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)
+ [Administer Your Amazon AppStream 2\.0 Images](administer-images.md)
+ [Create Your AppStream 2\.0 Image Programmatically by Using the Image Assistant CLI Operations](programmatically-create-image.md)
+ [Use Session Scripts to Manage Your AppStream 2\.0 Users' Streaming Experience](use-session-scripts.md)