# Using AWS Managed Policies and Service\-Linked Roles to Manage Administrator Access to AppStream 2\.0 Resources<a name="controlling-administrator-access-with-policies-service-linked-roles"></a>

This topic describes the AWS managed policies and service\-linked roles that are required to manage administrator access to AppStream 2\.0 resources, and to create and scale AppStream 2\.0 fleets\.

**Topics**
+ [AWS Managed Policies Required to Access AppStream 2\.0 Resources](#managed-policies-required-to-access-appstream-resources)
+ [Service\-Linked Roles Required for AppStream 2\.0 and Application Auto Scaling](#service-roles-required-for-appstream)
+ [Checking for the AmazonAppStreamServiceAccess Service Role and Policies](#controlling-access-checking-for-iam-service-access)
+ [Checking for the ApplicationAutoScalingForAmazonAppStreamAccess Service Role and Policies](#controlling-access-checking-for-iam-autoscaling)

## AWS Managed Policies Required to Access AppStream 2\.0 Resources<a name="managed-policies-required-to-access-appstream-resources"></a>

By default, IAM users and groups don't have permissions to access AppStream 2\.0 resources\. To provide full administrative or read\-only access to AppStream 2\.0, you must attach one of the following AWS managed policies to the appropriate IAM users or groups\. An *AWS managed policy* is a standalone policy that is created and administered by AWS\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

**AmazonAppStreamFullAccess**  
This managed policy provides full administrative access to AppStream 2\.0 resources\. To manage AppStream 2\.0 resources and perform API actions through the AWS Command Line Interface \(AWS CLI\), AWS SDK, or AWS Management Console, you must have the permissions defined in this policy\.  
If you sign into the AppStream 2\.0 console as an IAM user, you must attach this policy to your IAM user account\. If you sign in through console federation, you must attach this policy to the IAM role that was used for federation\.

**AmazonAppStreamReadOnlyAccess**  
This managed policy provides read\-only access to AppStream 2\.0 resources\.

The AppStream 2\.0 console uses two additional actions that provide functionality that is not available through the AWS CLI or AWS SDK\. The **AmazonAppStreamFullAccess** and **AmazonAppStreamReadOnlyAccess** policies both provide permissions for these actions\.


| Action | Description | Access Level | 
| --- | --- | --- | 
| GetImageBuilders | Grants permission to retrieve a list that describes one or more specified image builders, if the image builder names are provided\. Otherwise, all image builders in the account are described\. | Read | 
| GetParametersForThemeAssetUpload | Grants permission to upload theme assets for custom branding\. For more information, see [Add Your Custom Branding to Amazon AppStream 2\.0](branding.md)\. | Write | 

## Service\-Linked Roles Required for AppStream 2\.0 and Application Auto Scaling<a name="service-roles-required-for-appstream"></a>

In addition to having the permissions defined in the AmazonAppStreamFullAccess policy, you must also have the following service\-linked roles present in your AWS account, with the appropriate policies attached\. *Service\-linked roles* are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf\. For more information, see [Using Service\-Linked Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html) in the *IAM User Guide*\.

**AmazonAppStreamServiceAccess**  
While AppStream 2\.0 resources are being created, the AppStream 2\.0 service makes API calls to other AWS services on your behalf by assuming this role\. If this service role is not present in your AWS account and the required IAM permissions and trust relationship policies are not attached, you cannot create AppStream 2\.0 fleets\.

**ApplicationAutoScalingForAmazonAppStreamAccess**  
The Application Auto Scaling service uses this service role to scale AppStream 2\.0 resources on your behalf\. If this service role is not present in your AWS account and the required IAM permissions and trust relationship policies are not attached, you cannot scale AppStream 2\.0 fleets\.

If you have the required permissions, these two service roles are automatically created by AppStream 2\.0, with the required IAM policies attached, when you get started with the AppStream 2\.0 service in an AWS Region\.

To get started with AppStream 2\.0 in your AWS account, you or an administrator must have one of the following permissions to get started with AppStream 2\.0 in your AWS account:
+ Permissions to create an IAM role and attach IAM policies to a role 
+ AdministratorAccess permissions

**Note**  
IAM roles and policies control administrator access to AppStream 2\.0 resources\. For a simplified way to manage end user access to AppStream 2\.0, you can use the AppStream 2\.0 user pool\. The AppStream 2\.0 user pool lets you manage access to applications for your users through a persistent portal for each AWS Region\. This feature is a built\-in alternative to user management through Active Directory and SAML 2\.0 federation\. For more information, see [Manage Access Using the AppStream 2\.0 User Pool](user-pool.md)\.

## Checking for the AmazonAppStreamServiceAccess Service Role and Policies<a name="controlling-access-checking-for-iam-service-access"></a>

Follow the steps in this section to check whether the AmazonAppStreamServiceAccess service role is present and has the correct policies attached\. If this service role is not present and must be created, you or an administrator with the required permissions must perform the steps to get started with AppStream 2\.0 in your AWS account\.

**Topics**
+ [AmazonAppStreamServiceAccess permissions policy](#controlling-access-service-access-permissions-policy)
+ [AmazonAppStreamServiceAccess trust relationship policy](#controlling-access-service-access-trust-policy)

**To check whether the AmazonAppStreamServiceAccess IAM service role is present**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Roles**\. 

1. In the search box, type `amazonappstreamservice` to narrow the list of roles to select, and then choose **AmazonAppStreamServiceAccess**\. If this role is listed, select it to view the role summary\. 

1. On the **Permissions** tab, confirm whether the AmazonAppStreamServiceAccess permissions policy is attached and follows the correct format\. If so, the permissions policy is correctly configured\.

1. On the **Trust relationships** tab, choose **Edit trust relationship**, and then confirm whether the AmazonAppStreamServiceAccess trust relationship policy is attached and follows the correct format\. If so, the trust relationship is correctly configured\. Choose **Cancel** and close the IAM console\. 

### AmazonAppStreamServiceAccess permissions policy<a name="controlling-access-service-access-permissions-policy"></a>

The format for this permissions policy is as follows:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeVpcs",
        "ec2:DescribeVpcEndpoints",
        "ec2:DescribeSubnets",
        "ec2:DescribeAvailabilityZones",
        "ec2:CreateNetworkInterface",
        "ec2:DescribeNetworkInterfaces",
        "ec2:DeleteNetworkInterface",
        "ec2:DescribeSubnets",
        "ec2:AssociateAddress",
        "ec2:DisassociateAddress",
        "ec2:DescribeRouteTables",
        "ec2:DescribeSecurityGroups"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject",
        "s3:GetObjectVersion",
        "s3:DeleteObjectVersion",
        "s3:PutBucketPolicy"
      ],
      "Resource": "arn:aws:s3:::appstream2-36fb080bb8-*"
    }
  ]
}
```

### AmazonAppStreamServiceAccess trust relationship policy<a name="controlling-access-service-access-trust-policy"></a>

The format for this trust relationship policy is as follows:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
      "Service": "appstream.amazonaws.com"
    },
    "Action": "sts:AssumeRole"
    }
  ]
}
```

## Checking for the ApplicationAutoScalingForAmazonAppStreamAccess Service Role and Policies<a name="controlling-access-checking-for-iam-autoscaling"></a>

Follow the steps in this section to check whether the ApplicationAutoScalingForAmazonAppStreamAccess service role is present and has the correct policies attached\. If this service role is not present and must be created, you or an administrator with the required permissions must perform the steps to get started with AppStream 2\.0 in your AWS account\.

**Topics**
+ [ApplicationAutoScalingForAmazonAppStreamAccess permissions policy](#controlling-access-autoscaling-permissions-policy)
+ [ApplicationAutoScalingForAmazonAppStreamAccess trust relationship policy](#controlling-access-autoscaling-trust-policy)

**To check whether the ApplicationAutoScalingForAmazonAppStreamAccess IAM service role is present**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Roles**\. 

1. In the search box, type `applicationautoscaling` to narrow the list of roles to select, and then choose **ApplicationAutoScalingForAmazonAppStreamAccess**\. If this role is listed, select it to view the role summary\. 

1. On the **Permissions** tab, confirm whether the ApplicationAutoScalingForAmazonAppStreamAccess permissions policy is attached and follows the correct format\. If so, the permissions policy is correctly configured\. 

1. On the **Trust relationships **tab, choose **Edit trust relationship**, and then confirm whether the ApplicationAutoScalingForAmazonAppStreamAccess trust relationship policy is attached and follows the correct format\. If so, the trust relationship is correctly configured\. Choose **Cancel** and close the IAM console\. 

### ApplicationAutoScalingForAmazonAppStreamAccess permissions policy<a name="controlling-access-autoscaling-permissions-policy"></a>

The format for this permissions policy is as follows:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow", 
      "Action": [
        "appstream:UpdateFleet", 
        "appstream:DescribeFleets"
      ],
      "Resource": [ 
        "*"
      ]
    },
    {
      "Effect": "Allow", 
      "Action": [
        "cloudwatch:DescribeAlarms"
      ],
      "Resource": [ 
        "*"
      ]
    }
  ]
}
```

### ApplicationAutoScalingForAmazonAppStreamAccess trust relationship policy<a name="controlling-access-autoscaling-trust-policy"></a>

The format for this trust relationship policy is as follows:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "application-autoscaling.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```