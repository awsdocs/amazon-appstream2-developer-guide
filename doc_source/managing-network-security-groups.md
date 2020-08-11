# Security Groups in Amazon AppStream 2\.0<a name="managing-network-security-groups"></a>

You can provide additional access control to your VPC from streaming instances in a fleet or an image builder in Amazon AppStream 2\.0 by associating them with VPC security groups\. Security groups that belong to your VPC allow you to control the network traffic between AppStream 2\.0 streaming instances and VPC resources such as license servers, file servers, and database servers\. For more information, see [Security Groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the *Amazon VPC User Guide*\.

The rules that you define for your VPC security group are applied when the security group is associated with a fleet or image builder\. The security group rules determine what network traffic is allowed from your streaming instances\. For more information, see [Security Group Rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#SecurityGroupRules) in the *Amazon VPC User Guide*\.

You can associate up to five security groups while launching a new image builder or while creating a new fleet\. You can also associate security groups with an existing fleet or change the security groups for a fleet \(to change security groups for a fleet, you must first stop the fleet\)\. For more information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.

If you don't select a security group, your image builder or fleet is associated with the default security group for your VPC\. For more information, see [Default Security Group for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#DefaultSecurityGroup) in the *Amazon VPC User Guide*\.

Use these additional considerations when using security groups with AppStream 2\.0\.
+ All end user data, such as internet traffic, home folder data, or application communication with VPC resources, are affected by the security groups associated with the streaming instance\.
+ Streaming pixel data is not affected by security groups\.
+ If you have enabled default internet access for your fleet or image builder, the rules of the associated security groups must allow internet access\.

You can create or edit rules for your security groups or create new security groups using the Amazon VPC console\. 
+ **To associate security groups with an image builder** — Follow the instructions at [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.
+ **To associate security groups with a fleet**
  + *While creating the fleet* — Follow the instructions at [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.
  + *For an existing fleet* — Edit the fleet settings using the AWS Management Console\.

You can also associate security groups to your fleets using the AWS CLI and SDKs\.
+ **AWS CLI** — Use the [create\-fleet](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-fleet.html) and [update\-fleet](https://docs.aws.amazon.com/cli/latest/reference/appstream/update-fleet.html) commands\.
+ **AWS SDKs** — Use the [CreateFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateFleet.html) and [UpdateFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UpdateFleet.html) API operations\.

For more information, see the [AWS Command Line Interface User Guide](https://docs.aws.amazon.com/cli/latest/userguide/) and [Tools for Amazon Web Services](https://aws.amazon.com/tools/)\.