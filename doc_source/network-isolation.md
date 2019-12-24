# Network Isolation<a name="network-isolation"></a>

A virtual private cloud \(VPC\) is a virtual network in your own logically isolated area in the AWS Cloud\. Use separate VPCs to isolate infrastructure by workload or organizational entity\.

A subnet is a range of IP addresses in a VPC\. When you launch an instance, you launch it into a subnet in your VPC\. Use subnets to isolate the tiers of your application \(for example, web, application, and database\) within a single VPC\. Use private subnets for your instances if they should not be accessed directly from the internet\.

You can stream from AppStream 2\.0 streaming instances in your VPC without going through the public internet\. To do so, use an interface VPC endpoint \(interface endpoint\)\. For more information, see [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)\.

You can also call AppStream 2\.0 API operations from your VPC without sending traffic over the public internet by using an interface endpoint\. For information, see [Access AppStream 2\.0 API Operations and CLI Commands Through an Interface VPC Endpoint](access-api-cli-through-interface-vpc-endpoint.md)\.