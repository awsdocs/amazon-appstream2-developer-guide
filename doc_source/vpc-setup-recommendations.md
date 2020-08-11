# VPC Setup Recommendations<a name="vpc-setup-recommendations"></a>

When you create a fleet or launch an image builder, you specify the VPC and one or more subnets to use\. You can provide additional access control to your VPC by specifying security groups\. 

The following recommendations can help you configure your VPC more effectively and securely\. In addition, they can help you configure an environment that supports effective fleet scaling\. With effective fleet scaling, you can meet current and anticipated AppStream 2\.0 user demand, while avoiding unecessary resource usage and associated costs\. 

**Overall VPC Configuration**
+ Make sure that your VPC configuration can support your fleet scaling needs\. 

  As you develop your plan for fleet scaling, keep in mind that one user requires one fleet instance\. Therefore, the size of your fleet determines the number of users who can stream concurrently\. For this reason, for each [instance type](instance-types.md) that you plan to use, make sure that the number of fleet instances that your VPC can support is greater than the number of anticipated concurrent users for the same instance type\.
+ Make sure that your AppStream 2\.0 account quotas \(also referred to as limits\) are sufficient to support your anticipated demand\. To request a quota increase, use the [AppStream 2\.0 Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-appstream2)\. For more information about AppStream 2\.0 limits, see [Amazon AppStream 2\.0 Service Quotas](limits.md)\. 
+ If you plan to provide your streaming instances \(fleet instances or image builders\) with access to the internet, we recommend that you configure a VPC with two private subnets for your streaming instances and a NAT gateway in a public subnet\.

  The NAT gateway lets the streaming instances in your private subnets connect to the internet or other AWS services\. However, it prevents the internet from initiating a connection with those instances\. In addition, unlike configurations that use the **Default Internet Access** option for enabling internet access, the NAT configuration supports more than 100 fleet instances\. For more information, see [Configure a VPC with Private Subnets and a NAT Gateway](managing-network-internet-NAT-gateway.md)\.

**Elastic Network Interfaces**
+ AppStream 2\.0 creates as many [elastic network interfaces](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_ElasticNetworkInterfaces.html) \(network interfaces\) as the maximum desired capacity of your fleet\. By default, the limit for network interfaces per Region is 5000\. 

  When planning capacity for very large deployments, for example, thousands of streaming instances, consider the number of EC2 instances that are also used in the same Region\.

**Subnets**
+ If you are configuring more than one private subnet for your VPC, configure each in a different Availability Zone\. Doing so increases fault tolerance and can help prevent insufficient capacity errors\.
+ Make sure that the network resources required for your applications are accessible through both of your private subnets\. 
+ Configure each of your private subnets with a subnet mask that allows for enough client IP addresses to account for the maximum number of expected concurrent users\. In addition, allow for additional IP addresses to account for anticipated growth\. For more information, see [VPC and Subnet Sizing for IPv4](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-sizing-ipv4)\.
+ If you are using a VPC with NAT, configure at least one public subnet with a NAT Gateway for internet access, preferably two\. Configure the public subnets in the same Availability Zones where your private subnets reside\. 

  To enhance fault tolerance and reduce the chance of insufficient capacity errors for large AppStream 2\.0 fleet deployments, consider extending your VPC configuration into a third Availability Zone\. Include a private subnet, public subnet, and NAT gateway in this additional Availability Zone\.
**Note**  
To configure more than two Availability Zones, you can use the [UpdateFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UpdateFleet.html) API action or the [update\-fleet](https://docs.aws.amazon.com/cli/latest/reference/appstream;update-fleet.html) AWS CLI command\.

**Security Groups**
+ Use security groups to provide additional access control to your VPC\. 

  Security groups that belong to your VPC let you control the network traffic between AppStream 2\.0 streaming instances and network resources required by applications\. These resources may include other AWS services such as Amazon RDS or Amazon FSx, license servers, database servers, file servers, and application servers\.
+ Make sure that the security groups provide access to the network resources that your applications require\.

  For more information about configuring security groups for AppStream 2\.0, see [Security Groups in Amazon AppStream 2\.0](managing-network-security-groups.md)\. For general information about security groups, see [Security Groups for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups) in the *Amazon VPC User Guide*\.