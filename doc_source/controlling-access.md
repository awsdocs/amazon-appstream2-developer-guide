# Controlling Access to Amazon AppStream 2\.0 with IAM Policies and Service Roles<a name="controlling-access"></a>

AWS Identity and Access Management \(IAM\) policies grant permissions to specific resources and API actions\. To manage AppStream 2\.0 resources and perform API actions through the AWS Command Line Interface \(AWS CLI\), AWS SDK, or AWS Management Console, you must have the permissions defined in the AmazonAppStreamFullAccess managed policy\. 

If you sign into the AppStream 2\.0 console as an IAM user, you must attach this policy to your IAM user account\. If you sign in through console federation, you must attach this policy to the IAM role that was used for federation\. 

The AmazonAppStreamReadOnlyAccess managed policy is available for users who require only read access to AppStream 2\.0 resources\. 

**Topics**
+ [IAM Service Roles Required for Managing AppStream 2\.0 Resources](#controlling-access-iam-service-role)
+ [Permissions Required for IAM Service Role Creation](#controlling-access-service-role-creation-perms)
+ [Checking for the AmazonAppStreamServiceAccess Service Role and Policies](#controlling-access-checking-for-iam-service-access)
+ [Checking for the ApplicationAutoScalingForAmazonAppStreamAccess Service Role and Policies](#controlling-access-checking-for-iam-autoscaling)
+ [Application Auto Scaling Required IAM Permissions](#autoscaling-iam-policy)
+ [IAM Policies and the Amazon S3 Bucket for Home Folders](#s3-iam-policy)

## IAM Service Roles Required for Managing AppStream 2\.0 Resources<a name="controlling-access-iam-service-role"></a>

In addition to having the permissions defined in the AmazonAppStreamFullAccess policy, you must also have the AmazonAppStreamServiceAccess and the ApplicationAutoScalingForAmazonAppStreamAccess IAM service roles present in your AWS account, with the appropriate policies attached\. The AppStream 2\.0 and Application Auto Scaling services assume these roles and call other AWS services as needed to manage your resources\.

**AmazonAppStreamServiceAccess**  
While AppStream 2\.0 resources are being created, the AppStream 2\.0 service makes API calls to other AWS services on your behalf by assuming this role\. If this service role is not present in your AWS account and the required IAM permissions and trust relationship policies are not attached, you cannot create AppStream 2\.0 fleets\.

**ApplicationAutoScalingForAmazonAppStreamAccess**  
The Application Auto Scaling service uses this service role to scale AppStream 2\.0 resources on your behalf\. If this service role is not present in your AWS account and the required IAM permissions and trust relationship policies are not attached, you cannot scale AppStream 2\.0 fleets\.

## Permissions Required for IAM Service Role Creation<a name="controlling-access-service-role-creation-perms"></a>

If you have the required permissions, these two service roles are automatically created by AppStream 2\.0, with the required IAM policies attached, when you get started with the AppStream 2\.0 service in an AWS Region\. You or an administrator must have one of the following permissions to get started with AppStream 2\.0 in your AWS account:
+ Permissions to create an IAM role and attach IAM policies to a role 
+ AdministratorAccess permissions

**Note**  
IAM roles and policies control which AppStream 2\.0 resources can be accessed\. The user pool controls access to AppStream 2\.0 itself\. For more information, see [Manage Access Using the AppStream 2\.0 User Pool](user-pool.md)\.

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

## Application Auto Scaling Required IAM Permissions<a name="autoscaling-iam-policy"></a>

To use AppStream 2\.0 Fleet Auto Scaling, the IAM user accessing fleet creation and scaling settings must have appropriate permissions for the services that support dynamic scaling\. AppStream 2\.0 requires the following permissions:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
          "appstream:*",
          "application-autoscaling:*",
          "cloudwatch:DeleteAlarms",
          "cloudwatch:DescribeAlarmsForMetric",
          "cloudwatch:DisableAlarmActions",
          "cloudwatch:DescribeAlarms",
          "cloudwatch:EnableAlarmActions",
          "cloudwatch:ListMetrics",
          "cloudwatch:PutMetricAlarm",
          "iam:passrole",
          "iam:ListRoles"
      ],
      "Resource": "*"
    }
  ]
}
```

## IAM Policies and the Amazon S3 Bucket for Home Folders<a name="s3-iam-policy"></a>

Access to the Amazon S3 bucket for Home folders is managed using IAM permissions and policies\.

**Topics**
+ [Deleting the Amazon S3 Bucket for Home Folders](#s3-iam-policy-delete)
+ [Restricting Administrator Access to the Amazon S3 Bucket for Home Folders](#s3-iam-policy-restricted-access)

### Deleting the Amazon S3 Bucket for Home Folders<a name="s3-iam-policy-delete"></a>

AppStream 2\.0 adds an Amazon S3 bucket policy that prevents the accidental deletion of the S3 bucket, shown at the end of this section\. You must delete the S3 bucket policy first, and then you can delete the S3 bucket\. For more information, see [Deleting or Emptying a Bucket](http://docs.aws.amazon.com/AmazonS3/latest/dev/delete-or-empty-bucket.html) in the *Amazon Simple Storage Service Developer Guide*\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PreventAccidentalDeletionOfBucket",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:DeleteBucket",
      "Resource": "arn:aws:s3:::appstream2-36fb080bb8-region-code-account-id-without-hyphens"
    }
  ]
}
```

### Restricting Administrator Access to the Amazon S3 Bucket for Home Folders<a name="s3-iam-policy-restricted-access"></a>

By default, administrators who can access the Amazon S3 bucket created by AppStream 2\.0 can view and modify content that is part of users' Home folders\. To restrict administrator access to the S3 bucket containing user files, we recommend applying the S3 bucket access policy based on the following template: 

```
{
  "Sid": "RestrictedAccess",
  "Effect": "Deny",
  "NotPrincipal": 
  {
    "AWS": [
      "arn:aws:iam::account:role/service-role/AmazonAppStreamServiceAccess",
      "arn:aws:sts::account:assumed-role/AmazonAppStreamServiceAccess/PhotonSession",
      "arn:aws:iam::account:user/IAM-user-name"
    ]
  },
    "Action": "s3:*",
    "Resource": "arn:aws:s3:::appstream2-36fb080bb8-region-account"
  }
 ]
}
```

This policy allows Home folder S3 bucket access only to the users specified and to the AppStream 2\.0 service\. For every IAM user who should have access, replicate the following line:

```
"arn:aws:iam::account:user/IAM-user-name"
```

In the following example, the policy restricts access to the Home folder S3 bucket for anyone other than IAM users marymajor and johnstiles, and also restricts access to the AppStream 2\.0 service, in Region us\-west\-2 for account ID 123456789012\.

```
{
  "Sid": "RestrictedAccess",
  "Effect": "Deny",
  "NotPrincipal": 
  {
    "AWS": [
      "arn:aws:iam::123456789012:role/service-role/AmazonAppStreamServiceAccess",
      "arn:aws:sts::123456789012:assumed-role/AmazonAppStreamServiceAccess/PhotonSession",
      "arn:aws:iam::123456789012:user/marymajor",
      "arn:aws:iam::123456789012:user/johnstiles"
    ]
  },
    "Action": "s3:*",
    "Resource": "arn:aws:s3:::appstream2-36fb080bb8-us-west-2-123456789012"
  }
 ]
}
```