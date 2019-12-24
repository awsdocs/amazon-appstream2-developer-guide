# Internet Access<a name="internet-access"></a>

If your fleets and image builders require internet access, enable internet access by doing one of the following:
+ [Configure a VPC with Private Subnets and a NAT Gateway](managing-network-internet-NAT-gateway.md) \(recommended\) — With this configuration, you launch your fleets and image builders in a private subnet and configure a NAT gateway in a public subnet in your VPC\. Your streaming instances are assigned a private IP address that is not directly accessible from the internet\. 

  In addition, unlike configurations that use the **Default Internet Access** option for enabling internet access, the NAT configuration is not limited to 100 fleet instances\. If your deployment must support more than 100 concurrent users, use this configuration\.

  You can create and configure a new VPC to use with a NAT gateway, or add a NAT gateway to an existing VPC\. 
+ [Configure a New or Existing VPC with a Public Subnet](managing-network-default-internet-access.md) — With this configuration, you launch your fleets and image builders in a public subnet and enable **Default Internet Access**\. When you enable this option, AppStream 2\.0 uses the internet gateway in your Amazon VPC public subnet to provide the internet connection\. Your streaming instances are assigned a public IP address that is directly accessible from the internet\. You can create a new VPC or configure an existing one for this purpose\.
**Note**  
When **Default Internet Access** is enabled, a maximum of 100 fleet instances is supported\. If your deployment must support more than 100 concurrent users, use the [NAT gateway configuration](managing-network-internet-NAT-gateway.md) instead\.
+ [Use the Default VPC, Public Subnet, and Security Group](default-vpc-with-public-subnet.md) — If you are new to AppStream 2\.0 and want to get started using the service, you can launch your fleets and image builders in a default public subnet and enable **Default Internet Access**\. When you enable this option, AppStream 2\.0 uses the internet gateway in your Amazon VPC public subnet to provide the internet connection\. Your streaming instances are assigned a public IP address that is directly accessible from the internet\.

  Default VPCs are available in AWS accounts created after 2013\-12\-04\. 
**Note**  
When **Default Internet Access** is enabled, a maximum of 100 fleet instances is supported\. If your deployment must support more than 100 concurrent users, use the [NAT gateway configuration](managing-network-internet-NAT-gateway.md) instead\.