# Tutorial: Create a Custom Image<a name="tutorial-image-builder"></a>

Before you can stream your applications, Amazon AppStream 2\.0 requires at least one image that you create by using an image builder\. This tutorial describes how to create custom images by using an image builder\.

**Important**  
After you create an image builder and it is running, your account may incur nominal charges\. For more information, see [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

**Important**  
This tutorial contains details that apply to the latest base image release\. For more information, see [Amazon AppStream 2\.0 Windows Image Version History](base-image-version-history.md)\.  
If you are using images that are created from base images dated before 2017\-07\-24, you can view a compatible version of this tutorial by downloading the PDF file [appstream2\-dg\-2017\-07\-23\.pdf](http://awsdocs.s3.amazonaws.com/AppStream2/appstream2-dg-2017-07-23.pdf)\. 

**Topics**
+ [Step 1: Create an Image Builder](#tutorial-image-builder-create)
+ [Step 2: Install Applications to an Image](#tutorial-image-builder-install)
+ [Step 3: Add Applications to an Image](#tutorial-image-builder-add)
+ [Step 4: Optimize Applications](#tutorial-image-builder-optimize)
+ [Step 5: Create an Image](#tutorial-image-builder-create-image)
+ [Step 6 \(Optional\): Tag and Copy an Image](#tutorial-image-builder-tag-copy)
+ [Step 7: Clean Up](#tutorial-image-builder-finish)

## Step 1: Create an Image Builder<a name="tutorial-image-builder-create"></a>

In this step, you create a new image builder so that you can add applications and create images for streaming\.

**To create an image builder for adding applications**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. You can launch the image builder in the following ways: 
   + If a welcome screen appears displaying two options \(**Try it now** and **Get started**\), choose **Get started**, **Custom set up**\. 

     For information about these two options, see [Amazon AppStream 2\.0 FAQs](https://aws.amazon.com/appstream2/faqs/)\.
   + If a welcome screen does not appear, choose **Quick links** in the left navigation pane, then **Custom set up**\. 
   + Alternatively, choose **Images** in the left navigation pane, then the **Image Builder** tab, **Launch Image Builder**\.

1. For **Step 1: Choose Image**, select a base image\. If you are launching the image builder for the first time, you can use one of the latest base images released by AWS \(selected by default\)\. For a list of the latest versions of base images released by AWS, see [Amazon AppStream 2\.0 Windows Image Version History](base-image-version-history.md)\. If you have already created images, or you want to update applications in an existing image, you can select one of your existing images\. Be sure to select an image that aligns with the instance family that you need\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.

   Choose **Next**\.

1. For **Step 2: Configure Image Builder**, configure the image builder by accepting the default values or providing inputs for the following fields:   
**Name**  
Type a unique name identifier for the image builder\.  
**Instance Type**  
Select the instance type for the image builder\. Choose a type that matches the performance requirements of the applications that you plan to install\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.  
The AppStream 2\.0 agent software runs on your streaming instances, enabling your users to connect to and stream their applications\. Starting December 7, 2017, your streaming instances can be automatically updated with the latest AppStream 2\.0 agent software\. This capability helps to ensure that your image builder includes the latest features, performance improvements, and security updates that are available from AWS\.   
You can enable automatic updates of the AppStream 2\.0 agent by creating a new image from any base image published by AWS on or after December 7, 2017\. If the image from which you are launching your image builder is not using the latest version of the AppStream 2\.0 agent, we recommend that you select the option to launch your image builder with the latest agent\. This option is not displayed if you are already using the latest base image from AWS or if you are using a custom image that uses the latest version of the agent\. 

   Choose **Next**\.

1. For **Step 3: Configure Network**, choose a virtual private cloud \(VPC\) subnet in which to launch your image builder\. Your image builder has access to any of the network resources that are accessible from within this VPC subnet\. 

   For internet access on the image builder, choose **Default Internet Access**, select a VPC that has public subnets on your default VPC, and then select one of the public subnets listed for **Subnet**\. If you are controlling internet access using a NAT gateway, leave **Default Internet Access** unselected and use the VPC with the NAT gateway\. For more information, see [Network Settings for Amazon AppStream 2\.0 ](managing-network.md)\. 

   For **Security group\(s\)**, select up to five security groups to associate with this image builder\. If needed, choose **Create new security group**\. If you do not choose a security group, the image builder is associated with the default security group for your VPC\. For more information, see [Security Groups](managing-network.md#managing-network-security-groups)\.

   For **Active Directory Domain \(Optional\)**, expand this section to choose which Active Directory and organizational unit in which to place your streaming instance computer objects\. Ensure that the selected network access settings enable DNS resolvability and communication with your directory\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

1. Choose **Review** and confirm the details for the image builder\. To change the configuration for any section, choose **Edit** and make the needed changes\. After you finish reviewing the configuration details, choose **Launch**\. 

After the service prepares the needed resources, the image builder instance list appears\. The status of your new image builder appears as **Running** when the image builder is ready to use\.

Optionally, you can apply one or more tags to help manage the image builder\. Choose **Tags**, choose **Add/Edit Tags**, choose **Add Tag**, specify the key and value for the tag, and then choose **Save**\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

## Step 2: Install Applications to an Image<a name="tutorial-image-builder-install"></a>

In this step, you connect to the image builder that you created and launched, then install the applications to be included in the image\.

**To install applications**

1. On the left navigation pane, choose **Images**, **Image Builder**\.

1. Select the image builder to use, check to be sure it has a Running status, and choose **Connect**\. For this step to work, you may need to configure your browser to allow pop\-ups from https://stream\.<aws\-region>\.amazonappstream\.com/\.

1. Sign in by choosing one of the following options:  
**Administrator **  
This mode has full administrator permissions on the image builder instance\. Use this mode to install your applications, add applications to the image, and create an image\.  
**Test User **  
This mode has the same limited permissions as your end users have on their streaming instances\. Use this mode to test applications for proper function as an end user\.  
**Directory User **  
If your image builder is joined to an Active Directory domain, this mode allows you to log in as a user in your domain to access resources that are managed by Active Directory\. Provide the user name and password of the user to log in as\. The user must have local administrator permissions to install applications\. For more information, see [Granting Local Administrator Rights on Image Builders](active-directory-admin.md#active-directory-image-builder-local-admin)\.

    At any point after logging in, you can switch between users by selecting **Switch Users** from the **Admin Commands** menu\. This disconnects your current session and brings up the login menu\.

1. Install applications by browsing to an application website or other download source\. Complete the application's own installation process before moving to the next step\. If an application requires the Windows operating system to be restarted, let the operating system restart\. Before the operating system restarts, you are disconnected from your image builder\. Wait a few minutes, connect to the image builder again, open Image Assistant, and then finish installing the application\.

## Step 3: Add Applications to an Image<a name="tutorial-image-builder-add"></a>

In this step, you can add applications \(*\.exe*\), batch scripts \(*\.bat*\), and application shortcuts \(*\.lnk*\) to the image\.

**To add your applications**

1. From the image builder desktop, start the **Image Assistant** application\.

1. Choose **Add Application** and navigate to the location of the application, script, or shortcut to add\. Choose **Open**\. 

1. In the **Application Properties** dialog box, enter a display name to be shown to the users in the catalog, change the icon, and enter launch parameters \(additional arguments passed to the application when it is launched\)\. Repeat this step for each application that you add to the image\. 

1. When you finish adding applications, choose **Next**\.

**To test your applications**
+ Verify that the applications you've added start correctly\. To do this, start a new Windows session as a user who has similar access rights as your end users\. 

  1. From the **Admin Commands** menu, choose **Switch user**\. This disconnects you from the current session and shows the login menu\. 

  1. To log in as a local test user, choose **Test User**\. To log in as an Active Directory user, choose **Directory User**, and provide the user name and password of the user to log in as\. Choose **Log in**\.

  1. Launch **Image Assistant** from the shortcut on the desktop\. Choose **Launch** next to the application to launch, and test your application\. 

  1. Repeat the previous step for each application in the image\.

  1. To return to the admin mode, choose **Switch user**, and select the user used to add applications to the image\.

**Note**  
Do not exit the **Image Assistant** application, as you need to use it in the next section\.

## Step 4: Optimize Applications<a name="tutorial-image-builder-optimize"></a>

In this step, you optimize your applications and create the image\. The image builder optimizes your applications for startup performance\. This is a required step that is performed on all applications in the list\. All applications must be launched before optimization\.

**To optimize your applications**

1. Choose **Launch** and the service automatically launches the first application in your list\. When the application is running, choose **Continue**\.

1. Provide any interactions or inputs that are required by the application to bring it to a usable state\. For example, a web browser may prompt you to import settings before it is completely up and running\. 

1. After you bring the application to a usable state, choose **Continue**\. The application helper launches the next application automatically\.

1. Repeat the previous steps until all applications are launched, and leave them running\. After you launch all applications, in the **Image Assistant** application, choose **Next**\. 

## Step 5: Create an Image<a name="tutorial-image-builder-create-image"></a>

In this step, you choose an image name and create the image\. 

**To create the image**

1. Enter a unique image name and image display name \(a description is optional\), and choose **Next**\. The name you choose cannot begin with "Amazon", "AWS", or "AppStream"\.

1. Review the image details\. 
**Note**  
If you choose a base image that is published by AWS on or after December 7, 2017, the option **Always use the latest agent version** appears, and it is selected by default\. We recommend that you leave this option selected so that streaming instances that are launched from the image always use the latest version of the agent\. If you deselect this option, you cannot re\-select it after you finish creating the image\. For information about the latest release of the AppStream 2\.0 agent, see [Amazon AppStream 2\.0 Agent Version History](agent-software-versions.md)\.

   Choose **Disconnect and Create Image**\. After your new image is created and the session is disconnected, you can close the session window\. Your image builder transitions into a **Snapshotting** state while the image is being created\. After the image is created, your image builder transitions into the **Stopped** state\. You might need to refresh the console listing to see the state change\.

1. Return to the console and navigate to **Images**, **Image Registry**\. Verify that your new image appears in the list\.

   The new image first appears with a status of **Pending** in the image registry of your console\. After the image is successfully created, the status of the image changes to **Available**, which means that you can use the image to launch a stack and stream your applications\. 

    To continue creating images, you can start the image builder and connect to it from the console, or create a new image builder\. There is a limit of five image builders per account\.

## Step 6 \(Optional\): Tag and Copy an Image<a name="tutorial-image-builder-tag-copy"></a>

After you create an image, you can apply one or more tags to help manage the image\. You can also copy the image within the same region or to a new region within the same AWS account\. Copying a source image results in an identical but distinct destination image\. AWS does not copy any user\-defined tags, however\. Also, you can only copy custom images that you create, not the base images that are provided by AWS\. 

**Note**  
You can copy up to two images at the same time to a destination\. If the destination to which you are copying an image is at the image limit, you receive an error\. To copy the image in this case, you must first remove images from the destination\. After the destination is below the image limit, initiate the image copy from the source region\. For more information, see [Amazon AppStream 2\.0 Service Limits](limits.md)\.

**To add tags to an image**

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

## Step 7: Clean Up<a name="tutorial-image-builder-finish"></a>

Finally, stop your running image builders to free up resources and avoid unintended charges to your account\. We recommend stopping any unused, running image builders\. For more information, see [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

**To stop a running image builder**

1. In the navigation pane, choose **Images**, **Image Builders**, and select the running image builder instance\.

1. Choose **Actions**, **Stop**\.