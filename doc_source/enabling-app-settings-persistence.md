# Enabling Application Settings Persistence<a name="enabling-app-settings-persistence"></a>

**Topics**
+ [Prerequisites for Enabling Application Settings Persistence](#prerequisites-app-settings-persistence)
+ [Best Practices for Enabling Application Settings Persistence](#best-practices-app-settings-persistence)
+ [How to Enable Application Settings Persistence](#howto-enable-app-settings-persistence)

## Prerequisites for Enabling Application Settings Persistence<a name="prerequisites-app-settings-persistence"></a>

To enable application settings persistence, you must first do the following:
+ Check that you have the correct AWS Identity and Access Management \(IAM\) permissions for Amazon S3 actions\. For more information, see the *IAM Policies and the Amazon S3 Bucket for Home Folders* section in [Identity and Access Management for Amazon AppStream 2\.0](controlling-access.md)\.
+ Use an image that was created from a base image published by AWS on or after December 7, 2017\. For a current list of released AWS base images, see [AppStream 2\.0 Base Image Version History](base-image-version-history.md)\.
+ Associate the stack on which you plan to enable this feature with a fleet based on an image that uses a version of the AppStream 2\.0 agent released on or after August 29, 2018\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.
+ Enable network connectivity to Amazon S3 from your virtual private cloud \(VPC\) by configuring internet access or a VPC endpoint for Amazon S3\. For more information, see the *Home Folders and VPC Endpoints* section in [Networking and Access for Amazon AppStream 2\.0](managing-network.md)\.

## Best Practices for Enabling Application Settings Persistence<a name="best-practices-app-settings-persistence"></a>

To enable application settings persistence without providing internet access to your instances, use a VPC endpoint\. This endpoint must be in the VPC to which your AppStream 2\.0 instances are connected\. You must attach a custom policy to enable AppStream 2\.0 access to the endpoint\. For information about how to create the custom policy, see the *Home Folders and VPC Endpoints* section in [Networking and Access for Amazon AppStream 2\.0](managing-network.md)\. For more information about private Amazon S3 endpoints, see [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html) and [Endpoints for Amazon S3](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-s3.html) in the *Amazon VPC User Guide*\.

## How to Enable Application Settings Persistence<a name="howto-enable-app-settings-persistence"></a>

You can enable or disable application settings persistence while creating a stack or after the stack is created by using the AppStream 2\.0 console, AppStream 2\.0 API, an AWS SDK, or the AWS Command Line Interface \(CLI\)\. For each AWS Region, persistent application settings are stored in an S3 bucket in your account\.

The first time you enable application settings persistence for a stack in an AWS Region, AppStream 2\.0 creates an S3 bucket in your AWS account in the same Region\. The same bucket stores the application settings VHD file for all users and all stacks in that AWS Region\. For more information, see *Amazon S3 Bucket Storage* in [Administer the VHDs for Your Users' Application Settings](administer-app-settings-vhds.md)\.

**To enable application settings persistence while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), and make sure that **Enable Application Settings Persistence** is selected\.

**To enable application settings persistence for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to enable application settings persistence\.

1. Below the stacks list, choose **User Settings**, **Application Settings Persistence**, **Edit**\.

1. In the **Application Settings Persistence** dialog box, choose **Enable Application Settings Persistence**\. 

1. Confirm the current settings group or type the name of a new settings group\. When you're done, choose **Update**\.

New streaming sessions now have application settings persistence enabled\.