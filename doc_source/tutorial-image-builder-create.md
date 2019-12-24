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

1. For **Step 2: Configure Image Builder**, configure the image builder by doing the following: 
   + **Name**: Type a unique name identifier for the image builder\.
   + **Display name \(optional\)**: Type a name to display for the image builder \(maximum of 100 characters\)\.
   + **Tags \(optional\)**: Choose **Add Tag**, and type the key and value for the tag\. To add more tags, repeat this step\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.
   + **Instance Type**: Select the instance type for the image builder\. Choose a type that matches the performance requirements of the applications that you plan to install\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.
   + **Network Access Points \(Optional\)**: You can create a private link, which is an [interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) \(interface endpoint\), in your virtual private cloud \(VPC\)\. To start creating the interface endpoint, select **Create PrivateLink**\. Selecting this link opens the VPC console\. To finish creating the endpoint, follow steps 3 through 6 in *To create an interface endpoint*, in [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)\.

     After you create the interface endpoint, you can use it to keep streaming traffic within your VPC\.
   + **AppStream 2\.0 Agent**: This section displays only if you are not using the latest base image from AWS or a custom image that uses the latest version of the agent\.

     The AppStream 2\.0 agent software runs on your streaming instances, enabling your users to connect to and stream their applications\. Starting December 7, 2017, your streaming instances can be automatically updated with the latest AppStream 2\.0 agent software\. This capability helps to ensure that your image builder includes the latest features, performance improvements, and security updates that are available from AWS\. 

     You can enable automatic updates of the AppStream 2\.0 agent by creating a new image from any base image published by AWS on or after December 7, 2017\. If the image that you are launching your image builder from doesn't use the latest version of the AppStream 2\.0 agent, we recommend that you select the option to launch your image builder with the latest agent\. 
   + **IAM role \(Advanced\)**: When you apply an IAM role from your account to an AppStream 2\.0 image builder, you can make AWS API requests from the image builder instance without manually managing AWS credentials\. To apply an IAM role to the image builder, do either of the following:
     + To use an existing IAM role in your AWS account, choose the role that you want to use from the **IAM role** list\. The role must must be accessible from the image builder\. For more information, see [Configuring an Existing IAM Role to Use With AppStream 2\.0 Streaming Instances](using-iam-roles-to-grant-permissions-to-applications-scripts-streaming-instances.md#configuring-existing-iam-role-to-use-with-streaming-instances)\.
     + To create a new IAM role, choose **Create new IAM role** and follow the steps in [How to Create an IAM Role to Use With AppStream 2\.0 Streaming Instances](using-iam-roles-to-grant-permissions-to-applications-scripts-streaming-instances.md#how-to-create-iam-role-to-use-with-streaming-instances)\.

1. Choose **Next**\.

1. For **Step 3: Configure Network**, do the following:
   + To add internet access for the image builder in a VPC with a public subnet, choose **Default Internet Access**\. If you are providing internet access by using a NAT gateway, leave **Default Internet Access** unselected\. For more information, see [Internet Access](internet-access.md)\.
   + For **VPC** and **Subnet 1**, choose a VPC and at least one subnet\. For increased fault tolerance, we recommend that you choose two subnets in different Availability Zones\. For more information, see [Configure a VPC with Private Subnets and a NAT Gateway](managing-network-internet-NAT-gateway.md)\.

     If you don't have your own VPC and subnet, you can use the [default VPC](default-vpc-with-public-subnet.md) or create your own\. To create your own, choose the **Create a new VPC** and **Create new subnet** links to create them\. Choosing these links opens the Amazon VPC console\. After you create your VPC and subnets, return to the AppStream 2\.0 console and choose the refresh icon to the left of the **Create a new VPC** and **Create new subnet** links to display them in the list\. For more information, see [Configure a VPC for AppStream 2\.0](appstream-vpc.md)\.
   + For **Security group\(s\)**, choose up to five security groups to associate with this image builder\. If you don't have your own security group and you don't want to use the default security group, choose the **Create new security group** link to create one\. After you create your subnets in the Amazon VPC console, return to the AppStream 2\.0 console and choose the refresh icon to the left of the **Create new security group** link to display them in the list\. For more information, see [Security Groups in Amazon AppStream 2\.0](managing-network-security-groups.md)\.

1. For **Active Directory Domain \(Optional\)**, expand this section to choose the Active Directory configuration and organizational unit in which to place your streaming instance computer objects\. Ensure that the selected network access settings enable DNS resolvability and communication with your directory\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

1. Choose **Review** and confirm the details for the image builder\. To change the configuration for any section, choose **Edit** and make the needed changes\.

1. After you finish reviewing the configuration details, choose **Launch**\. If an error message notifies you that you don’t have sufficient quotas \(also referred to as limits\) to create the image builder, submit a quota increase request through the AWS Support Center\. For more information, see [Amazon AppStream 2\.0 Service Quotas](limits.md)\.

1. During the image builder creation process, the status of the image builder displays as **Pending **while AppStream 2\.0 prepares the necessary resources\. Click the **Refresh** icon periodically to update the image builder status\. After the status changes to** Running**, the image builder is ready to use and you can create a custom image\.

**Next Steps**

Next, install and configure your applications for streaming, and then create an image by creating a snapshot of the image builder instance\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.