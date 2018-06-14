# Enable and Administer Home Folders for Your AppStream 2\.0 Users<a name="home-folders"></a>

AppStream 2\.0 supports persistent storage for your users with home folders and Google Drive\. You can enable one or both options as needed for your organization\. When you enable home folders for an AppStream 2\.0 stack, end users of the stack can access a persistent storage folder during their application streaming sessions\. No further conﬁguration is required on your users' part to access their home folder\. Data stored by users in their home folder is automatically backed up to an Amazon S3 bucket in your AWS account and is made available in subsequent sessions for those users\. 

**Note**  
As an administrator, you can access a home folder in the following default location on an image builder instance: C:\\Users\\PhotonUser\\My Files\\Home Folder\. Use this path if you are configuring your applications to save to the home folder\. In some cases, your end users may not be able to find their home folder because some applications do not recognize the redirect that displays the home folder as a top\-level folder in File Explorer\. If this is the case, your users can access their home folder by browsing to the same directory in File Explorer\.

**Topics**
+ [Enable Home Folders for Your AppStream 2\.0 Users](#enable-home-folders)
+ [Administer Your Home Folders](#home-folders-admin)
+ [Provide Your AppStream 2\.0 Users with Guidance for Working with Home Folders](#home-folders-end-user)

## Enable Home Folders for Your AppStream 2\.0 Users<a name="enable-home-folders"></a>

Before enabling home folders, you must do the following:
+ Check that you have the correct IAM permissions for Amazon S3 actions\. For more information, see [IAM Policies and the Amazon S3 Bucket for Home Folders](controlling-access.md#s3-iam-policy)\.
+ Use an image that was created from an AWS base image released on or after May 18, 2017\. For a current list of released AWS images, see [Amazon AppStream 2\.0 Windows Image Version History](base-image-version-history.md)\.
+ Enable network connectivity to Amazon S3 from your VPC by configuring internet access or a VPC endpoint for Amazon S3\. For more information, see [Network Settings for Amazon AppStream 2\.0 ](managing-network.md) and [ Home Folders and VPC Endpoints](managing-network.md#managing-network-vpce-iam-policy)\.

You can enable or disable home folders while creating a stack \(see [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install)\), or after the stack is created by using the AWS Management Console for AppStream 2\.0, AWS SDK, or AWS CLI\. For each AWS Region, home folders are backed up by an S3 bucket\.

The first time you enable home folders for an AppStream 2\.0 stack in an AWS Region, the service creates an S3 bucket in your account in that same region\. The same bucket is used to store the content of home folders for all users and all stacks in that region\. For more information, see [Amazon S3 Bucket Storage](#home-folders-s3)\.

**To enable home folders while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), and ensure that **Enable Home Folders** is selected\.

**To enable home folders for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **Stacks**, and select the stack for which to enable home folders\.

1. Below the stacks list, choose **Storage** and select **Enable Home Folders**\.

1. In the **Enable Home Folders** dialog box, choose **Enable**\.

## Administer Your Home Folders<a name="home-folders-admin"></a>

**Topics**
+ [Disable Home Folders](#home-folders-admin-disabling)
+ [Amazon S3 Bucket Storage](#home-folders-s3)
+ [Home Folder Formats](#home-folders-admin-folders)
+ [Using the AWS Command Line Interface or AWS SDKs](#home-folders-admin-cli)

### Disable Home Folders<a name="home-folders-admin-disabling"></a>

You can disable home folders for a stack without losing user content already stored in home folders\. Disabling home folders for a stack has the following effects:
+ For any users who are connected to active streaming sessions for the stack, an error message displays during the session to inform these users that they can no longer store content in their home folder\. 
+ Any new sessions that use the stack with home folders disabled do not present home folders\. 
+ Disabling home folders for one stack does not disable it for other stacks\. Only the specific stack for which home folders is disabled is affected\.
+ Even if home folders are disabled for all stacks, AppStream 2\.0 does not delete the user content\.

To restore access to home folders for the stack, enable home folders again by following the steps described earlier in this topic\. 

**To disable home folders while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install) and ensure that **Enable Home Folders** is cleared\.

**To disable home folders for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **Stacks**, and select the stack\.

1. Below the stacks list, choose **Storage** and clear **Enable Home Folders**\.

1. In the **Disable Home Folders** dialog box, type `CONFIRM` \(case\-sensitive\) to confirm your choice, then choose **Disable**\.

### Amazon S3 Bucket Storage<a name="home-folders-s3"></a>

AppStream 2\.0 manages user content stored in home folders by using S3 buckets created in your account\. For every region, AppStream 2\.0 creates a bucket in your account and stores all user content generated from streaming sessions of stacks in that region in that bucket\. The buckets are fully managed by the service without any admin inputs or configuration\. The buckets are named in a specific format as follows: 

```
appstream2-36fb080bb8-region-code-account-id-without-hyphens
```

Where `region-code` is the AWS region code in which the stack is created and `account-id-without-hyphens` is your AWS account ID\. The first part of the bucket name, `appstream2-36fb080bb8-`, does not change across accounts or regions\. 

For example, if you enable home folders for stacks in region us\-west\-2 on account number 123456789012, the service creates an S3 bucket in the us\-west\-2 region with the name shown\. This bucket name cannot change or be deleted without manual modification by an administrator\.

```
appstream2-36fb080bb8-us-west-2-123456789012
```

As mentioned, disabling home folders for stacks does not delete any user content stored in the S3 bucket\. To permanently delete user content, an administrator with adequate access must do so from the Amazon S3 console\. AppStream 2\.0 adds a bucket policy that prevents accidental deletion of the bucket\. For more information, see [IAM Policies and the Amazon S3 Bucket for Home Folders](controlling-access.md#s3-iam-policy)\. 

#### Additional Resources<a name="home-folders-admin-additional"></a>

To learn more about managing S3 buckets and best practices, see the following topics in the *Amazon Simple Storage Service Developer Guide*: 
+ You can provide offline access to user data for your users with Amazon S3 policies\. For more information, see [Allow Users to Access a Personal "Home Directory" in Amazon S3](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html#iam-policy-example-s3-home-directory)\.
+ You can enable file versioning for content stored in S3 buckets used by AppStream 2\.0\. For more information, see [Using Versioning](http://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html)\.

### Home Folder Formats<a name="home-folders-admin-folders"></a>

When home folders are enabled, users are provided with a unique folder in which to store their content \(one folder per user\)\. The folder is created and maintained as a unique Amazon S3 object within the bucket for that region\. The hierarchy of a user folder depends on how the user launches a streaming session\.

#### AWS SDKs and AWS CLI<a name="home-folders-admin-folders-aws"></a>

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

#### SAML<a name="home-folders-admin-folders-saml"></a>

For sessions created using SAML federation, the user folder structure is as follows:

```
bucket-name/user/federated/user-id-SHA-256-hash/
```

In this case, `user-id-SHA-256-hash` is the folder name created using a lower case SHA\-256 hash hexadecimal string generated from the `NameID` SAML attribute value passed in the SAML federation request\. To differentiate users with the same name belonging to two different domains, send the SAML request with `NameID` in the format `domainname\username`\. For more information, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\.

The following example folder structure applies to session access using SAML federation with a `NameID` SAMPLEDOMAIN\\testuser, account ID 123456789012 in region us\-west\-2:

```
appstream2-36fb080bb8-us-west-2-123456789012/user/federated/34832ec7383294b01bface2ebc32ab9cacfb5fc12ad33d5eb5d0fcc1d78ae144
```

When part or all of the NameID string is capitalized \(as the domain name *SAMPLEDOMAIN* is in the example\), AppStream 2\.0 converts the string to lowercase and then generates the hash value based on the lowercase string\. So for the example, AppStream 2\.0 converts the `NameID` string *SAMPLEDOMAIN\\test user* to *sampledomain\\testuser* and generates the hash value based on that string\. Administrators can identify the folder for a user by generating the SHA\-256 hash value of the lowercase `NameID` by using websites or open source coding libraries available online\.

### Using the AWS Command Line Interface or AWS SDKs<a name="home-folders-admin-cli"></a>

You can enable and disable home folders for a stack using the AWS CLI or AWS SDKs\.

Use the following [create\-stack](http://docs.aws.amazon.com/cli/latest/reference/appstream/create-stack.html) command enable home folders while creating a new stack:

```
aws appstream create-stack --name ExampleStack –-storage-connectors type=HOMEFOLDERS
```

Use the following [update\-stack](http://docs.aws.amazon.com/cli/latest/reference/appstream/update-stack.html) command to enable home folders for an existing stack:

```
aws appstream update-stack –-name ExistingStack –-storage-connectors type=HOMEFOLDERS
```

Use the following command to disable home folders for an existing stack\. This command does not delete any user data\.

```
aws appstream update-stack –name ExistingStack –-delete-storage-connectors
```

## Provide Your AppStream 2\.0 Users with Guidance for Working with Home Folders<a name="home-folders-end-user"></a>

To help your users understand how to work with home folders, you can provide them with the following information\. 

**Guidance for Users**

When you are signed in to an AppStream 2\.0 streaming session, you can do the following with your home folder: 
+ Open and edit files and folders that you store in your home folder\. Content that is stored in your home folder is specific to you and cannot be accessed by other users\.
+ Upload and download files between your local computer and your home folder\. AppStream 2\.0 continuously checks for the most recently modified files and folders and backs them up to your home folder\.
+ When you are working in an application, you can access files and folders that are stored in your home folder by choosing **File Open** from the application interface and browsing to the file or folder that you want to open\. To save changes to a file that you are working in to your home folder, choose **File Save** from the application interface and browse to the location in your home folder where you want to save the file\. 
+ You can also access your home folder by choosing **My Files** from the web view session toolbar\.
**Note**  
If your home folder doesn't appear, you can view your home folder files by browsing to the following directory in File Explorer: C:\\Users\\PhotonUser\\My Files\\Home Folder\. 

**To upload and download files between your local computer and your home folder**

1. In the AppStream 2\.0 web view session, choose the **My Files** icon at the top left of your browser\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-WebView-MyFolders2.png)

1. Navigate to an existing folder, or choose **Add Folder** to create a new folder\.

1. When the folder that you want is displayed, do one of the following: 
   + To upload a file to the folder, select the file that you want to upload, and choose **Upload**\.
   + To download a file from the folder, select the file that you want to download, choose the down arrow to the right of the file name, and choose **Download**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/home-folder-new.png)