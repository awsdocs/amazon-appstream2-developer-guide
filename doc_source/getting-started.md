# Getting Started with Amazon AppStream 2\.0<a name="getting-started"></a>

To stream your applications, Amazon AppStream 2\.0 requires an environment consisting of a stack, a fleet, and at least one application image\. This tutorial describes how to configure a sample AppStream 2\.0 environment for application streaming and give users access to that stream\.


+ [Step 1: Set Up a Sample Stack, Choose an Image, and Configure a Fleet](#getting-started-stack)
+ [Step 2: Provide Access to Users](#getting-started-access)
+ [Resources](#getting-started-next)

## Step 1: Set Up a Sample Stack, Choose an Image, and Configure a Fleet<a name="getting-started-stack"></a>

Before you can stream your applications, you need to set up a stack, choose an image that has applications installed, and configure a fleet\. In this step, you use a template to help simplify these tasks\.

**To set up a sample stack, choose an image, and configure a fleet**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose **Get Started** if you are new to the console, or **Quick Links** from the left navigation menu\. Choose **Set up with sample apps**\.

1. For **Step 1: Stack Details**, keep the default sample stack name and description, or type new ones\. You can also specify a redirect URL\. If you specify a redirect URL, after users’ streaming sessions end, the users are redirected to that URL\. Choose **Next**\.

1. For **Step 2: Choose Image**, choose an image, and then choose **Next**\. The sample image contains pre\-installed open source applications for evaluation purposes\. For more information, see [Amazon AppStream 2\.0 Windows Image Version History](base-image-version-history.md)\.

1. For **Step 3: Configure Fleet**, we recommend that you keep the default values and choose **Next**\. You can change most of these values after fleet creation\.

   + **Choose instance type** — Choose the instance type that matches the performance requirements of your applications\. All streaming instances in your fleet launch with the instance type that you select\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.

   + **Fleet type** — Choose the fleet type that suits your use case\. The fleet type determines its immediate availability and how you pay for it\.

   + **Maximum session duration** — Choose the maximum amount of time that a streaming session can remain active\. If users are still connected to a streaming session five minutes before this limit is reached, they are prompted to save any open documents before being disconnected\.

   + **Disconnect timeout** — Choose the time that a streaming instance should remain active after users disconnect\. If users try to reconnect to the streaming session after a disconnection or network interruption within this time interval, they are connected to the previous session\. Otherwise, they are connected to a new session with a new instance\. If you associate a stack with a fleet for which a redirect URL is specified, after users’ streaming sessions end, the users are redirected to that URL\.

     If a user ends the session by choosing **End Session** on the streaming session toolbar, the disconnect timeout does not apply\. Instead, the user is prompted to save any open documents, and then immediately disconnected from the streaming instance\. 

   + **Minimum capacity** — Choose a minimum number of instances for your fleet based on the minimum number of expected concurrent users\. Every unique user session is served by an instance\. For example, to have your stack support 100 concurrent users during low demand, specify a minimum capacity of 100\. This ensures that 100 instances are running even if there are fewer than 100 users\.

   + **Maximum capacity** — Choose a maximum number of instances for your fleet based on the maximum number of expected concurrent users\. Every unique user session is served by an instance\. For example, to have your stack support 500 concurrent users during high demand, specify a maximum capacity of 500\. This ensures that up to 500 instances can be created on demand\.

1. For **Step 4: Configure Network**, choose a VPC and two subnets with access to the network resources that your application needs\. If you don't have a VPC or subnets, you can create them using the links provided and then click the refresh icons\. For **Security groups**, you can select up to five security groups\. Otherwise, the default security group is used\. For more information, see [Network Settings for Fleet and Image Builder Instances](managing-network.md)\.

1. For **Step 5: Enable Storage**, keep the default setting, **Enable Home Folders**, and choose **Review**\. Home Folders offer persistent storage for AppStream 2\.0 streaming sessions\. For more information, see [Persistent Storage with AppStream 2\.0 Home Folders](home-folders.md)\.

1. Choose **Create**\.

   After the service sets up resources, the **Stacks** page appears\. The status of your new stack is **Active** when it is available to work with from the console\.

   Optionally, you can apply one or more tags to help manage the stack\. Choose **Tags**, choose **Add/Edit Tags**, choose **Add Tag**, specify the key and value for the tag, and then choose **Save**\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

## Step 2: Provide Access to Users<a name="getting-started-access"></a>

After you create a stack, each user needs an active URL for access\. The AppStream 2\.0 User Pool feature enables you to create and manage users, using a permanent login portal URL\. For more information, see [Manage Access Using the AppStream 2\.0 User Pool](user-pool.md)\. To quickly test application streaming without setting up users, create a temporary URL as shown below\.

**To provide access to users with a temporary URL**

1. In the navigation pane, choose **Stacks**\. Select the radio button for the stack, and then choose **Actions**, **Create Streaming URL**\.

1. For **User id**, type the user ID\. Select an expiration time, which determines how long the generated URL is valid\.

1. To view the user ID and URL, choose **Get URL**\.

1. To copy the link to the clipboard, choose **Copy Link**\. 

## Resources<a name="getting-started-next"></a>

For more information, see the following:

+ Learn how to use the AppStream 2\.0 image builder to add your own apps and create images you can stream\. For more information, see [Tutorial: Create a Custom Image](tutorial-image-builder.md)\.

+ Provide persistent storage for your session users using AppStream 2\.0 Home Folders\. For more information, see [Persistent Storage with AppStream 2\.0 Home Folders](home-folders.md)\.

+ Integrate your AppStream 2\.0 streaming resources with your Microsoft Active Directory environment\. For more information, see [Using Active Directory Domains with AppStream 2\.0](active-directory.md)\.

+ Control who has access to your AppStream 2\.0 streaming instances\. For more information, see [Controlling Access to Amazon AppStream 2\.0 with IAM Roles and Policies](controlling-access.md), [Manage Access Using the AppStream 2\.0 User Pool](user-pool.md) and [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\.

+ Monitor your AppStream 2\.0 resources using Amazon CloudWatch\. For more information, see [AppStream 2\.0 Metrics and Dimensions](monitoring.md#monitoring-with-cloudwatch)\.

+ Troubleshoot your AppStream 2\.0 streaming experience\. For more information, see [Troubleshooting](troubleshooting.md)\.