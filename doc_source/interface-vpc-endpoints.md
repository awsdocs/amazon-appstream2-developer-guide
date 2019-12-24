# AppStream 2\.0 Interface VPC Endpoints<a name="interface-vpc-endpoints"></a>

A virtual private cloud \(VPC\) is a virtual network in your own logically isolated area in the AWS Cloud\. If you use Amazon Virtual Private Cloud to host your AWS resources, you can establish a private connection between your VPC and AppStream 2\.0\. You can use this connection to enable AppStream 2\.0 to communicate with your resources on your VPC without going through the public internet\.

Interface endpoints are powered by AWS PrivateLink, a technology that lets you keep streaming traffic within a VPC that you specify by using private IP addresses\. When you use the VPC with an AWS Direct Connect or AWS Virtual Private Network \(VPN\) tunnel, you can keep the streaming traffic within your network\. 

The following topics provide information about AppStream 2\.0 interface endpoints\.

**Topics**
+ [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)
+ [Access AppStream 2\.0 API Operations and CLI Commands Through an Interface VPC Endpoint](access-api-cli-through-interface-vpc-endpoint.md)