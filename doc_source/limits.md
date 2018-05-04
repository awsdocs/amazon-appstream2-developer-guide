# Amazon AppStream 2\.0 Service Limits<a name="limits"></a>

By default, AWS limits the resources you can create and the number of users that can use the service\. To request a limit increase, use the [AppStream 2\.0 Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-appstream2)\.

The following table lists the limits for each AppStream 2\.0 resource\.


**Default Limits Per Region Per Account**  

| Resource | Default Limit | 
| --- | --- | 
| Stacks | 5 | 
| Fleets | 5 | 
| Streaming instances | 5 \* | 
| Images | 5 | 
| Image builders | 5 \*\* | 
| Concurrent image copies | 2 \*\*\* | 
| Image copies \(per month\) | 20 | 

**\*** This is the total limit across all instance families\. Certain instance families have additional limits\. For the Graphics Desktop and Graphics Pro [instance families](instance-types.md), the default limit is 0\. For the Graphics Design instance family, the default limit is 2\.

**\*\*** This is the total limit across all instance families\. Certain instance families have additional limits\. For the Graphics Desktop and Graphics Pro [instance families](instance-types.md), the default limit is 0\. For the Graphics Design instance family, the default limit is 1\.

**\*\*\*** This is the limit for the number of images that you can copy at the same time to a destination\.