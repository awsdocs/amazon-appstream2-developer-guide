# Manage Access with IAM<a name="controlling-access"></a>

An AWS Identity and Access Management \(IAM\) *policy* is an object in AWS that, when associated with an identity or resource, defines its permissions\. An IAM *role* is an identity that you create in your AWS account\. You can attach policies to an IAM role to control what actions the role can perform, on which resources, and under what conditions\. This topic describes how to use IAM policies and roles to manage the permissions required to perform key AppStream 2\.0 management tasks, and how to manage access to AppStream 2\.0 resources\.

**Topics**
+ [Using AWS Managed Policies and Service\-Linked Roles to Manage Administrator Access to AppStream 2\.0 Resources](controlling-administrator-access-with-policies-service-linked-roles.md)
+ [Using IAM Policies to Manage Administrator Access to Application Auto Scaling](autoscaling-iam-policy.md)
+ [Using IAM Policies to Manage Administrator Access to the Amazon S3 Bucket for Home Folders and Application Settings Persistence](s3-iam-policy.md)
+ [Using an IAM Role to Grant Permissions to Applications and Scripts Running on AppStream 2\.0 Streaming Instances](using-iam-roles-to-grant-permissions-to-applications-scripts-streaming-instances.md)