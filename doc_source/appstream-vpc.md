# Configure a VPC for AppStream 2\.0<a name="appstream-vpc"></a>

When you set up AppStream 2\.0, you must specify the virtual private cloud \(VPC\) and at least one subnet in which to launch your fleet instances and image builders\. A VPC is a virtual network in your own logically isolated area within the AWS cloud\. A subnet is a range of IP addresses in your VPC\.

When you configure your VPC for AppStream 2\.0, you can specify either public or private subnets, or a mix of both types of subnets\. A public subnet has direct access to the internet through an internet gateway\. A private subnet, which doesn't have a route to an internet gateway, requires a Network Address Translation \(NAT\) gateway or NAT instance to provide access to the internet\.

**Topics**
+ [VPC Setup Recommendations](vpc-setup-recommendations.md)
+ [Configure a VPC with Private Subnets and a NAT Gateway](managing-network-internet-NAT-gateway.md)
+ [Configure a New or Existing VPC with a Public Subnet](managing-network-default-internet-access.md)
+ [Use the Default VPC, Public Subnet, and Security Group](default-vpc-with-public-subnet.md)