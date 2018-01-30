# General Troubleshooting<a name="troubleshooting-general"></a>

The following are possible general issues you might have while using Amazon AppStream 2\.0\.


+ [SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.](#troubleshooting-13)
+ [After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.](#troubleshooting-adfs-upn)
+ [I get an invalid redirect URI error\.](#troubleshooting-14)
+ [My stack's Home Folders aren't working correctly\.](#troubleshooting-s3-failures)

## SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.<a name="troubleshooting-13"></a>

This may happen because the policy of the IAM role, which is assumed by the federated user who is accessing an AppStream 2\.0 stack, does not include permissions to the stack ARN\. Edit the role permissions to include the stack ARN\. For more information, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md) and [Troubleshooting SAML 2\.0 Federation with AWS](http://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_saml.html) in the *IAM User Guide*\.

## After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.<a name="troubleshooting-adfs-upn"></a>

Set the claim rule's **Incoming Claim Type** for the **NameID** SAML attribute to **UPN** and try the connection again\.

## I get an invalid redirect URI error\.<a name="troubleshooting-14"></a>

This error happens due to a malformed or invalid AppStream 2\.0 stack relay state URL\. Make sure that the relay state configured in your federation setup is the same as the stack relay state available in stack details through the AppStream 2\.0 console\. If they are the same and the problem still persists, contact AWS Support\. For more information, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\.

## My stack's Home Folders aren't working correctly\.<a name="troubleshooting-s3-failures"></a>

Home Folder backup to the S3 bucket can have problems under the following scenarios:

+ There is no internet connectivity from the streaming instance, or there is no access to the private Amazon S3 VPC endpoint, if applicable\.

+ Network bandwidth consumption is too high\. For example, multiple large files being downloaded or streamed by the user while the service is trying to back up the Home Folder containing large files to Amazon S3\.

+ The administrator deleted the bucket created by the service\.

+ The administrator incorrectly edited the Amazon S3 permissions of the **AmazonAppStreamServiceAccess** service role\.

For more information, see the [Amazon Simple Storage Service Console User Guide](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/) and [Amazon Simple Storage Service Developer Guide](http://docs.aws.amazon.com/AmazonS3/latest/dev/)\.