# Enable Internet Access for Your Fleet and Image Builder<a name="managing-network-manual-enable-internet-access"></a>

After your NAT gateway is available on a VPC, you can enable internet access for your fleet and image builder\.

## Enable Internet Access for Your Fleet<a name="managing-network-manual-enable-internet-access-fleet"></a>

You can enable internet access either when you create the fleet or later\.

**To enable internet access at fleet creation**

1. Complete the steps in [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create) up to **Step 4: Configure Network**\.

1. Choose a VPC with a NAT gateway\.

1. If the subnet fields are empty, select a private subnet for **Subnet 1** and, optionally, another private subnet for **Subnet 2**\. If you don't already have a private subnet in your VPC, you may need to create a second private subnet\.

1. Continue with the steps in [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

**To enable internet access after fleet creation by using a NAT gateway**

1. In the navigation pane, choose **Fleets**\.

1. Select a fleet and verify that the state is **Stopped**\.

1. Choose **Fleet Details**, **Edit**, and choose a VPC with a NAT gateway\.

1. Choose a private subnet for **Subnet 1** and, optionally, another private subnet for **Subnet 2**\. If you don't already have a private subnet in your VPC, you may need to [create a second private subnet](create-configure-new-vpc-with-private-public-subnets-nat.md#vpc-with-private-and-public-subnets-add-private-subnet-nat)\. 

1. Choose **Update**\.

You can test your internet connectivity by starting your fleet, and then connecting to your streaming instance and browsing to the internet\. 

## Enable Internet Access for Your Image Builder<a name="managing-network-manual-enable-internet-access-image-builder"></a>

If you plan to enable internet access for your image builder, you must do so when you create the image builder\.

**To enable internet access for an image builder**

1. Complete the steps in [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md), up to **Step 3: Configure Network**\.

1. Choose the VPC with a NAT gateway\.

1. If **Subnet** is empty, select a subnet\.

1. Continue with the steps in [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.