# Enable and Administer Home Folders for Your AppStream 2\.0 Users<a name="home-folders"></a>

AppStream 2\.0 supports the following persistent storage options for users in your organization: 
+ Home folders
+ Google Drive for G Suite
+ OneDrive for Business

You can enable one or more options for your organization\. When you enable home folders for an AppStream 2\.0 stack, users of the stack can access a persistent storage folder during their application streaming sessions\. No further conﬁguration is required for your users to access their home folder\. Data stored by users in their home folder is automatically backed up to an Amazon Simple Storage Service bucket in your AWS account and is made available to those users in subsequent sessions\. 

Files and folders are encrypted in transit using Amazon S3's SSL endpoints\. Files and folders are encrypted at rest using Amazon S3\-managed encryption keys\. 

Home folders are stored on fleet instances in the following default locations:
+ Non\-domain\-joined instances: C:\\Users\\PhotonUser\\My Files\\Home Folder
+ Domain\-joined instances: C:\\Users\\%username%\\My Files\\Home Folder

As an administrator, use the applicable path if you configure your applications to save to the home folder\. In some cases, your users may not be able to find their home folder because some applications do not recognize the redirect that displays the home folder as a top\-level folder in File Explorer\. If this is the case, your users can access their home folder by browsing to the same directory in File Explorer\.

