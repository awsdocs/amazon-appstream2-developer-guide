# Amazon AppStream 2\.0 Service Quotas<a name="limits"></a>

By default, AWS sets quotas \(also referred to as limits\) for the resources that you can create and the number of users who can use the service\. To request a quota increase, use the [AppStream 2\.0 Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-appstream2)\.

The following table lists the quotas for each AppStream 2\.0 resource\. Where no default quota is listed for a specific [instance family](instance-types.md) or instance type, the quota is 0\. To determine which instance types are available in which Regions or Availability Zones, see *Pricing by AWS Region – Always\-On, On\-Demand, and image builder instances* in [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.


**Default Quotas Per AWS Region Per Account**  

| Resource | Default Quota | 
| --- | --- | 
| Stacks | 10 | 
| Fleets | 10 | 
| Fleet instances\* |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/limits.html)  | 
| Image builder instances  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/limits.html)  | 
| Image builders \(total\) | 10 | 
| Images | 10 | 
| Number of AWS accounts an image can be shared with | 100 | 
| Concurrent image copies | 2 per destination Region | 
| Image copies \(per month\) | 20 | 
| Users in the user pool | 50 | 

\*For fleets that have **Default Internet Access** enabled, the quota is 100 fleet instances\. If your deployment must support more than 100 concurrent users, use the [NAT gateway configuration](managing-network-internet-NAT-gateway.md) instead\. For more information about enabling internet access for a fleet, see [Internet Access](internet-access.md)\.