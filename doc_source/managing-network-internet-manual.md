# Enabling Internet Access Using a NAT Gateway<a name="managing-network-internet-manual"></a>

You can control internet access for your users using an advanced networking configuration such as NAT gateways\. To manage your own VPC and VPC NAT gateway, launch your AppStream 2\.0 image builders and fleets in private VPC subnets that provide a route to the internet\. Use the instructions below to quickly create a network setup for enabling internet access\. For more information, see [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) and [VPC with Public and Private Subnets \(NAT\)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html) in the *Amazon VPC User Guide*\.

**To create and configure a new VPC to use with a VPC NAT gateway**

1. Navigate to [Implementing VPC with Public and Private Subnets \(NAT\)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html#VPC_Scenario2_Implementation) in the *Amazon VPC User Guide*, and follow the steps given in the section **To create a VPC**, leaving out the optional IPv6 step\.

1. For **Availability Zone**, leave the public subnet zone as the default, and select a specific zone for the private subnet\. Make a note of the zones you chose\.

1. For **Elastic IP Allocation ID**, choose an existing Elastic IP address\. If you don't have one, create an Elastic IP address from the **Elastic IPs** section on the Amazon VPC console\.

1. Leave the other fields as their default values, making a note of the value for **Private subnet's IPv4 CIDR**, and then choose **Create VPC**\. This may take some time to complete\.

1. If you want to add another private subnet to your VPC, perform the following steps\.

   1. In the left navigation pane, choose **Subnets**, **Create Subnet**\. Be sure to choose a different name than the ones specified in step 3\.

   1. For **VPC**, enter the VPC that you created earlier\. For **Availability Zone**, enter a different value than the one noted earlier\.

   1. For **IPv4 CIDR block**, provide a unique for the new subnet\. For example, if you noted that the first subnet has a IPv4 CIDR block range of `10.0.1.0/24`, the new subnet could have a valid CIDR block range of `10.0.2.0/24`\.

1. Choose **Yes, Create**\.

**To add a NAT gateway to an existing VPC**

1. Follow the instructions in [Creating a NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html#nat-gateway-creating) in the *Amazon VPC User Guide*\.

1. To update the route tables of your private subnets and route internet traffic through the NAT gateway, follow the instructions in [Updating Your Route Table](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html#nat-gateway-create-route) in the *Amazon VPC User Guide*\.

1. Check your VPC to be sure it has at least one private subnet and, if needed, create a new private subnet\. For more information, see [Creating a Subnet](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html#Add_IGW_Create_Subnet) in the *Amazon VPC User Guide*\.

## Enabling Internet Access for a Fleet Using a NAT Gateway<a name="managing-network-internet-manual-fleet"></a>

After you have a NAT gateway available on a VPC, you can enable internet access for your fleet\. This can be performed either when you create it, or by editing the fleet details after creation\.

**To enable internet access at fleet creation using a NAT gateway**

1. Follow the instructions at [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create) up to the **Network access** section\.

1. Choose a VPC with a NAT gateway\.

1. If the subnet fields are empty, select a private subnet for **Subnet 1** and, if desired, another private subnet for **Subnet 2**\. If one is not already present for your VPC, you may need to create a second private subnet \.

1. Continue with the instructions at [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

**To enable internet access after fleet creation using a NAT gateway**

1. In the navigation pane, choose **Fleets**\.

1. Select a fleet and check that the state is **Stopped**\.

1. Choose **Fleet Details**, **Edit**, and choose a VPC with a NAT gateway\.

1. Choose a private subnet for **Subnet 1** and, if desired, another private **Subnet 2**\. You may need to create a second private subnet if one is not already present for your VPC\. 

1. Choose **Update**\.

You can test your internet connectivity by starting your fleet, and then connecting to your streaming instance and browsing to the internet\. 

## Enabling Internet Access for an Image Builder Using a NAT Gateway<a name="managing-network-internet-manual-image-builder"></a>

After you have a NAT gateway available on a VPC, and can enable internet access for your image builder\. This can be performed when you create the image builder\.

**To enable internet access for an image builder using a NAT gateway**

1. Follow the instructions at [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md), up to the **Network Access** section\.

1. Choose the VPC with a NAT gateway\.

1. If **Subnet** is empty, select a subnet\.

1. Continue with the instructions at [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.