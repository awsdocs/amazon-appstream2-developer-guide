# Roles Required for AppStream 2\.0 and Application Auto Scaling<a name="roles-required-for-appstream"></a>

In AWS, IAM roles are used to give permissions to an AWS service so it can access AWS resources\. The policies that are attached to the role determine which AWS resources the service can access and what it can do with those resources\. For AppStream 2\.0, in addition to having the permissions defined in the **AmazonAppStreamFullAccess** policy, you must also have the following roles in your AWS account, with the required policies attached\.

**Topics**
+ [AmazonAppStreamServiceAccess](#AmazonAppStreamServiceAccess)
+ [ApplicationAutoScalingForAmazonAppStreamAccess](#ApplicationAutoScalingForAmazonAppStreamAccess)
+ [AWSServiceRoleForApplicationAutoScaling\_AppStreamFleet](#AWSServiceRoleForApplicationAutoScaling_AppStreamFleet)

These roles are automatically created for you, with the required IAM policies attached, when you get started with the AppStream 2\.0 service in an AWS Region\. To get started with AppStream 2\.0, you must have either of the following permissions:
+ **AdministratorAccess** permissions
+ Permissions to create an IAM role and attach IAM policies to a role

**Note**  
To create the **AWSServiceRoleForApplicationAutoScaling\_AppStreamFleet** role, you must have also have the **iam:CreateServiceLinkedRole** permission\.

## AmazonAppStreamServiceAccess<a name="AmazonAppStreamServiceAccess"></a>

While AppStream 2\.0 resources are being created, the AppStream 2\.0 service makes API calls to other AWS services on your behalf by assuming this role\. To create fleets, you must have this service role in your account\. If this service role is not in your AWS account and the required IAM permissions and trust relationship policies are not attached, you cannot create AppStream 2\.0 fleets\.

## ApplicationAutoScalingForAmazonAppStreamAccess<a name="ApplicationAutoScalingForAmazonAppStreamAccess"></a>

Automatic scaling is a feature of AppStream 2\.0 fleets\. To configure scaling policies, you must have this service role in your AWS account\. If this service role is not in your AWS account and the required IAM permissions and trust relationship policies are not attached, you cannot scale AppStream 2\.0 fleets\.

## AWSServiceRoleForApplicationAutoScaling\_AppStreamFleet<a name="AWSServiceRoleForApplicationAutoScaling_AppStreamFleet"></a>

Application Auto Scaling uses a service\-linked role to perform automatic scaling on your behalf\. A *service\-linked role* is an IAM role that is linked directly to an AWS service\. This role includes all the permissions that the service requires to call other AWS services on your behalf\.

For more information, see [Service\-Linked Roles](https://docs.aws.amazon.com/autoscaling/application/userguide/application-auto-scaling-service-linked-roles.html) in the *Application Auto Scaling User Guide*\.