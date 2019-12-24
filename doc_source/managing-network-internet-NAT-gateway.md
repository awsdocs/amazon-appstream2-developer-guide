# Configure a VPC with Private Subnets and a NAT Gateway<a name="managing-network-internet-NAT-gateway"></a>

If you plan to provide your streaming instances \(fleet instances and image builders\) with access to the internet, we recommend that you configure a VPC with two private subnets for your streaming instances and a NAT gateway in a public subnet\. You can create and configure a new VPC to use with a NAT gateway, or add a NAT gateway to an existing VPC\. For additional VPC configuration recommendations, see [VPC Setup Recommendations](vpc-setup-recommendations.md)\.

The NAT gateway lets the streaming instances in your private subnets connect to the internet or other AWS services, but prevents the internet from initiating a connection with those instances\. In addition, unlike configurations that use the **Default Internet Access** option for enabling internet access for AppStream 2\.0 streaming instances, this configuration is not limited to 100 fleet instances\.

For information about using NAT Gateways and this configuration, see [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) and [VPC with Public and Private Subnets \(NAT\)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html) in the *Amazon VPC User Guide*\.

**Topics**
+ [Create and Configure a New VPC](create-configure-new-vpc-with-private-public-subnets-nat.md)
+ [Add a NAT Gateway to an Existing VPC](add-nat-gateway-existing-vpc.md)
+ [Enable Internet Access for Your Fleet and Image Builder](managing-network-manual-enable-internet-access.md)