**Topics**
+ [Files and Directories Associated with Compute\-Intensive Applications](#storage-solutions-files-directories-associated-with-compute-intensive-applications)
+ [Enable Home Folders for Your AppStream 2\.0 Users](#enable-home-folders)
+ [Administer Your Home Folders](#home-folders-admin)

## Files and Directories Associated with Compute\-Intensive Applications<a name="storage-solutions-files-directories-associated-with-compute-intensive-applications"></a>

During AppStream 2\.0 streaming sessions, saving large files and directories associated with compute\-intensive applications to persistent storage can take longer than saving files and directories required for basic productivity applications\. For example, it might take longer for applications to save a large amount of data or frequently modify the same files than it would to save files created by applications that perform a single write action\. It might also take longer to save many small files\.

If your users save files and directories associated with compute\-intensive applications and AppStream 2\.0 persistent storage options aren't performing as expected, we recommend that you use a Server Message Block \(SMB\) solution such as Amazon FSx for Windows File Server or an AWS Storage Gateway file gateway\. Following are examples of files and directories associated with compute\-intensive applications that are more suitable for use with these SMB solutions:
+ Workspace folders for integrated development environments \(IDEs\)
+ Local database files
+ Scratch space folders created by graphics simulation applications

For more information, see:
+  [https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)
+ [Using Amazon FSx with Amazon AppStream 2\.0 ](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-amazon-fsx-with-amazon-appstream-2-0/)
+ [File gateways](https://docs.aws.amazon.com/storagegateway/latest/userguide/StorageGatewayConcepts.html#file-gateway-concepts) in the *AWS Storage Gateway User Guide*

## Enable Home Folders for Your AppStream 2\.0 Users<a name="enable-home-folders"></a>

Before enabling home folders, you must do the following:
+ Check that you have the correct AWS Identity and Access Management \(IAM\) permissions for Amazon S3 actions\. For more information, see [Using IAM Policies to Manage Administrator Access to the Amazon S3 Bucket for Home Folders and Application Settings Persistence](s3-iam-policy.md)\.
+ Use an image that was created from an AWS base image released on or after May 18, 2017\. For a current list of released AWS images, see [AppStream 2\.0 Base Image Release Notes](base-image-version-history.md)\.
+ Enable network connectivity to Amazon S3 from your virtual private cloud \(VPC\) by configuring internet access or a VPC endpoint for Amazon S3\. For more information, see [Networking and Access for Amazon AppStream 2\.0](managing-network.md) and [Using Amazon S3 VPC Endpoints for Home Folders and Application Settings Persistence](managing-network-vpce-iam-policy.md)\.

You can enable or disable home folders while creating a stack \(see [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install)\), or after the stack is created by using the AWS Management Console for AppStream 2\.0, AWS SDK, or AWS CLI\. For each AWS Region, home folders are backed up by an Amazon S3 bucket\.

The first time you enable home folders for an AppStream 2\.0 stack in an AWS Region, the service creates an Amazon S3 bucket in your account in that same Region\. The same bucket is used to store the content of home folders for all users and all stacks in that Region\. For more information, see [Amazon S3 Bucket Storage](#home-folders-s3)\.

**Note**  
For guidance that you can provide your users to help them get started with using home folders during AppStream 2\.0 streaming sessions, see [Use Home Folders](home-folders-end-user.md)\.

**To enable home folders while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), and make sure that **Enable Home Folders** is selected\.

**To enable home folders for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to enable home folders\.

1. Below the stacks list, choose **Storage** and select **Enable Home Folders**\.

1. In the **Enable Home Folders** dialog box, choose **Enable**\.

## Administer Your Home Folders<a name="home-folders-admin"></a>

**Topics**
+ [Disable Home Folders](#home-folders-admin-disabling)
+ [Amazon S3 Bucket Storage](#home-folders-s3)
+ [Home Folder Content Synchronization](#home-folders-content-synchronization)
+ [Home Folder Formats](#home-folders-admin-folders)
+ [Using the AWS Command Line Interface or AWS SDKs](#home-folders-admin-cli)
+ [Additional Resources](#home-folders-admin-additional)

### Disable Home Folders<a name="home-folders-admin-disabling"></a>

You can disable home folders for a stack without losing user content already stored in home folders\. Disabling home folders for a stack has the following effects:
+ Users who are connected to active streaming sessions for the stack receive an error message\. They are informed that they can no longer store content in their home folder\. 
+ Home folders do not appear for any new sessions that use the stack with home folders disabled\. 
+ Disabling home folders for one stack does not disable it for other stacks\. 
+ Even if home folders are disabled for all stacks, AppStream 2\.0 does not delete the user content\.

To restore access to home folders for the stack, enable home folders again by following the steps described earlier in this topic\. 

**To disable home folders while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install) and make sure that the **Enable Home Folders** option is cleared\.

**To disable home folders for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack\.

1. Below the stacks list, choose **Storage** and clear **Enable Home Folders**\.

1. In the **Disable Home Folders** dialog box, type `CONFIRM` \(case\-sensitive\) to confirm your choice, then choose **Disable**\.

### Amazon S3 Bucket Storage<a name="home-folders-s3"></a>

AppStream 2\.0 manages user content stored in home folders by using Amazon S3 buckets created in your account\. For every AWS Region, AppStream 2\.0 creates a bucket in your account\. All user content generated from streaming sessions of stacks in that Region is stored in that bucket\. The buckets are fully managed by the service without any input or configuration from an administrator\. The buckets are named in a specific format as follows: 

```
appstream2-36fb080bb8-region-code-account-id-without-hyphens
```

Where `region-code` is the AWS Region code in which the stack is created and `account-id-without-hyphens` is your AWS account ID\. The first part of the bucket name, `appstream2-36fb080bb8-`, does not change across accounts or Regions\. 

For example, if you enable home folders for stacks in the US West \(Oregon\) Region \(us\-west\-2\) on account number 123456789012, the service creates an Amazon S3 bucket in that Region with the name shown\. Only an administrator with sufficient permissions can delete this bucket\.

```
appstream2-36fb080bb8-us-west-2-123456789012
```

As mentioned earlier, disabling home folders for stacks does not delete any user content stored in the Amazon S3 bucket\. To permanently delete user content, an administrator with adequate access must do so from the Amazon S3 console\. AppStream 2\.0 adds a bucket policy that prevents accidental deletion of the bucket\. For more information, see [Using IAM Policies to Manage Administrator Access to the Amazon S3 Bucket for Home Folders and Application Settings Persistence](s3-iam-policy.md)\. 

### Home Folder Content Synchronization<a name="home-folders-content-synchronization"></a>

When home folders are enabled, AppStream 2\.0 creates a unique folder for each user in which to store their content\. The folder is created as a unique Amazon S3 prefix that uses a hash of the user name within an S3 bucket for your AWS account and Region\. After AppStream 2\.0 creates the home folder in Amazon S3, it copies the accessed content in that folder from the S3 bucket to the fleet instance\. This enables the user to access their home folder content quickly, from the fleet instance, during their streaming session\. Changes that you make to a user’s home folder content in an S3 bucket and that the user makes to their home folder content on a fleet instance are synchronized between Amazon S3 and AppStream 2\.0 as follows\. 

1. At the beginning of a user’s AppStream 2\.0 streaming session, AppStream 2\.0 catalogs the home folder files that are stored for that user in the Amazon S3 bucket for your AWS account and Region\. 

1. A user’s home folder content is also stored on the AppStream 2\.0 fleet instance from which they stream\. When a user accesses their home folder on the AppStream 2\.0 fleet instance, the list of cataloged files is displayed\. 

1. AppStream 2\.0 downloads a file from the S3 bucket to the fleet instance only after the user uses a streaming application to open the file during their streaming session\.

1. After AppStream 2\.0 downloads the file to the fleet instance, synchronization occurs after the file is accessed 

1. If the user changes the file during their streaming session, AppStream 2\.0 uploads the new version of the file from the fleet instance to the S3 bucket every periodically or at the end of the streaming session\. However, the file is not downloaded from the S3 bucket again during the streaming session\.

The following sections describe synchronization behavior when you add, replace, or remove a user's home folder file in Amazon S3\.

**Topics**
+ [Synchronization of files that you add to a user’s home folder in Amazon S3](#home-folders-content-synchronization-content-added-to-user-home-folder-in-S3)
+ [Synchronization of files that you replace in a user’s home folder in Amazon S3](#home-folders-content-synchronization-content-replaced-in-user-home-folder-S3)
+ [Synchronization of files that you remove from a user’s home folder in Amazon S3](#home-folders-content-synchronization-content-removed-from-user-home-folder-S3)

#### Synchronization of files that you add to a user’s home folder in Amazon S3<a name="home-folders-content-synchronization-content-added-to-user-home-folder-in-S3"></a>

If you add a new file to a user’s home folder in an S3 bucket, AppStream 2\.0 catalogs the file and displays it in the list of files in the user’s home folder within a few minutes\. However, the file isn’t downloaded from the S3 bucket to the fleet instance until the user opens the file with an application during their streaming session\.

#### Synchronization of files that you replace in a user’s home folder in Amazon S3<a name="home-folders-content-synchronization-content-replaced-in-user-home-folder-S3"></a>

If a user opens a file in their home folder on the fleet instance during their streaming session, and you replace the same file in their home folder in an S3 bucket with a new version during that user’s active streaming session, the new version of the file is not immediately downloaded to the fleet instance\. The new version is downloaded from the S3 bucket to the fleet instance only after the user starts a new streaming session and opens the file again\. 

#### Synchronization of files that you remove from a user’s home folder in Amazon S3<a name="home-folders-content-synchronization-content-removed-from-user-home-folder-S3"></a>

If a user opens a file in their home folder on the fleet instance during their streaming session, and you remove the file from their home folder in an S3 bucket during that user’s active streaming session, the file is removed from the fleet instance after the user does either of the following: 
+ Opens the home folder again
+ Refreshes the home folder

### Home Folder Formats<a name="home-folders-admin-folders"></a>

The hierarchy of a user folder depends on how a user launches a streaming session, as described in the following sections\.

#### AWS SDKs and AWS CLI<a name="home-folders-admin-folders-aws"></a>

For sessions launched using `CreateStreamingURL` or `create-streaming-url` the user folder structure is as follows:

```
bucket-name/user/custom/user-id-SHA-256-hash/
```

Where `bucket-name` is in the format shown in [Amazon S3 Bucket Storage](#home-folders-s3) and `user-id-SHA-256-hash` is the user\-specific folder name created using a lowercase SHA\-256 hash hexadecimal string generated from the `UserId` value passed to the CreateStreamingURL API operation or `create-streaming-url` command\. For more information, see [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) in the *Amazon AppStream 2\.0 API Reference* and [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) in the *AWS CLI Command Reference*\.

The following example folder structure applies to session access using the API or AWS CLI with a `UserId` testuser@mydomain\.com, account id 123456789012 in the US West \(Oregon\) Region \(us\-west\-2\):

```
appstream2-36fb080bb8-us-west-2-123456789012/user/custom/a0bcb1da11f480d9b5b3e90f91243143eac04cfccfbdc777e740fab628a1cd13/
```

You can identify the folder for a user by generating the lowercase SHA\-256 hash value of the `UserId` using websites or open source coding libraries available online\.

#### SAML 2\.0<a name="home-folders-admin-folders-saml"></a>

For sessions created using SAML federation, the user folder structure is as follows:

```
bucket-name/user/federated/user-id-SHA-256-hash/
```

In this case, `user-id-SHA-256-hash` is the folder name created using a lowercase SHA\-256 hash hexadecimal string generated from the `NameID` SAML attribute value passed in the SAML federation request\. To differentiate users who have the same name but belong to two different domains, send the SAML request with `NameID` in the format `domainname\username`\. For more information, see [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md)\.

The following example folder structure applies to session access using SAML federation with `NameID` SAMPLEDOMAIN\\testuser, account ID 123456789012 in the US West \(Oregon\) Region:

```
appstream2-36fb080bb8-us-west-2-123456789012/user/federated/8dd9a642f511609454d344d53cb861a71190e44fed2B8aF9fde0C507012a9901
```

When part or all of the NameID string is capitalized \(as the domain name *SAMPLEDOMAIN* is in the example\), AppStream 2\.0 generates the hash value based on the capitalization used in the string\. Using this example, the hash value for SAMPLEDOMAIN\\testuser is 8DD9A642F511609454D344D53CB861A71190E44FED2B8AF9FDE0C507012A9901\. In the folder for that user, this value is displayed in lowercase, as follows: 8dd9a642f511609454d344d53cb861a71190e44fed2B8aF9fde0C507012a9901\. 

You can identify the folder for a user by generating the SHA\-256 hash value of the `NameID` using websites or open source coding libraries available online\.

### Using the AWS Command Line Interface or AWS SDKs<a name="home-folders-admin-cli"></a>

You can enable and disable home folders for a stack by using the AWS CLI or AWS SDKs\.

Use the following [create\-stack](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-stack.html) command to enable home folders while creating a new stack:

```
aws appstream create-stack --name ExampleStack –-storage-connectors type=HOMEFOLDERS
```

Use the following [update\-stack](https://docs.aws.amazon.com/cli/latest/reference/appstream/update-stack.html) command to enable home folders for an existing stack:

```
aws appstream update-stack –-name ExistingStack –-storage-connectors type=HOMEFOLDERS
```

Use the following command to disable home folders for an existing stack\. This command does not delete any user data\.

```
aws appstream update-stack –name ExistingStack –-delete-storage-connectors
```

### Additional Resources<a name="home-folders-admin-additional"></a>

For more information about managing Amazon S3 buckets and best practices, see the following topics in the *Amazon Simple Storage Service Developer Guide*: 
+ You can provide offline access to user data for your users with Amazon S3 policies\. For more information, see [Amazon S3: Allows IAM Users Access to Their S3 Home Directory, Programmatically and In the Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_examples_s3_home-directory-console.html) in the *IAM User Guide*\.
+ You can enable file versioning for content stored in Amazon S3 buckets used by AppStream 2\.0\. For more information, see [Using Versioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html)\.