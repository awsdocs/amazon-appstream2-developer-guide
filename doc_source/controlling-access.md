# Controlling Access to Amazon AppStream 2\.0 with IAM Roles and Policies<a name="controlling-access"></a>

By default, IAM users don't have permission to create or modify AppStream 2\.0 resources, use Fleet Auto Scaling, or perform tasks using the AppStream 2\.0 API\. To allow IAM users to create or modify resources and perform tasks, you must create IAM policies that grant permissions on specific resources and API actions, and then attach those policies to the IAM users or groups that require those permissions\.

While creating AppStream 2\.0 resources, AppStream 2\.0 makes API calls to other AWS services on behalf of the user\. This authentication is accomplished by the service assuming specific IAM roles available in the user's account\. These IAM roles are created by the service when the user gets started with the service in an AWS region\.

**Note**  
IAM roles and policies control which AppStream 2\.0 resources can be accessed, while the user pool controls access to AppStream 2\.0 itself\. For more information, see [Manage Access Using the AppStream 2\.0 User Pool](user-pool.md)\.

**Topics**
+ [IAM Service Role](#controlling-access-iam-service-role)
+ [Identity Based Policies](#controlling-access-iam)
+ [Application Auto Scaling IAM Role](#autoscaling-iam-role)
+ [Application Auto Scaling Required IAM Permissions](#autoscaling-iam-policy)
+ [IAM Policies and the Amazon S3 Bucket for Home Folders](#s3-iam-policy)

## IAM Service Role<a name="controlling-access-iam-service-role"></a>

The **AmazonAppStreamServiceAccess** service role is available for AppStream 2\.0\.

## Identity Based Policies<a name="controlling-access-iam"></a>

AppStream 2\.0 provides managed policies that you can attach to your IAM users and allow users to control your AppStream 2\.0 resources or perform API actions through the AWS CLI, SDK, or console\.

**AmazonAppStreamFullAccess**  
Provides full administrator access to AppStream 2\.0 resources\.

**AmazonAppStreamReadOnlyAccess**  
Provides read\-only access to AppStream 2\.0 resources\.

## Application Auto Scaling IAM Role<a name="autoscaling-iam-role"></a>

Before you can use AppStream 2\.0 Fleet Auto Scaling, Application Auto Scaling needs permissions to access Amazon CloudWatch alarms and AppStream 2\.0 fleets\. The service role **ApplicationAutoscalingForAmazonAppStreamAccess** is automatically added to your IAM roles when you use the AppStream 2\.0 console\. If you plan to use the AWS CLI instead, you must create the following role\.

**Permissions**  

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

**Trust Relationship**  

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

To use AppStream 2\.0 Fleet Auto Scaling, the IAM user accessing fleet creation and settings must have appropriate permissions for the services that support scaling\. AppStream 2\.0 requires the following permissions:

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

AppStream 2\.0 adds an Amazon S3 bucket policy that prevents accidental deletion of the S3 bucket, shown below\. To delete the S3 bucket,delete the S3 bucket policy first, and then delete the S3 bucket\. For more information, see [Deleting or Emptying a Bucket](http://docs.aws.amazon.com/AmazonS3/latest/dev/delete-or-empty-bucket.html) in the *Amazon Simple Storage Service Developer Guide*\.

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

By default, administrators who can access the Amazon S3 bucket created by AppStream 2\.0 can view and modify content that is part of users' Home folders\. To restrict administrator access to the S3 bucket containing user files, we recommend applying the S3 bucket access policy based on the following policy template: 

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

This policy only allows Home folder S3 bucket access to the users specified and to the AppStream 2\.0 service\. For every IAM user who should have access, replicate the following line:

```
"arn:aws:iam::account:user/IAM-user-name"
```

For example, the following policy restricts access to the Home folder S3 bucket for anyone other than IAM users bobsmith and terrypratt, and the AppStream 2\.0 service, in region us\-west\-2 for account ID 123456789012\.

```
{
  "Sid": "RestrictedAccess",
  "Effect": "Deny",
  "NotPrincipal": 
  {
    "AWS": [
      "arn:aws:iam::123456789012:role/service-role/AmazonAppStreamServiceAccess",
      "arn:aws:sts::123456789012:assumed-role/AmazonAppStreamServiceAccess/PhotonSession",
      "arn:aws:iam::123456789012:user/bobsmith",
      "arn:aws:iam::123456789012:user/terrypratt"
    ]
  },
    "Action": "s3:*",
    "Resource": "arn:aws:s3:::appstream2-36fb080bb8-us-west-2-123456789012"
  }
 ]
}
```