# Create AppStream 2\.0 Stacks and Fleets<a name="set-up-stacks-fleets"></a>

To stream your applications, Amazon AppStream 2\.0 requires an environment consisting of a stack, an associated fleet and at least one application image\. This tutorial walks through the steps to set up a stack and a fleet, and how to give users access to the stack\. If you haven't already done so, we recommend that you try the procedures in [Getting Started with Amazon AppStream 2\.0](getting-started.md) first\.

If you want to create an image to use, see [Tutorial: Create a Custom Image](tutorial-image-builder.md)\.

If you intend to join a fleet to an Active Directory domain, configure your Active Directory before following the steps below\. For more information, see [Using Active Directory Domains with AppStream 2\.0](active-directory.md)\.


+ [Create a Fleet](#set-up-stacks-fleets-create)
+ [Create a Stack](#set-up-stacks-fleets-install)
+ [Provide Access to Users](#set-up-stacks-fleets-add)
+ [Clean Up Resources](#set-up-stacks-fleets-finish)

## Create a Fleet<a name="set-up-stacks-fleets-create"></a>

Set up and create a fleet from which user applications are executed and streamed\.

**To set up and create a fleet**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose **Get Started** if you are new to the console, or **Fleets** from the left navigation pane\. Choose **Create Fleet**\.

1. For **Step 1: Provide Fleet Details**, provide a fleet name, optional display name, and optional description\. Choose **Next**\.

1. For **Step 2: Choose an Image**, choose an image that meets your needs and then choose **Next**\.

1. For **Step 3: Configure Fleet**, do the following:

   1. For **Choose instance type**, choose the instance type that meets the performance requirements of your applications\.

   1. For **Fleet type**, choose the fleet type that suits your use case\. The fleet type determines its immediate availability and how you pay for it\.

   1. For **Maximum session duration** — Choose the maximum amount of time that a streaming session can remain active\. If users are still connected to a streaming session five minutes before this limit is reached, they are prompted to save any open documents before being disconnected\. 

   1. For **Disconnect timeout**, choose the time that a streaming instance should remain active after users disconnect\. If users try to reconnect to the streaming session after a disconnection or network interruption within this time interval, they are connected to the previous session\. Otherwise, they are connected to a new session with a new instance\. If you associate a stack with a fleet for which a redirect URL is specified, after users’ streaming sessions end, the users are redirected to that URL\.

      If a user ends the session by choosing **End Session** on the streaming session toolbar, the disconnect timeout does not apply\. Instead, the user is prompted to save any open documents, and then immediately disconnected from the streaming instance\. 

   1. For **Minimum capacity**, choose a minimum number of instances for your fleet based on the minimum number of expected concurrent users\.

   1. For **Maximum capacity**, choose a maximum number of instances for your fleet based on the maximum number of expected concurrent users\.

   1. For **Scaling details**, specify the scaling policies that AppStream 2\.0 uses to increase and decrease the capacity of your fleet\. Note that the size of your fleet is limited by the minimum and maximum capacity that you specified\. For more information, see [Fleet Auto Scaling for Amazon AppStream 2\.0](autoscaling.md)\.

1. For **Step 4: Configure Network**, do the following:

   1. To add internet access for fleet instances in a VPC with a public subnet, choose **Default Internet Access**\. If you are providing internet access using a NAT gateway, leave **Default Internet Access** unselected\. For more information, see [Network Settings for Fleet and Image Builder Instances](managing-network.md)\.

   1. Choose a VPC and two subnets with access to the network resources that your application needs\. If you don't have a VPC or subnets, you can create them using the links provided and then click the refresh icons\.

   1. For **Security groups**, select up to five security groups to associate with this fleet\. Otherwise, the default security group for the VPC is used\. If you need to create a security group, use the link provided and then click the refresh icon\.

   1. For **Active Directory Domain \(Optional\)**, choose the Active Directory and organizational unit \(OU\) for your streaming instance computer objects\. Ensure that the network access settings you selected enable DNS resolvability and communication with your directory\. For more information, see [Using Active Directory Domains with AppStream 2\.0](active-directory.md)\.

1. Choose **Create**\.

   The initial status of your new fleet is **Starting**\. You cannot associate the fleet with a stack and use it for streaming sessions until the status of the fleet is **Running**\.

   Optionally, you can apply one or more tags to help manage the fleet\. Choose **Tags**, choose **Add/Edit Tags**, choose **Add Tag**, specify the key and value for the tag, and then choose **Save**\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

## Create a Stack<a name="set-up-stacks-fleets-install"></a>

Set up and create a stack to control access to your fleet\.

**To set up and create a stack**

1. In the left navigation pane, choose **Stacks**, and then choose **Create Stack**\.

1. For **Step 1: Stack Details**, provide a stack name\. Optionally, you can also provide a display name, description, and redirect URL\. If you specify a redirect URL, after users’ streaming sessions end, the users are redirected to that URL\. For **Fleet**, choose the fleet to associate with your stack\. If you need to create a fleet, use the link provided and then click the refresh icon\. Choose **Next**\.

1. For **Step 2: Enable Storage**, you can enable persistent storage for the stack users by selecting **Enable Home Folders**\. Choose **Review**\.

1. Choose **Create**\.

   The status of your new stack is **Active** when it is available to work with from the console\. 

   Optionally, you can apply one or more tags to help manage the stack\. Choose **Tags**, choose **Add/Edit Tags**, choose **Add Tag**, specify the key and value for the tag, and then choose **Save**\. For more information, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

## Provide Access to Users<a name="set-up-stacks-fleets-add"></a>

After you create a stack with an associated fleet, you can provide access to users through the AppStream 2\.0 user pool\. For more information, see [User Pool Administration](user-pool-admin.md)\.

Note that user pool users cannot be assigned to stacks with fleets that are joined to an Active Directory domain\.

## Clean Up Resources<a name="set-up-stacks-fleets-finish"></a>

You can stop your running fleet and delete your active stack to free up resources and to avoid unintended charges to your account\. We recommend stopping any unused, running fleets\.

Note that you cannot delete a stack with an associated fleet\.

**To clean up your resources**

1. In the navigation pane, choose **Stacks**\.

1. Select the stack and choose **Actions**, **Disassociate Fleet**\.

1. From **Stack Details**, open the **Associated Fleet** link to select the fleet\.

1. Choose **Actions**, **Stop**\. It takes about 5 minutes to stop a fleet\.

1. When the status of the fleet is **Stopped**, choose **Actions**, **Delete**\.

1. In the navigation pane, choose **Stacks**\.

1. Select the stack and choose **Actions**, **Delete**\.