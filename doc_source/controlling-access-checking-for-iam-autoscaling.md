# Checking for the ApplicationAutoScalingForAmazonAppStreamAccess Service Role and Policies<a name="controlling-access-checking-for-iam-autoscaling"></a>

Complete the steps in this section to check whether the **ApplicationAutoScalingForAmazonAppStreamAccess** service role is present and has the correct policies attached\. If this role is not in your account and must be created, you or an administrator with the required permissions must perform the steps to get started with AppStream 2\.0 in your AWS account\.

**To check whether the ApplicationAutoScalingForAmazonAppStreamAccess IAM service role is present**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Roles**\. 

1. In the search box, type **applicationautoscaling** to narrow the list of roles to select, and then choose **ApplicationAutoScalingForAmazonAppStreamAccess**\. If this role is listed, select it to view the role **Summary** page\. 

1. On the **Permissions** tab, confirm whether the **ApplicationAutoScalingForAmazonAppStreamAccess** permissions policy is attached\. 

1. Return to the role **Summary** page\.

1. On the **Trust relationships** tab, choose **Show policy document**, and then confirm whether the **ApplicationAutoScalingForAmazonAppStreamAccess** trust relationship policy is attached and follows the correct format\. If so, the trust relationship is correctly configured\. Choose **Cancel** and close the IAM console\. 

## ApplicationAutoScalingForAmazonAppStreamAccess trust relationship policy<a name="controlling-access-autoscaling-trust-policy"></a>

The **ApplicationAutoScalingForAmazonAppStreamAccess** trust relationship policy must include the Application Auto Scaling service as the principal\. This policy must also include the `sts:AssumeRole` action\. The following policy configuration defines Application Auto Scaling as a trusted entity\.

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