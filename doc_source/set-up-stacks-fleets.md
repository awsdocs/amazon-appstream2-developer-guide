# Create an AppStream 2\.0 Fleet and Stack<a name="set-up-stacks-fleets"></a>

To stream your applications, Amazon AppStream 2\.0 requires an environment that includes a fleet that is associated with a stack, and at least one application image\. This tutorial describes the steps to set up a fleet and stack, and how to give users access to the stack\. If you haven't already done so, we recommend that you try the procedures in [Get Started with Amazon AppStream 2\.0: Set Up With Sample Applications](getting-started.md) first\.

If you want to create an image to use, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

If you plan to join a fleet to an Active Directory domain, configure your Active Directory domain before completing the following steps\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

**Topics**
+ [Create a Fleet](#set-up-stacks-fleets-create)
+ [Create a Stack](#set-up-stacks-fleets-install)
+ [Provide Access to Users](#set-up-stacks-fleets-add)
+ [Clean Up Resources](#set-up-stacks-fleets-finish)

## Create a Fleet<a name="set-up-stacks-fleets-create"></a>

Set up and create a fleet from which user applications are launched and streamed\.

**To set up and create a fleet**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose **Get Started** if you are new to the console, or **Fleets** from the left navigation pane\. Choose **Create Fleet**\.

1. For **Step 1: Provide Fleet Details**, type a unique name identifier for the fleet\. Optionally, you can also specify the following: 
   + **Display Name** — Type a name to display for the fleet \(maximum of 100 characters\)\.
   + **Description** — Type a description for the fleet \(maximum of 256 characters\)\.
   + **Tags** — Choose **Add Tag**, and type the key and value for the tag\. To add more tags, repeat this step\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

1. Choose **Next**\.

1. For **Step 2: Choose an Image**, choose an image that meets your needs and then choose **Next**\.

1. For **Step 3: Configure Fleet**, do the following:
   + For **Choose instance type**, choose the instance type that meets the performance requirements of your applications\. All streaming instances in your fleet launch with the instance type that you select\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.
   + For **Fleet type**, choose the fleet type that suits your use case\. The fleet type determines its immediate availability and how you pay for it\.
   + For **Maximum session duration in minutes** — Choose the maximum amount of time that a streaming session can remain active\. If users are still connected to a streaming instance five minutes before this limit is reached, they are prompted to save any open documents before being disconnected\. After this time elapses, the instance is terminated and replaced by a new instance\. The maximum session duration that you can set in the AppStream 2\.0 console is 5760 minutes \(96 hours\)\.
   + For **Disconnect timeout in minutes**, choose the amount of time that a streaming session remains active after users disconnect\. If users try to reconnect to the streaming session after a disconnection or network interruption within this time interval, they are connected to their previous session\. Otherwise, they are connected to a new session with a new streaming instance\. If you associate a stack with a fleet for which a redirect URL is specified, after users’ streaming sessions end, the users are redirected to that URL\.

     If a user ends the session by choosing **End Session** on the streaming session toolbar, the disconnect timeout does not apply\. Instead, the user is prompted to save any open documents, and then immediately disconnected from the streaming instance\. The instance the user was using is then terminated\. 
   + For **Idle disconnect timeout in minutes**, choose the amount of time that users can be idle \(inactive\) before they are disconnected from their streaming session and the **Disconnect timeout in minutes** time interval begins\. Users are notified before they are disconnected due to inactivity\. If they try to reconnect to the streaming session before the time interval specified in **Disconnect timeout in minutes** has elapsed, they are connected to their previous session\. Otherwise, they are connected to a new session with a new streaming instance\. Setting this value to 0 disables it\. When this value is disabled, users are not disconnected due to inactivity\.
**Note**  
Users are considered idle when they stop providing keyboard or mouse input during their streaming session\. File uploads and downloads, audio in, audio out, and pixels changing do not qualify as user activity\. If users continue to be idle after the time interval in **Idle disconnect timeout in minutes** elapses, they are disconnected\. 
   + For **Minimum capacity**, choose a minimum number of instances for your fleet based on the minimum number of expected concurrent users\.
   + For **Maximum capacity**, choose a maximum number of instances for your fleet based on the maximum number of expected concurrent users\.
   + For **Scaling details \(Advanced\)**, specify the scaling policies that AppStream 2\.0 uses to increase and decrease the capacity of your fleet\. Note that the size of your fleet is limited by the minimum and maximum capacity that you specified\. For more information, see [Fleet Auto Scaling for Amazon AppStream 2\.0](autoscaling.md)\.
   + For **IAM role \(Advanced\)**, when you apply an IAM role from your account to an AppStream 2\.0 fleet instance, you can make AWS API requests from the fleet instance without manually managing AWS credentials\. To apply an IAM role, do either of the following:
     + To use an existing IAM role in your AWS account, choose the role that you want to use from the **IAM role** list\. The role must must be accessible from the fleet instance\. For more information, see [Configuring an Existing IAM Role to Use With AppStream 2\.0 Streaming Instances](using-iam-roles-to-grant-permissions-to-applications-scripts-streaming-instances.md#configuring-existing-iam-role-to-use-with-streaming-instances)\.
     + To create a new IAM role, choose **Create new IAM role** and follow the steps in [How to Create an IAM Role to Use With AppStream 2\.0 Streaming Instances](using-iam-roles-to-grant-permissions-to-applications-scripts-streaming-instances.md#how-to-create-iam-role-to-use-with-streaming-instances)\.

1. Choose **Next**\.

1. For **Step 4: Configure Network**, do the following:
   + To add internet access for fleet instances in a VPC with a public subnet, choose **Default Internet Access**\. If you are providing internet access by using a NAT gateway, leave **Default Internet Access** unselected\. For more information, see [Internet Access](internet-access.md)\.
   + For **VPC** and **Subnet 1**, choose a VPC and at least one subnet that has access to the network resources that your application needs\. For increased fault tolerance, we recommend that you choose two subnets in different Availability Zones\. For more information, see [Configure a VPC with Private Subnets and a NAT Gateway](managing-network-internet-NAT-gateway.md)\.

     If you don't have your own VPC and subnet, you can use the [default VPC](default-vpc-with-public-subnet.md) or create your own\. To create your own, choose the **Create a new VPC** and **Create new subnet** links to create them\. Choosing these links opens the Amazon VPC console\. After you create your VPC and subnets, return to the AppStream 2\.0 console and choose the refresh icon to the left of the **Create a new VPC** and **Create new subnet** links to display them in the list\. For more information, see [Configure a VPC for AppStream 2\.0](appstream-vpc.md)\.
   + For **Security group\(s\)**, choose up to five security groups to associate with this fleet\. If you don't have your own security group and you don't want to use the default security group, choose the **Create new security group** link to create one\. After you create your subnets in the Amazon VPC console, return to the AppStream 2\.0 console and choose the refresh icon to the left of the **Create new security group** link to display them in the list\. For more information, see [Security Groups in Amazon AppStream 2\.0](managing-network-security-groups.md)\.
   + For **Active Directory Domain \(Optional\)**, choose the Active Directory and organizational unit \(OU\) for your streaming instance computer objects\. Ensure that the network access settings you selected enable DNS resolvability and communication with your directory\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

1. Choose **Next**\.

1. For **Step 5: Review**, confirm the details for the fleet\. To change the configuration for any section, choose **Edit **and make the needed changes\. After you finish reviewing the configuration details, choose **Create**\. 

1. In the pricing acknowledgement dialog box, select the acknowledgement check box, and choose **Create**\.

1. While your fleet is being created and fleet instances are provisioned, the status of your fleets displays as **Starting** in the **Fleets** list\. Choose the **Refresh** icon periodically to update the fleet status until the status is **Running**\. You cannot associate the fleet with a stack and use it for streaming sessions until the status of the fleet is **Running**\.

## Create a Stack<a name="set-up-stacks-fleets-install"></a>

Set up and create a stack to control access to your fleet\.

**To set up and create a stack**

1. In the left navigation pane, choose **Stacks**, and then choose **Create Stack**\.

1. For **Step 1: Stack Details**, Under **Stack details**, type a unique name identifier for the stack\. Optionally, you can do the following:
   + **Display name** — Enter a name to display for the stack \(maximum of 100 characters\)\.
   + **Description**— Enter a description for the stack \(maximum of 256 characters\)\.
   + **Redirect URL** — Specify a URL to which users are redirected after their streaming sessions end\.
   + **Feedback URL** — Specify a URL to which users are redirected after they click the **Send Feedback** link to submit feedback about their application streaming experience\. If you do not specify a URL, this link is not displayed\.
   + **Fleet** — Select an existing fleet or create a new one to associate with your stack\.
   + **Tags** — Choose **Add Tag**, and type the key and value for the tag\. To add more tags, repeat this step\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.
   + **VPC Endpoints \(Advanced\)** — You can create a private link, which is an [interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) \(interface endpoint\), in your virtual private cloud \(VPC\)\. To start creating the interface endpoint, select **Create VPC Endpoint**\. Selecting this link opens the VPC console\. To finish creating the endpoint, follow steps 3 through 6 in *To create an interface endpoint*, in [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)\. 

     After you create the interface endpoint, you can use it to keep streaming traffic within your VPC\.
   + **Embed AppStream 2\.0 \(Optional\)** — To embed an AppStream 2\.0 streaming session in a webpage, specify the domain to host the embedded streaming session\. Embedded streaming sessions are only supported over HTTPS \[TCP port 443\]\. 
**Note**  
You must meet prerequisites and perform additional steps to configure embedded AppStream 2\.0 streaming sessions\. For more information, see [Embed AppStream 2\.0 Streaming Sessions](embed-streaming-sessions.md)\.

1. Choose **Next\.**

1. For **Step 2: Enable Storage**, you can provide persistent storage for your users by choosing one or more of the following: 
   + **Home Folders** — Users can save their files to their home folder and access existing files in their home folder during application streaming sessions\. For information about requirements for enabling home folders, see [Enable Home Folders for Your AppStream 2\.0 Users](home-folders.md#enable-home-folders)\.
   + **Google Drive for G Suite** — Users can link their Google Drive for G Suite account to AppStream 2\.0\. During application streaming sessions, they can sign in to their Google Drive account, save files to Google Drive, and access their existing files in Google Drive\. You can enable Google Drive for accounts in G Suite domains only, not for personal Gmail accounts\. 
**Note**  
After you select **Enable Google Drive**, type the name of at least one organizational domain that is associated with your G Suite account\. Access to Google Drive during application streaming sessions is limited to user accounts that are in the domains that you specify\. You can specify up to 10 domains\. For more information about requirements for enabling Google Drive, see [Enable Google Drive for Your AppStream 2\.0 Users](google-drive.md#enable-google-drive)\.
   + **OneDrive for Business** — Users can link their OneDrive for Business account to AppStream 2\.0\. During application streaming sessions, they can sign in to their OneDrive account, save files to OneDrive, and access their existing files in OneDrive\. You can enable OneDrive for accounts in OneDrive domains only, not for personal accounts\. 
**Note**  
After you select **Enable OneDrive**, type the name of least one organizational domain that is associated with your OneDrive account\. Access to Google Drive during application streaming sessions is limited to user accounts that are in the domains that you specify\. You can specify up to 10 domains\. For more information about requirements for enabling OneDrive, see [Enable OneDrive for Your AppStream 2\.0 Users](onedrive.md#enable-onedrive)\.

1. Choose **Next**\.

1. For **Step 3: User Settings**, select the ways in which your users can transfer data between their streaming session and their local device\. Then, choose whether to enable application settings persistence\. When you're done, choose **Review**\. 

   **Clipboard, file transfer, and print to local device permissions options**:
   + **Clipboard** — By default, users can copy and paste data between their local device and streaming applications\. You can limit Clipboard options so that users can paste data to their remote streaming session only or copy data to their local device only\. You can also disable Clipboard options entirely\. Users can still copy and paste between applications in their streaming session\.
   + **File transfer** — By default, users can upload and download files between their local device and streaming session\. You can limit file transfer options so that users can upload files to their streaming session only or download files to their local device only\. You can also disable file transfer entirely\. 
**Important**  
If your users require AppStream 2\.0 file system redirection to access local drives and folders during their streaming sessions, you must enable both file upload and download\. To use file system redirection, your users must have AppStream 2\.0 client version 1\.0\.480 or later installed\. For more information, see [Enable File System Redirection for Your AppStream 2\.0 Users](enable-file-system-redirection.md)\.
   + **Print to local device** — By default, users can print to their local device from within a streaming application\. When they choose **Print** in the application, they can download a \.pdf file that they can print to a local printer\. You can disable this option to prevent users from printing to a local device\.
**Note**  
These settings affect only whether users can use AppStream 2\.0 data transfer features\. If your image provides access to a browser, network printer, or other remote resource, your users might be able to transfer data to or from their streaming session in other ways\.

   **Application settings persistence options**:
   + **Enable Application Settings Persistence** — Users' application customizations and Windows settings are automatically saved after each streaming session and applied during the next session\. These settings are saved to an Amazon Simple Storage Service \(Amazon S3\) bucket in your account, within the AWS Region in which application settings persistence is enabled\.
   + **Settings Group** — The settings group determines which saved application settings are used for a streaming session from this stack\. If the same settings group is applied to another stack, both stacks use the same application settings\. By default, the settings group value is the name of the stack\.
**Note**  
For information about requirements for enabling and administering application settings persistence, see [Enable Application Settings Persistence for Your AppStream 2\.0 Users](app-settings-persistence.md)\.

1. For **Step 4: Review**, confirm the details for the stack\. To change the configuration for any section, choose **Edit **and make the needed changes\. After you finish reviewing the configuration details, choose **Create**\. 

After the service sets up resources, the **Stacks** page appears\. The status of your new stack appears as **Active** when it is ready to use\. 

## Provide Access to Users<a name="set-up-stacks-fleets-add"></a>

After you create a stack with an associated fleet, you can provide access to users through the AppStream 2\.0 user pool, SAML 2\.0 \[single sign\-on \(SSO\)\], or the AppStream 2\.0 API\. For more information, see [User Pool Administration](user-pool-admin.md) and [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md)\. 

**Note**  
Users in the AppStream 2\.0 user pool can't be assigned to stacks with fleets that are joined to an Active Directory domain\.

After you provide your users with access to AppStream 2\.0, they can start AppStream 2\.0 streaming sessions by using a web browser or by using the AppStream 2\.0 client application for a supported device\. If you provide access to users through the AppStream 2\.0 user pool, they must use a web browser for streaming sessions\. If you use SAML 2\.0 or the AppStream 2\.0 API, you can make the AppStream 2\.0 client available to them\. The AppStream 2\.0 client is a native application that is designed for users who require additional functionality during their AppStream 2\.0 streaming sessions\. For more information, see [Provide Access Through the AppStream 2\.0 Client for Windows](client-application.md)\.

## Clean Up Resources<a name="set-up-stacks-fleets-finish"></a>

You can stop your running fleet and delete your active stack to free up resources and to avoid unintended charges to your account\. We recommend stopping any unused, running fleets\.

Note that you cannot delete a stack with an associated fleet\.

**To clean up your resources**

1. In the navigation pane, choose **Stacks**\.

1. Select the stack and choose **Actions**, **Disassociate Fleet**\. In the confirmation dialog box, choose **Disassociate\.**

1. In the navigation pane, choose **Fleets**\.

1. Select the fleet that you want to stop, choose **Actions**, and then choose **Stop**\. It takes about 5 minutes to stop a fleet\.

1. When the status of the fleet is **Stopped**, choose **Actions**, **Delete**\.

1. In the navigation pane, choose **Stacks**\.

1. Select the stack and choose **Actions**, **Delete**\.