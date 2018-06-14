# Enabling Internet Access Using a Public Subnet<a name="managing-network-internet-default"></a>

AppStream 2\.0 can provide your fleets with a default internet connection by using your Amazon VPC public subnet\. This subnet has a route to the internet through an internet gateway\. 

AppStream 2\.0 enables internet connectivity by associating an [Elastic IP address](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/elastic-ip-addresses-eip.html) to the network interface that is attached from the streaming instance to your VPC public subnet\. You can have a VPC with a public subnet in several ways:

**Default VPC**  
Your AWS account, if it was created after 2013\-12\-04, has a default VPC that has public subnets\. You can use this default VPC to enable internet access from your streaming instances\. For more information, see [Default VPC and Default Subnets](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/default-vpc.html) in the *Amazon VPC User Guide*\.

**New VPC**  
If your AWS account was created before 2013\-12\-04 or to manage a new VPC, you can create a new VPC with a public subnet using the VPC creation wizard\. For more information, see [Implementation of VPC with a single public subnet](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Scenario1.html#VPC_Scenario1_Implementation) in the *Amazon VPC User Guide*\. 

**Existing VPC**  
To use an existing VPC that does not have a public subnet, you can add a new public subnet using the following steps\.  

**To add a new public subnet to an existing VPC**

1. Follow the steps in [Creating a Subnet](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IGW_Create_Subnet) in the *Amazon VPC User Guide*, using the existing VPC you intend to use with AppStream 2\.0\.

1. To add an internet gateway to your VPC, follow the steps in [Attaching an Internet Gateway](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IGW_Attach_Gateway) in the *Amazon VPC User Guide*\.

1. To configure your subnets to route internet traffic through the internet gateway, follow the steps in [Creating a Custom Route Table](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IGW_Routing) in the *Amazon VPC User Guide*\. Use IPv4 format \(`0.0.0.0/0`\) for **Destination**\.

## Enabling Internet Access for a Fleet<a name="managing-network-internet-dia-fleet"></a>

After you have a public subnet available on a VPC, you can enable internet access for your fleet\. This can be performed either when you create the fleet, or by editing the fleet details after creation\.

**To enable internet access at fleet creation**

1. Follow the instructions at [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create) up to the **Network access** section\.

1. Choose **Default Internet Access**\.

1. If the subnet fields are empty, select a subnet for **Subnet 1** and, if desired, **Subnet 2**\.

1. Continue with the instructions at [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

**To enable internet access after fleet creation**

1. In the navigation pane, choose **Fleets**\.

1. Select a fleet and check that its state is **Stopped**\.

1. Choose **Fleet Details**, **Edit**, **Default Internet Access**\.

1. Choose a subnet for **Subnet 1** and, if desired, **Subnet 2**\. Choose **Update**\.

You can test internet connectivity by starting your fleet, creating a stack, associating the fleet to a stack, and browsing the internet within a streaming session for stack\. For more information, see [Create AppStream 2\.0 Fleets and Stacks](set-up-stacks-fleets.md)\.

## Enabling Internet Access for an Image Builder<a name="managing-network-internet-dia-image-builder"></a>

After you have a public subnet available on a VPC, and can enable internet access for your image builder\. This can be performed when you create the image builder\.

**To enable internet access for an image builder**

1. Follow the instructions at [Step 1: Create an Image Builder](tutorial-image-builder.md#tutorial-image-builder-create) up to the **Network Access** section\.

1. Choose **Default Internet Access**\.

1. If **Subnet** is empty, select a subnet\.

1. Continue with the instructions at [Step 1: Create an Image Builder](tutorial-image-builder.md#tutorial-image-builder-create)\.