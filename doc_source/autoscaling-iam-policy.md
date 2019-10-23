# Using IAM Policies to Manage Administrator Access to Application Auto Scaling<a name="autoscaling-iam-policy"></a>

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