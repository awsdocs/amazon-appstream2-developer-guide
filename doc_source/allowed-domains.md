# Allowed Domains<a name="allowed-domains"></a>

For AppStream 2\.0 users to access streaming instances, you must allow the following domain on the network from which users initiate access to the streaming instances\.
+ Session Gateway: \*\.amazonappstream\.com

One or more of the following domains must be allowed to enable user authentication\. You must allow the domains that correspond to the Regions where AppStream 2\.0 is deployed\. 


| Region | Domain | 
| --- | --- | 
| US East \(N\. Virginia\) | appstream2\.us\-east\-1\.aws\.amazon\.com | 
| US West \(Oregon\) | appstream2\.us\-west\-2\.aws\.amazon\.com | 
| Asia Pacific \(Mumbai\) | appstream2\.ap\-south\-1\.aws\.amazon\.com | 
| Asia Pacific \(Seoul\) | appstream2\.ap\-northeast\-2\.aws\.amazon\.com | 
| Asia Pacific \(Singapore\) | appstream2\.ap\-southeast\-1\.aws\.amazon\.com | 
| Asia Pacific \(Sydney\) | appstream2\.ap\-southeast\-2\.aws\.amazon\.com | 
| Asia Pacific \(Tokyo\) | appstream2\.ap\-northeast\-1\.aws\.amazon\.com | 
| Europe \(Frankfurt\) | appstream2\.eu\-central\-1\.aws\.amazon\.com | 
| Europe \(Ireland\) | appstream2\.eu\-west\-1\.aws\.amazon\.com | 
| AWS GovCloud \(US\-West\) | appstream2\.us\-gov\-west\-2\.amazonaws\-us\-gov\.com | 

**Note**  
If your users use a network proxy to access streaming instances, disable any proxy caching for the user auth domains in the table and the session gateway, \*\.amazonappstream\.com\.

Amazon Web Services \(AWS\) publishes its current IP address ranges, including the ranges that the Session Gateway and CloudFront domains may resolve to, in JSON format\. For information about how to download the \.json file and view the current ranges, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the Amazon Web Services General Reference\. Or, if you are using AWS Tools for Windows PowerShell, you can access the same information by using the `Get-AWSPublicIpAddressRange` cmdlet\. For more information, see [Querying the Public IP Address Ranges for AWS](https://aws.amazon.com/blogs/developer/querying-the-public-ip-address-ranges-for-aws/)\.