# User Connections to Amazon AppStream 2\.0<a name="user-connections-to-appstream2"></a>

Users can connect to AppStream 2\.0 streaming instances through the default public internet endpoint, or by using an [interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) \(interface endpoint\) that you create in your virtual private cloud \(VPC\)\. After you create this endpoint, you configure your AppStream 2\.0 stack or image builder to use it\. The interface endpoint lets you keep streaming traffic within your VPC\. When you use this endpoint with an AWS Direct Connect or AWS Virtual Private Network \(VPN\) tunnel, you can keep the streaming traffic within your network\.

By default, AppStream 2\.0 is configured to route streaming connections over the public internet\. Internet connectivity is required to authenticate users and deliver the web assets that AppStream 2\.0 requires to function\. To allow this traffic, you must whitelist the domains listed in [Whitelisted Domains](whitelisted_ports.md)\.

The following topics provide information about how to enable user connections to AppStream 2\.0, including bandwidth recommendations, required ports and domains, and how to create and stream from interface endpoints\.

**Topics**
+ [Bandwidth Recommendations](bandwidth-recommendations-user-connections.md)
+ [Ports for AppStream 2\.0 User Devices](client-application-ports.md)
+ [Whitelisted Domains](whitelisted_ports.md)
+ [Creating and Streaming From Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)