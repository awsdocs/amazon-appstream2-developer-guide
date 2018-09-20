# Launch an Image Builder to Install and Configure Streaming Applications<a name="tutorial-image-builder-create"></a>

 To install and configure applications to stream to your users, you start by launching an image builder instance as described in the following procedure\.

**Important**  
After you launch an image builder and it is running, your account may incur nominal charges\. For more information, see [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

**To launch an image builder**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. You can launch the image builder in the following ways: 
   + If a welcome screen appears displaying two options \(**Try it now** and **Get started**\), choose **Get started**, **Custom set up**\. 

     For information about these two options, see [Amazon AppStream 2\.0 FAQs](https://aws.amazon.com/appstream2/faqs/)\.
   + If a welcome screen does not appear, choose **Quick links** in the left navigation pane, then **Custom set up**\. 
   + Alternatively, choose **Images** in the left navigation pane, then the **Image Builder** tab, **Launch Image Builder**\.

1. For **Step 1: Choose Image**, choose a base image\. If you are launching the image builder for the first time, you can use one of the latest base images released by AWS \(selected by default\)\. For a list of the latest versions of base images released by AWS, see [AppStream 2\.0 Base Image Version History](base-image-version-history.md)\. If you have already created images, or you want to update applications in an existing image, you can select one of your existing images\. Be sure to select an image that aligns with the instance family that you need\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.

   Choose **Next**\.

1. For **Step 2: Configure Image Builder**, configure the image builder by accepting the default values or providing inputs for the following fields:   
**Name**  
Type a unique name identifier for the image builder\.  
**Instance Type**  
Select the instance type for the image builder\. Choose a type that matches the performance requirements of the applications that you plan to install\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.  
**AppStream 2\.0 Agent **  
This section displays only if you are not using the latest base image from AWS or a custom image that uses the latest version of the agent\.  
The AppStream 2\.0 agent software runs on your streaming instances, enabling your users to connect to and stream their applications\. Starting December 7, 2017, your streaming instances can be automatically updated with the latest AppStream 2\.0 agent software\. This capability helps to ensure that your image builder includes the latest features, performance improvements, and security updates that are available from AWS\.   
You can enable automatic updates of the AppStream 2\.0 agent by creating a new image from any base image published by AWS on or after December 7, 2017\. If the image that you are launching your image builder from doesn't use the latest version of the AppStream 2\.0 agent, we recommend that you select the option to launch your image builder with the latest agent\. 

   Choose **Next**\.

1. Do the following:
   + For **Step 3: Configure Network**, choose a virtual private cloud \(VPC\) subnet in which to launch your image builder\. Your image builder has access to any of the network resources that are accessible from within this VPC subnet\. 
   + For internet access on the image builder, choose **Default Internet Access**, select a VPC that has public subnets on your default VPC, and then select one of the public subnets listed for **Subnet**\. If you are controlling internet access using a NAT gateway, leave **Default Internet Access** unselected and use the VPC with the NAT gateway\. For more information, see [Networking, Access, and Security for Amazon AppStream 2\.0](managing-network.md)\. 
   + For **Security group\(s\)**, select up to five security groups to associate with this image builder\. If needed, choose **Create new security group**\. If you do not choose a security group, the image builder is associated with the default security group for your VPC\. For more information, see [Security Groups](managing-network.md#managing-network-security-groups)\.
   + For **Active Directory Domain \(Optional\)**, expand this section to choose which Active Directory and organizational unit in which to place your streaming instance computer objects\. Ensure that the selected network access settings enable DNS resolvability and communication with your directory\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

1. Choose **Review** and confirm the details for the image builder\. To change the configuration for any section, choose **Edit** and make the needed changes\.

1. After you finish reviewing the configuration details, choose **Launch**\. If an error message notifies you that you don’t have sufficient limits to create the image builder, submit a limit increase request through the AWS Support Center\. For more information, see [Amazon AppStream 2\.0 Service Limits](limits.md)\.

1. During the image builder creation process, the status of the image builder displays as **Pending **while AppStream 2\.0 prepares the necessary resources\. Click the **Refresh** icon periodically to update the image builder status\. After the status changes to** Running**, the image builder is ready to use and you can create a custom image\.

   Optionally, you can apply one or more tags to help manage the image builder\. Choose **Tags**, choose **Add/Edit Tags**, choose **Add Tag**, specify the key and value for the tag, and then choose **Save**\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

**Next Steps**

Next, install and configure your applications for streaming, and then create an image by creating a snapshot of the image builder instance\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image](tutorial-image-builder.md)\.