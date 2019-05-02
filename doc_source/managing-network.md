# Networking, Access, and Security for Amazon AppStream 2\.0<a name="managing-network"></a>

The following sections contain information about enabling users to connnect to AppStream 2\.0 streaming instances and enabling your AppStream 2\.0 fleets and image builders to access network resources and the internet\.

**Contents**
+ [User Connections to Amazon AppStream 2\.0](appstream2-port-requirements-users.md)
  + [Bandwidth Recommendations](appstream2-port-requirements-users.md#bandwidth-recommendations-user-connections)
  + [Ports for AppStream 2\.0 User Devices](appstream2-port-requirements-users.md#client-application-ports)
  + [Whitelisted Domains](appstream2-port-requirements-users.md#whitelisted_ports)
+ [Amazon AppStream 2\.0 Connections to Your VPC](appstream2-port-requirements-appstream2.md)
  + [Network Interfaces](appstream2-port-requirements-appstream2.md#network-interfaces)
  + [Management Network Interface IP Address Range and Ports](appstream2-port-requirements-appstream2.md#management_ports)
  + [Customer Network Interface Ports](appstream2-port-requirements-appstream2.md#primary_ports)
+ [Network Setup Guidelines](#managing-network-guidelines)
  + [Fleets](#managing-network-guidelines-fleets)
  + [Image Builders](#managing-network-guidelines-image-builders)
+ [Security Groups](#managing-network-security-groups)
+ [Home Folders and VPC Endpoints](#managing-network-vpce-iam-policy)
+ [Enabling Internet Access Using a Public Subnet](managing-network-internet-default.md)
  + [Enabling Internet Access for a Fleet](managing-network-internet-default.md#managing-network-internet-dia-fleet)
  + [Enabling Internet Access for an Image Builder](managing-network-internet-default.md#managing-network-internet-dia-image-builder)
+ [Enabling Internet Access Using a NAT Gateway](managing-network-internet-manual.md)
  + [Enabling Internet Access for a Fleet Using a NAT Gateway](managing-network-internet-manual.md#managing-network-internet-manual-fleet)
  + [Enabling Internet Access for an Image Builder Using a NAT Gateway](managing-network-internet-manual.md#managing-network-internet-manual-image-builder)

## Network Setup Guidelines<a name="managing-network-guidelines"></a>

There are some network setup guidelines to consider for fleets and image builders\. If your fleets and image builders require internet access, you can use the Default Internet Access feature\. You could also manually control internet access using an advanced networking configuration, such as a VPC with NAT gateways\. For more information, see [Enabling Internet Access Using a Public Subnet](managing-network-internet-default.md) and [Enabling Internet Access Using a NAT Gateway](managing-network-internet-manual.md)\.

### Fleets<a name="managing-network-guidelines-fleets"></a>

You can provide subnets to establish network connections from your fleet instances to your VPC\. We recommend that you specify two private subnets from different Availability Zones for high availability and fault tolerance\. Also, ensure that the network resources for your applications are accessible through both of the specified private subnets\.

AppStream 2\.0 creates as many elastic network interfaces as the maximum desired capacity of your fleet\. The following guidelines will help you set up a VPC to support scaling behavior for your fleet\.
+ Make sure that your AWS account has sufficient elastic network interface capacity to support the scaling requirements of your fleet\. If you are planning to launch a large fleet of streaming instances, contact AWS Support and request a higher ENI limit to match the maximum number of instances that you plan to launch\.
+ Specify subnets with a sufficient number of elastic IP addresses to match the maximum desired capacity of your fleet\.
+ Use security groups to provide your VPC with specific security settings\. For more information, see [Security Groups](#managing-network-security-groups)\.

### Image Builders<a name="managing-network-guidelines-image-builders"></a>

When you launch an image builder, you choose the subnet and security groups to use\. Make sure that the subnet and security groups provide access to the network resources that your applications require\. Typical network resources required by applications may include licensing servers, database servers, file servers, and application servers\.

## Security Groups<a name="managing-network-security-groups"></a>

You can provide additional access control to your VPC from streaming instances in a fleet or an image builder in Amazon AppStream 2\.0 by associating them with VPC security groups\. Security groups that belong to your VPC allow you to control the network traffic between AppStream 2\.0 streaming instances and VPC resources such as license servers, file servers, and database servers\. For more information, see [Security Groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the *Amazon VPC User Guide*\.

The rules that you define for your VPC security group are applied when the security group is associated with a fleet or image builder\. The security group rules determine what network traffic is allowed from your streaming instances\. For more information, see [Security Group Rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#SecurityGroupRules) in the *Amazon VPC User Guide*\.

You can associate up to five security groups while launching a new image builder or while creating a new fleet\. You can also associate security groups to an existing fleet or change the security groups of a fleet\. For more information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.

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

## Home Folders and VPC Endpoints<a name="managing-network-vpce-iam-policy"></a>

To support home folders and application settings persistence on a private network, AppStream 2\.0 needs access permissions to the VPC endpoint\. To enable AppStream 2\.0 access to your private Amazon S3 endpoint, attach a custom policy, as defined below, to your VPC endpoint for Amazon S3\. For more information about private Amazon S3 endpoints, see [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html) and [Endpoints for Amazon S3](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-s3.html) in the *Amazon VPC User Guide*\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-AppStream-to-access-home-folder-and-application-settings",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:sts::account-id-without-hyphens:assumed-role/AmazonAppStreamServiceAccess/AppStream2.0"
      },
      "Action": [
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject",
        "s3:GetObjectVersion",
        "s3:DeleteObjectVersion"
      ],
      "Resource": [
        "arn:aws:s3:::appstream2-36fb080bb8-*",
        "arn:aws:s3:::appstream-app-settings-*"
      ]
    }
  ]
}
```