# General Troubleshooting<a name="troubleshooting-general"></a>

The following are possible general issues you might have while using Amazon AppStream 2\.0\.

**Topics**
+ [SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.](#troubleshooting-13)
+ [After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.](#troubleshooting-adfs-upn)
+ [I get an invalid redirect URI error\.](#troubleshooting-14)
+ [My stack's Home Folders aren't working correctly\.](#troubleshooting-s3-failures)
+ [My users can't access their Home Folder directory from one of our applications\.](#alternate-path-accessing-home-folders)

## SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.<a name="troubleshooting-13"></a>

This might happen because the inline policy that is embedded for the SAML 2\.0 federation IAM role does not include permissions to the stack ARN\. The IAM role is assumed by the federated user who is accessing an AppStream 2\.0 stack\. Edit the role permissions to include the stack ARN\. For more information, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md) and [Troubleshooting SAML 2\.0 Federation with AWS](http://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_saml.html) in the *IAM User Guide*\.

## After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.<a name="troubleshooting-adfs-upn"></a>

Set the claim rule's **Incoming Claim Type** for the **NameID** SAML attribute to **UPN** and try the connection again\.

## I get an invalid redirect URI error\.<a name="troubleshooting-14"></a>

This error occurs due to a malformed or invalid AppStream 2\.0 stack relay state URL\. Make sure that the relay state configured in your federation setup is the same as the stack relay state that is displayed in the stack details through the AppStream 2\.0 console\. If they are the same and the problem still persists, contact AWS Support\. For more information, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\.

## My stack's Home Folders aren't working correctly\.<a name="troubleshooting-s3-failures"></a>

Problems with Home Folder backup to an S3 bucket can occur in the following scenarios:
+ There is no internet connectivity from the streaming instance, or there is no access to the private Amazon S3 VPC endpoint, if applicable\.
+ Network bandwidth consumption is too high\. For example, multiple large files are being downloaded or streamed by the user while the service is trying to back up a Home Folder that contains large files to Amazon S3\.
+ An administrator deleted the bucket created by the service\.
+ An administrator incorrectly edited the Amazon S3 permissions for the **AmazonAppStreamServiceAccess** service role\.

For more information, see the [Amazon Simple Storage Service Console User Guide](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/) and [Amazon Simple Storage Service Developer Guide](http://docs.aws.amazon.com/AmazonS3/latest/dev/)\.

## My users can't access their Home Folder directory from one of our applications\.<a name="alternate-path-accessing-home-folders"></a>

Some applications do not recognize the redirect that displays the Home Folder as a top\-level folder in File Explorer\. If this is the case, your users can access their Home Folder when they are working in an application during a streaming session by choosing **File Open** from the application interface and browsing to the following directory: C:\\Users\\PhotonUser\\My Files\\Home Folder\.