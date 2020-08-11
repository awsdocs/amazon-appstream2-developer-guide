# Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console<a name="tutorial-image-builder"></a>

This tutorial describes how to create a custom Amazon AppStream 2\.0 image that contains applications you can stream to your users, and default application and Windows settings to enable your users to get started with their applications quickly\. To complete this tutorial, you must already have an image builder\. If you don't have an image builder, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

**Important**  
This tutorial includes information that applies to the latest base image release\. For more information, see [AppStream 2\.0 Base Image Version History](base-image-version-history.md)\.

**Topics**
+ [Step 1: Install Applications on the Image Builder](#tutorial-image-builder-install)
+ [Step 2: Create an AppStream 2\.0 Application Catalog](#tutorial-image-builder-add)
+ [Step 3: Create Default Application and Windows Settings](#tutorial-image-builder-create-default-app-settings)
+ [Step 4: Test Applications](#tutorial-image-builder-test-applications)
+ [Step 5: Optimize Applications](#tutorial-image-builder-optimize)
+ [Step 6: Finish Creating Your Image](#tutorial-image-builder-finish-create-image)
+ [Step 7 \(Optional\): Tag and Copy an Image](#tutorial-image-builder-tag-copy)
+ [Step 8: Clean Up](#tutorial-image-builder-finish)

## Step 1: Install Applications on the Image Builder<a name="tutorial-image-builder-install"></a>

In this step, you connect an image builder and install your applications on the image builder\.

**Important**  
To complete this step, you must log into the image builder with the local **Administrator** account or a domain user account that has local administrator permissions\. Do not rename or delete the local built\-in **Administrator** account\. If you rename or delete this account, the image creation will fail\. 

**To install applications on the image builder**

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder to use, verify that it is in the **Running** state, and choose **Connect**\. For this step to work, you may need to configure your browser to allow pop\-ups from https://stream\.<aws\-region>\.amazonappstream\.com/\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain and you require access to resources that are managed by Active Directory to install your applications, choose the **Directory User** tab, type the credentials for a domain user account that has local administrator permissions on the image builder, then choose **Log in**\. 

1. Install applications from an application website or other download source\. Install the applications you want before proceeding to the next step\. 
**Note**  
Download and install applications only from sites that you trust\.

   If an application requires the Windows operating system to restart, let it do so\. Before the operating system restarts, you are disconnected from your image builder\. After the restart is complete, connect to the image builder again, then finish installing the application\.

## Step 2: Create an AppStream 2\.0 Application Catalog<a name="tutorial-image-builder-add"></a>

In this step, create an AppStream 2\.0 application catalog by specifying applications \(*\.exe*\), batch scripts \(*\.bat*\), and application shortcuts \(*\.lnk*\) for your image\. For each application that you plan to stream, you can specify the name, display name, executable file to launch, and icon to display\. If you choose an application shortcut, these values are prepopulated for you\.

**Important**  
To complete this step, you must be logged into the image builder with the local **Administrator** account or a domain user account that has local administrator permissions\. 

**To create an AppStream 2\.0 application catalog**

1. From the image builder desktop, open Image Assistant\. Image Assistant guides you through the image creation process\.

1. In **1\. Add Apps**, choose **\+ Add App**, and navigate to the location of the application, script, or shortcut to add\. Choose **Open**\. 

1. In the **App Launch Settings** dialog box, keep or change the default settings for **Name**, **Display Name**, and **Icon Path**\. Optionally, you can specify launch parameters \(additional arguments passed to the application when it is launched\) and a working directory for the application\. When you're done, choose **Save**\. 

   The **Display Name** and **Icon Path** settings determine how your application name and icon appear in the application catalog\. The catalog displays to users when they sign in to an AppStream 2\.0 streaming session\.

1. Repeat steps 2 and 3 for each application in Image Assistant and confirm that the applications appear on the **Add Apps** tab\. When you're done, choose **Next** to continue using Image Assistant to create your image\.

## Step 3: Create Default Application and Windows Settings<a name="tutorial-image-builder-create-default-app-settings"></a>

In this step, you create default application and Windows settings for your AppStream 2\.0 users\. Doing this enables your users to get started with applications quickly during their AppStream 2\.0 streaming sessions, without the need to create or configure these settings themselves\.

**Important**  
To complete this step, you must be logged into the image builder with the local **Template User** account or a domain user account that does not have local administrator permissions\. 

**To create default application and Windows settings for your users**

1. In Image Assistant, in **2\. Configure Apps**, choose **Switch user**\. This disconnects you from the current session and displays the login menu\.

1. Do either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Template User**\. This account enables you to create your default application and Windows settings\.
   + If your image builder is joined to an Active Directory domain, choose **Directory User**, and log in as a domain user that does not have local administrator permissions\.

1. From the image builder desktop, open Image Assistant, which displays the applications that you added when you created the application catalog\.

1. Choose the application for which you want to create default application settings\.

1. After the application opens, create these settings as needed\.

1. When you're done, close the application, and return to Image Assistant\.

1. If you specified more than one application in Image Assistant, repeat steps 4 through 6 for each application as needed\. 

1. If you want default Windows settings, create them now\. When you're done, return to Image Assistant\.

1. Choose **Switch user** and log in with the same account that you used to create the application catalog \(an account that has local administrator permissions\)\.

1. In Image Assistant, in **2\. Configure Apps**, do either of the following:
   + If your image builder is not joined to an Active Directory domain, choose **Save settings**\.
   + If your image builder is joined to an Active Directory domain, in the **Choose which user settings to copy **list, choose the same account that you used to log into the image builder when you created the default application and Windows settings, then choose **Save settings**\.

     The **Choose which settings to copy** list displays any user account that currently has settings saved on the image builder\.

1. When you're done, choose **Next** to continue creating your image\.

## Step 4: Test Applications<a name="tutorial-image-builder-test-applications"></a>

In this step, verify that the applications you've added open correctly and perform as expected\. To do so, start a new Windows session as a user who has the same permissions as your users\. 

**Important**  
To complete this step, you must log in to the image builder with the **Test User** account or a domain user account that does not have local administrator permissions\. 

**To test your applications**

1. In Image Assistant, in **3\. Test**, do either of the following:
   + If your image builder is not joined to an Active Directory domain, choose **Switch user**\.
   + If your image builder is joined to an Active Directory domain, you require a domain user account to test your applications, and the user already has settings on the image builder, you must reset the application settings for that user\. To do so, select the user from the **User to reset** list, and choose **Reset**\. When you're done, choose **Switch user**\. 
**Note**  
If your image builder is new and no users have settings on the image builder, the list does not display any users\.

1. Choose the user account to use for testing by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, choose **Test User**\. This account enables you to test your applications by using the same policies and permissions as your users\.
   + If your image builder is joined to an Active Directory domain, choose **Directory User**, specify the credentials for a domain user account that does not have local administrator permissions, then choose **Log in**\. 

1. From the image builder desktop, open Image Assistant, which displays the applications that you specified when you created the application catalog\.

1. Choose the application that you want to test, to confirm that it opens correctly and that any default application settings you created are applied\.

1. After the application opens, test it as needed\. When you're done, close the application and return to Image Assistant\. 

1. If you specified more than one application in Image Assistant, repeat steps 4 and 5 to test each application as needed\. 

1. When you're done, choose **Switch user**, then do either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain and you logged in as a domain user with local administrator permissions to specify applications in Image Assistant, log in as that user\.

1. Choose **Next** to continue creating your image\.

## Step 5: Optimize Applications<a name="tutorial-image-builder-optimize"></a>

In this step, Image Assistant opens your applications one after another, identifies their launch dependencies, and performs optimizations to ensure that applications launch quickly\. These are required steps that are performed on all applications in the list\.

**To optimize your applications**

1. In Image Assistant, in **4\. Optimize**, choose **Launch**\. 

1. AppStream 2\.0 automatically launches the first application in your list\. When the application completely starts, provide any required input to perform the first run experience for the application\. For example, a web browser may prompt you to import settings before it is completely up and running\. 

1. After you complete the first run experience and verify that the application performs as expected, choose **Continue**\. If you added more than one application to your image, each application opens automatically\. Repeat this step for each application as needed, leaving all applications running\.

1. When you're done, the next tab in Image Assistant, **5\. Configure Image**, automatically displays\. 

## Step 6: Finish Creating Your Image<a name="tutorial-image-builder-finish-create-image"></a>

In this step, choose an image name and finish creating your image\. 

**To create the image**

1. Type a unique image name, and an optional image display name and description\. The image name cannot begin with "Amazon," "AWS," or "AppStream\." 

   You can also add one or more tags to the image\. To do so, choose **Add Tag**, and type the key and value for the tag\. To add more tags, repeat this step\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\. When you're done, choose **Next**\.
**Note**  
If you choose a base image that is published by AWS on or after December 7, 2017, the option **Always use the latest agent version** appears, selected by default\. We recommend that you leave this option selected so that streaming instances that are launched from the image always use the latest version of the agent\. If you disable this option, you cannot enable it after you finish creating the image\. For information about the latest release of the AppStream 2\.0 agent, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.

1. In **6\. Review**, verify the image details\. To make changes, choose **Previous** to navigate to the appropriate Image Assistant tab, make your changes, and then proceed through the steps in Image Assistant as needed\.

1. After you finish reviewing the image details, choose **Disconnect and Create Image**\. 

1. The remote session disconnects within a few moments\. When the **Lost Connectivity** message appears, close the browser tab\. While the image is created, the image builder status appears as **Snapshotting**\. You cannot connect to the image builder until this process finishes\. 

1. Return to the console and navigate to **Images**, **Image Registry**\. Verify that your new image appears in the list\.

   While your image is being created, the image status in the image registry of the console appears as **Pending** and you cannot connect to it\. 

1. Choose the **Refresh** icon periodically to update the status\. After your image is created, the image status changes to **Available** and the image builder is automatically stopped\.

    To continue creating images, start the image builder and connect to it from the console, or create a new image builder\.

**Note**  
After you create an image, you can't change it\. To add other applications, update existing applications, or change image settings, you must start and reconnect to the image builder that you used to create the image, or, if you deleted that image builder, launch a new image builder builder that is based on your image\. Then, make your changes and create a new image\. 

## Step 7 \(Optional\): Tag and Copy an Image<a name="tutorial-image-builder-tag-copy"></a>

You can add one or more tags to an image during image creation or after you create an image\. You can also copy the image within the same Region or to a new Region within the same AWS account\. Copying a source image results in an identical but distinct destination image\. AWS does not copy any user\-defined tags, however\. Also, you can only copy custom images that you create, not the base images that are provided by AWS\. 

**Note**  
You can copy up to two images at the same time to a destination\. If the destination to which you are copying an image is at the image limit, you receive an error\. To copy the image in this case, you must first remove images from the destination\. After the destination is below the image quota \(also referred to as limit\), initiate the image copy from the source Region\. For more information, see [Amazon AppStream 2\.0 Service Quotas](limits.md)\.

**To add tags to an existing image**

1. In the navigation pane, choose **Images**, **Image Registry**\. 

1. In the image list, select the image to which you want to add tags\.

1. Choose **Tags**, choose **Add/Edit Tags**, choose **Add Tag**, specify the key and value for the tag, and then choose **Save**\.

For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

**To copy an image**

Copying an image across geographically diverse regions enables you to stream applications from multiple regions based on the same image\. By streaming your applications in closer proximity to your users, you can improve your users' experience streaming applications with AppStream 2\.0\.

1. In the navigation pane, choose **Images**, **Image Registry**\. 

1. In the image list, select the image that you want to copy\.

1. Choose **Actions**, **Copy**\.

1. In the **Copy Image** dialog box, specify the following information, and then choose **Copy Image:**
   + For **Destination region**, choose the region to which to copy the new image\. 
   + For **Name**, specify a name that the image will have when it is copied to the destination\. 
   + For **Description** \(optional\), specify a description that the image will have when it is copied to the destination\. 

1. To check on the progress of the copy operation, return to the console and navigate to **Images**, **Image Registry**\. Use the navigation bar to switch to the destination region \(if applicable\), and confirm that your new image appears in the list of images\.

   The new image first appears with a status of **Copying** in the image registry of your console\. After the image is successfully created, the status of the image changes to **Available**, which means that you can use the image to launch a stack and stream your applications\. 

## Step 8: Clean Up<a name="tutorial-image-builder-finish"></a>

Finally, stop your running image builders to free up resources and avoid unintended charges to your account\. We recommend stopping any unused, running image builders\. For more information, see [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

**To stop a running image builder**

1. In the navigation pane, choose **Images**, **Image Builders**, and select the running image builder instance\.

1. Choose **Actions**, **Stop**\.