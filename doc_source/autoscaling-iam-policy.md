# Using IAM Policies to Manage Administrator Access to Application Auto Scaling<a name="autoscaling-iam-policy"></a>

Automatic scaling for fleets is made possible by a combination of the AppStream 2\.0, Amazon CloudWatch, and Application Auto Scaling APIs\. AppStream 2\.0 fleets are created with AppStream 2\.0, alarms are created with CloudWatch, and scaling policies are created with Application Auto Scaling\.

In addition to having the permissions defined in the [AmazonAppStreamFullAccess](managed-policies-required-to-access-appstream-resources.md) policy, the IAM user that accesses fleet scaling settings must have the required permissions for the services that support dynamic scaling\. IAM users must have permissions to use the actions shown in the following example policy\. 

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
          "iam:PassRole",
          "iam:ListRoles"
      ],
      "Resource": "*"
    }
  ]
}
```

You can also create your own IAM policies to set more specific permissions for calls to the Application Auto Scaling API\. For more information, see [Authentication and Access Control](https://docs.aws.amazon.com/autoscaling/application/userguide/auth-and-access-control.html) in the *Application Auto Scaling User Guide*\.