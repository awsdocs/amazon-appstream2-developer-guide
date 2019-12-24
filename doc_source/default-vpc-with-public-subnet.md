# Use the Default VPC, Public Subnet, and Security Group<a name="default-vpc-with-public-subnet"></a>

Your AWS account, if it was created after 2013\-12\-04, has a default VPC in each AWS Region\. The default VPC includes a default public subnet in each Availability Zone and an internet gateway that is attached to your VPC\. The VPC also includes a default security group\. If you are new to AppStream 2\.0 and want to get started using the service, you can keep the default VPC and security group selected when you create a fleet or launch an image builder\. Then, you can select at least one default subnet\.

**Note**  
If your AWS account was created before 2013\-12\-04, you must create a new VPC or configure an existing one to use with AppStream 2\.0\. We recommend that you manually configure a VPC with two private subnets for your fleets and image builders and a NAT gateway in a public subnet\. For more information, see [Configure a VPC with Private Subnets and a NAT Gateway](managing-network-internet-NAT-gateway.md)\. Alternatively, you can configure a non\-default VPC with a public subnet\. For more information, see [Configure a New or Existing VPC with a Public Subnet](managing-network-default-internet-access.md)\.

**To use the default VPC, subnet, and security group for a fleet**

1. Complete the steps in [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create) up to **Step 4: Configure Network**\.

1. In **Step 4: Configure Network**, do the following:
   + To enable your fleet instances to access the internet, select the **Default Internet Access** check box\.
**Note**  
For fleet instances that have the **Default Internet Access** option enabled, the limit is 100\.
   + For **VPC**, choose the default VPC for your AWS Region\.

     The default VPC name uses the following format: `vpc-`*vpc\-id*` (No_default_value_Name)`\.
   + For **Subnet 1**, choose a default public subnet and make a note of the Availability Zone\. 

     The default subnet names use the following format: `subnet-`*subnet\-id*` | (`*IPv4 CIDR block*`) | Default in` *availability\-zone*\.
   + Optionally, for **Subnet 2**, choose a default subnet in a different Availability Zone\.
   + For **Security groups**, select the default security group\.

     The default security group name uses the following format: `sg-`*security\-group\-id*`-default`

1. Continue with the steps in [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

Complete the following steps to use the default VPC, subnet, and security group for an image builder\.

**To use the default VPC, subnet, and security group for an image builder**

1. Follow the steps in [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md) up to **Step 3: Configure Network**\.

1. In **Step 4: Configure Network**, do the following:
   + To enable your image builder to access the internet, select the **Default Internet Access** check box\.
   + For **VPC**, choose the default VPC for your AWS Region\.

     The default VPC name uses the following format: `vpc-`*vpc\-id*` (No_default_value_Name)`\.
   + For **Subnet 1**, choose a default public subnet\.

     The default subnet names use the following format: `subnet-`*subnet\-id*` | (`*IPv4 CIDR block*`) | Default in` *availability\-zone*\.
   + For **Security groups**, select the default security group\.

     The default security group name uses the following format: `sg-`*security\-group\-id*`-default`

1. Continue with the steps in [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.