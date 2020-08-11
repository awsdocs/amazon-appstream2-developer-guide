# Administer the VHDs for Your Users' Application Settings<a name="administer-app-settings-vhds"></a>

**Topics**
+ [Amazon S3 Bucket Storage](#app-persistence-s3-buckets)
+ [Reset a User's Application Settings](#app-persistence-s3-reset)
+ [Enable Amazon S3 Object Versioning and Revert a User's Application Settings](#app-persistence-enable-versions-revert-settings)
+ [Increase the Size of the Application Settings VHD](#app-persistence-increase-VHD-size)

## Amazon S3 Bucket Storage<a name="app-persistence-s3-buckets"></a>

When you enable application settings persistence, your users’ application customizations and Windows settings are automatically saved to a Virtual Hard Disk \(VHD\) file that is stored in an Amazon S3 bucket created in your AWS account\. For every AWS Region, AppStream 2\.0 creates a bucket in your account that is unique to your account and the Region\. All application settings configured by your users are stored in the bucket for that Region\.

You do not need to perform any configuration tasks to manage these S3 buckets; they are fully managed by the AppStream 2\.0 service\. The VHD file that is stored in each bucket is encrypted in transit using Amazon S3's SSL endpoints and at rest using [AWS Managed CMKs](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#aws-managed-cmk)\. The buckets are named in a specific format as follows:

```
appstream-app-settings-region-code-account-id-without-hyphens-random-identifier
```

***region\-code***  
This is the AWS Region code in which the stack is created with application settings persistence\.

***account\-id\-without\-hyphens***  
Your AWS account ID\. The random identifier ensures there is no conflict with other buckets in that Region\. The first part of the bucket name, `appstream-app-settings`, does not change across accounts or Regions\.

For example, if you enable application settings persistence for stacks in the US West \(Oregon\) Region \(us\-west\-2\) on account number 123456789012, AppStream 2\.0 creates an Amazon S3 bucket within your account in that Region with the name shown\. Only an administrator with sufficient permissions can delete this bucket\.

```
appstream-app-settings-us-west-2-1234567890123-abcdefg
```

Disabling application settings persistence does not delete any VHDs stored in the S3 bucket\. To permanently delete settings VHDs, you or another administrator with adequate permissions must do so by using the Amazon S3 console or API\. AppStream 2\.0 adds a bucket policy that prevents accidental deletion of the bucket\. For more information, see *IAM Policies and the Amazon S3 Bucket for Application Settings Persistence* in [Identity and Access Management for Amazon AppStream 2\.0](controlling-access.md)\.

When application settings persistence is enabled, a unique folder is created for each settings group to store the settings VHD\. The hierarchy of the folder in the S3 bucket depends on how the user launches a streaming session, as described in the following section\.

 The path for the folder where the settings VHD is stored in the S3 bucket in your account uses the following structure:

```
bucket-name/Windows/v4/settings-group/access-mode/user-id-SHA-256-hash
```

***bucket\-name***  
The name of the S3 bucket in which users' application settings are stored\. The name format is described earlier in this section\.

***settings\-group ***  
The settings group value\. This value is applied to one or more stacks that share the same the same application settings\.

***access\-mode***  
The identity method of the user: `custom` for the AppStream 2\.0 API or CLI, `federated` for SAML, and `userpool` for user pool users\.

***user\-id\-SHA\-256\-hash***  
The user\-specific folder name\. This name is created using a lowercase SHA\-256 hash hexadecimal string generated from the user ID\.

The following example folder structure applies to a streaming session that is accessed using the API or CLI with a user ID of `testuser@mydomain.com`, an AWS account ID of `123456789012`, and the settings group `test-stack` in the US West \(Oregon\) Region \(us\-west\-2\):

```
appstream-app-settings-us-west-2-1234567890123-abcdefg/Windows/v2/test-stack/custom/a0bcb1da11f480d9b5b3e90f91243143eac04cfccfbdc777e740fab628a1cd13
```

You can identify the folder for a user by generating the lowercase SHA\-256 hash value of the user ID using websites or open source coding libraries available online\.

## Reset a User's Application Settings<a name="app-persistence-s3-reset"></a>

To reset a user's application settings, you must find and delete the VHD and associated metadata file from the S3 bucket in your AWS account\. Make sure that you do not do this during a user's active streaming session\. After you delete the user's VHD and the metadata file, the next time the user launches a session from a streaming instance that has application settings persistence enabled, AppStream 2\.0 creates a new settings VHD for that user\.

**To reset a user's application settings**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name** list, choose the S3 bucket that contains the application settings VHD that you want to reset\.

1. Locate the folder that contains the VHD\. For more information about how to navigate the S3 bucket folder structure, see *Amazon S3 Bucket Storage* earlier in this topic\.

1. In the **Name** list, select the check box next to the VHD and the REG, choose **More**, and then choose **Delete**\.

1. In the **Delete objects** dialog box, verify that the VHD and the REG are listed, and then choose **Delete**\. 

The next time the user streams from a fleet on which application settings persistence is enabled with the applicable settings group, a new application settings VHD is created\. This VHD is saved to the S3 bucket at the end of the session\.

## Enable Amazon S3 Object Versioning and Revert a User's Application Settings<a name="app-persistence-enable-versions-revert-settings"></a>

You can use Amazon S3 object versioning and lifecycle policies to manage your users’ application settings when your users change them\. With Amazon S3 object versioning, you can preserve, retrieve, and restore every version of the settings VHD\. This enables you to recover from both unintended user actions and application failures\. When versioning is enabled, after each streaming session, a new version of the application settings VHD is synced to Amazon S3\. The new version does not overwrite the previous version, so if an issue with your users' settings occurs, you can revert to a previous version of the VHD\.

**Note**  
Each version of the application settings VHD is saved to Amazon S3 as a separate object and is charged accordingly\.

Object versioning is not enabled by default in your S3 bucket, so you must explicitly enable it\. 

**To enable object versioning for your application settings VHD**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name **list, choose the S3 bucket that contains the application settings VHD on which to enable object versioning\.

1. Choose **Properties**\.

1. Choose **Versioning**, **Enable versioning**, and then choose **Save**\.

To expire older versions of your application settings VHDs, you can use Amazon S3 lifecycle policies\. For information, see [How Do I Create a Lifecycle Policy for an S3 Bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-lifecycle.html) in the *Amazon Simple Storage Service Console User Guide*\.

**To revert a user's application settings VHD**

You can revert to a previous version of a user's application settings VHD by deleting newer versions of the VHD from the applicable S3 bucket\. Do not do this when the user has an active streaming session\.

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name** list, choose the S3 bucket that contains the user's application settings VHD version to revert to\.

1. Locate and select the folder that contains the VHD\. For information about how to navigate the S3 bucket folder structure, see *Amazon S3 Bucket Storage* earlier in this topic\.

   When you select the folder, the settings VHD and associated metadata file display\.

1. To display a list of the VHD and metadata file versions, choose **Show**\.

1. Locate the version of the VHD to revert to\.

1. In the **Name** list, select the check boxes next to the newer versions of the VHD and associated metadata files, choose **More**, and then choose **Delete**\.

1. Verify that the application settings VHD that you want to revert to and the associated metadata file are the newest versions of these files\. 

The next time the user streams from a fleet on which application settings persistence is enabled with the applicable settings group, the reverted version of the user's settings displays\.

## Increase the Size of the Application Settings VHD<a name="app-persistence-increase-VHD-size"></a>

The default VHD maximum size is 1 GB\. If a user requires additional space for application settings, you can download the applicable application settings VHD to a Windows computer to expand it\. Then, replace the current VHD in the S3 bucket with the larger one\. Do not do this when the user has an active streaming session\. 

**To increase the size of the application settings VHD**
**Note**  
The full VHD must be downloaded before a user can stream applications\. Increasing the size of an application settings VHD can increase the time it takes for users to start application streaming sessions\.

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name** list, choose the S3 bucket that contains the application settings VHD to expand\.

1. Locate and select the folder that contains the VHD\. For information about how to navigate the S3 bucket folder structure, see *Amazon S3 Bucket Storage* earlier in this topic\.

   When you select the folder, the settings VHD and associated metadata file display\.

1. Download the Profile\.vhdx file to a directory on your Windows computer\. Do not close your browser after the download completes, because you'll use the browser again later to upload the expanded VHD\.

1. To use Diskpart to increase the size of the VHD to 2 GB, open the command prompt as an administrator, and type the following commands\.

   `diskpart`

   `select vdisk file="C:\path\to\application\settings\profile.vhdx"`

   `expand vdisk maximum=2000`

1. Then, type the following Diskpart commands to find and attach the VHD, and display the list of volumes:

   `select vdisk file="C:\path\to\application\settings\profile.vhdx"`

   `attach vdisk`

   `list volume`

   In the output, make note of the volume number with the label "AppStreamUS"\. In the next step, you select this volume so that you can enlarge it\.

1. Type the following command:

   `select volume ###`

   where \#\#\# is the number in the list volume output\.

1. Type the following command:

   `extend`

1. Type the following commands to confirm that the size of the partition on the VHD increased as expected \(2 GB in this example\):

   `diskpart`

   `select vdisk file="C:\path\to\application\settings\profile.vhdx"`

   `list volume`

1. Type the following command to detach the VHD so that it can be uploaded:

   `detach vdisk`

1. Return to your browser with the Amazon S3 console, choose **Upload**, **Add files**, and then select the enlarged VHD\. 

1. Choose **Upload**\.

After the VHD is uploaded, the next time the user streams from a fleet on which application settings persistence is enabled with the applicable settings group, the larger application settings VHD is available\.