# AWS Managed Policies Required to Access AppStream 2\.0 Resources<a name="managed-policies-required-to-access-appstream-resources"></a>

To provide full administrative or read\-only access to AppStream 2\.0, you must attach one of the following AWS managed policies to the IAM users or groups that require those permissions\. An *AWS managed policy* is a standalone policy that is created and administered by AWS\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

**AmazonAppStreamFullAccess**  
This managed policy provides full administrative access to AppStream 2\.0 resources\. To manage AppStream 2\.0 resources and perform API actions through the AWS Command Line Interface \(AWS CLI\), AWS SDK, or AWS Management Console, you must have the permissions defined in this policy\.  
If you sign into the AppStream 2\.0 console as an IAM user, you must attach this policy to your IAM user account\. If you sign in through console federation, you must attach this policy to the IAM role that was used for federation\.

**AmazonAppStreamReadOnlyAccess**  
This managed policy provides read\-only access to AppStream 2\.0 resources\.

The AppStream 2\.0 console uses two additional actions that provide functionality that is not available through the AWS CLI or AWS SDK\. The **AmazonAppStreamFullAccess** and **AmazonAppStreamReadOnlyAccess** policies both provide permissions for these actions\.


| Action | Description | Access Level | 
| --- | --- | --- | 
| GetImageBuilders | Grants permission to retrieve a list that describes one or more specified image builders, if the image builder names are provided\. Otherwise, all image builders in the account are described\. | Read | 
| GetParametersForThemeAssetUpload | Grants permission to upload theme assets for custom branding\. For more information, see [Add Your Custom Branding to Amazon AppStream 2\.0](branding.md)\. | Write | 