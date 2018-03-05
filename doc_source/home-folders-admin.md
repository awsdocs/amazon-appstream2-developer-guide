# Home Folder Administration<a name="home-folders-admin"></a>

AppStream 2\.0 administrators can enable or disable Home Folders for a stack by using the AWS Management Console for AppStream 2\.0, AWS SDK, or AWS CLI\. For each region, Home Folders are backed up by an S3 bucket\.


+ [Before Enabling Home Folders](#home-folders-guidelines)
+ [Enabling Home Folders](#home-folders-admin-enabling)
+ [Disabling Home Folders](#home-folders-admin-disabling)
+ [Amazon S3 Bucket Storage](#home-folders-s3)
+ [Home Folder Formats](#home-folders-admin-folders)
+ [Using the AWS Command Line Interface or AWS SDKs](#home-folders-admin-cli)

## Before Enabling Home Folders<a name="home-folders-guidelines"></a>

Refer to the following guidelines before enabling Home Folders for a stack:

+ Check that you have the correct IAM permissions for Amazon S3 actions\. For more information, see [IAM Policies and the Amazon S3 Bucket for Home Folders](controlling-access.md#s3-iam-policy)\.

+ Use an image that was created from an AWS base image released on or after May 18, 2017\. For a current list of released AWS images, see [Amazon AppStream 2\.0 Windows Image Version History](base-image-version-history.md)\.

+ Enable network connectivity to Amazon S3 from your VPC by configuring internet access or a VPC endpoint for Amazon S3\. For more information, see [Network Settings for Amazon AppStream 2\.0 ](managing-network.md) and [Home Folders and VPC Endpoints](managing-network.md#managing-network-vpce-iam-policy)\.

## Enabling Home Folders<a name="home-folders-admin-enabling"></a>

An AppStream 2\.0 administrator can enable or disable Home Folders while creating a stack \(see [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install)\), or after the stack is created\.

The first time you enable Home Folders for an AppStream 2\.0 stack in an AWS region, the service creates an S3 bucket in your account in that same region\. The same bucket is used to store the content of Home Folders for all users and all stacks in that region\. For more information, see [Amazon S3 Bucket Storage](#home-folders-s3)\.

**To enable Home Folders while creating a stack**

+ Follow the instructions at [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), and ensure that **Enable Home Folders** is selected\.

**To enable Home Folders for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **Stacks**, and select the stack for which to enable Home Folders\.

1. Below the stack list, choose **Storage** and select **Enable Home Folders**\.

1. Confirm the enable action in the resulting dialog box by choosing **Enable**\.

## Disabling Home Folders<a name="home-folders-admin-disabling"></a>

You can disable Home Folders for a stack without losing user content already stored in Home Folders\. Disabling Home Folders for a stack has the following effects:

+ If the stack has sessions that are in use, an error message is shown to any users currently using the session, and these users can no longer store content to Home Folders in the session\. 

+ Any new sessions using the stack with Home Folders disabled do not present Home Folders\. 

+ Other stacks that have Home Folders enabled are not affected by this stack's disable operation, and continue to provide users access to their data within those stacks' streaming sessions\. Only the specific stack for which Home Folders is disabled is affected\.

+ Even if Home Folders are disabled for all stacks, AppStream 2\.0 does not delete the user content\.

To restore access to Home Folders for the stack, enable Home Folders again by following the steps described earlier in this topic\. 

**To disable Home Folders while creating a stack**

+ Follow the instructions at [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install) and ensure that **Enable Home Folders** is cleared\.

**To disable Home Folders for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **Stacks**, and select the stack\.

1. Below the stack list, choose **Storage** and clear **Enable Home Folders**\.

1. Confirm the disable action in the resulting dialog box by typing **CONFIRM** \(case\-sensitive\) and choosing **Disable**\.

## Amazon S3 Bucket Storage<a name="home-folders-s3"></a>

AppStream 2\.0 manages user content stored in Home Folders by using S3 buckets created in your account\. For every region, AppStream 2\.0 creates a bucket in your account and stores all user content generated from streaming sessions of stacks in that region in that bucket\. The buckets are fully managed by the service without any admin inputs or configuration\. The buckets are named in a specific format as follows: 

```
appstream2-36fb080bb8-region-code-account-id-without-hyphens
```

Where `region-code` is the AWS region code in which the stack is created and `account-id-without-hyphens` is your AWS account ID\. The first part of the bucket name, `appstream2-36fb080bb8-`, does not change across accounts or regions\. 

For example, if you enable Home Folders for stacks in region us\-west\-2 on account number 123456789012, the service creates an S3 bucket in the us\-west\-2 region with the name shown\. This bucket name cannot change or be deleted without manual modification by an administrator\.

```
appstream2-36fb080bb8-us-west-2-123456789012
```

As mentioned, disabling Home Folders for stacks does not delete any user content stored in the S3 bucket\. To permanently delete user content, an administrator with adequate access must do so from the Amazon S3 console\. AppStream 2\.0 adds a bucket policy that prevents accidental deletion of the bucket\. For more information, see [IAM Policies and the Amazon S3 Bucket for Home Folders](controlling-access.md#s3-iam-policy)\. 

### Additional Resources<a name="home-folders-admin-additional"></a>

To learn more about managing S3 buckets and best practices, see the following topics in the *Amazon Simple Storage Service Developer Guide*: 

+ You can provide offline access to user data for your users with Amazon S3 policies\. For more information, see [Allow Users to Access a Personal "Home Directory" in Amazon S3](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html#iam-policy-example-s3-home-directory)\.

+ You can enable file versioning for content stored in S3 buckets used by AppStream 2\.0\. For more information, see [Using Versioning](http://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html)\.

## Home Folder Formats<a name="home-folders-admin-folders"></a>

When Home Folders are enabled, users are provided with a unique folder in which to store their content \(one folder per user\)\. The folder is created and maintained as a unique Amazon S3 object within the bucket for that region\. The hierarchy of a user folder depends on how the user launches a streaming session\.

### AWS SDKs and AWS CLI<a name="home-folders-admin-folders-aws"></a>

For sessions created using `CreateStreamingURL` or `create-streaming-url` the user folder structure is as follows:

```
bucket-name/user/custom/user-id-SHA-256-hash/
```

Where `bucket-name` is in the format shown in [Amazon S3 Bucket Storage](#home-folders-s3) and `user-id-SHA-256-hash` is the user\-specific folder name created using a lower case SHA\-256 hash hexadecimal string generated from the `UserId` value passed to the CreateStreamingURL API operation or `create-streaming-url` command\. For more information, see [CreateStreamingURL](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) in the *Amazon AppStream 2\.0 API Reference* and [create\-streaming\-url](http://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) in the *AWS CLI Command Reference*\.

The following example folder structure applies to session access using the API or CLI with a `UserId` testuser@mydomain\.com, account id 123456789012 in region us\-west\-2:

```
appstream2-36fb080bb8-us-west-2-123456789012/user/custom/a0bcb1da11f480d9b5b3e90f91243143eac04cfccfbdc777e740fab628a1cd13/
```

Administrators can identify the folder for a user by generating the lower case SHA\-256 hash value of the `UserId` using websites or open source coding libraries available online\.

### SAML<a name="home-folders-admin-folders-saml"></a>

For sessions created using SAML federation, the user folder structure is as follows:

```
bucket-name/user/federated/user-id-SHA-256-hash/
```

In this case, `user-id-SHA-256-hash` is the folder name created using a lower case SHA\-256 hash hexadecimal string generated from the `NameID` SAML attribute value passed in the SAML federation request\. To differentiate users with the same name belonging to two different domains, send the SAML request with `NameID` in the format `domainname\username`\. For more information, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\.

The following example folder structure applies to session access using SAML federation with a `NameID` SAMPLEDOMAIN\\testuser, account ID 123456789012 in region us\-west\-2:

```
appstream2-36fb080bb8-us-west-2-123456789012/user/federated/8dd9a642f511609454d344d53cb861a71190e44fed2b8af9fde0c507012a9901
```

Administrators can identify the folder for a user by generating the lower case SHA\-256 hash value of the `NameID` using websites or open source coding libraries available online\.

## Using the AWS Command Line Interface or AWS SDKs<a name="home-folders-admin-cli"></a>

You can enable and disable Home Folders for a stack using the AWS CLI or AWS SDKs\.

Use the following [create\-stack](http://docs.aws.amazon.com/cli/latest/reference/appstream/create-stack.html) command enable Home Folders while creating a new stack:

```
aws appstream create-stack --name ExampleStack –-storage-connectors type=HOMEFOLDERS
```

Use the following [update\-stack](http://docs.aws.amazon.com/cli/latest/reference/appstream/update-stack.html) command to enable Home Folders for an existing stack:

```
aws appstream update-stack –-name ExistingStack –-storage-connectors type=HOMEFOLDERS
```

Use the following command to disable Home Folders for an existing stack\. This command does not delete any user data\.

```
aws appstream update-stack –name ExistingStack –-delete-storage-connectors
```