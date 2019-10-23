# Using IAM Policies to Manage Administrator Access to the Amazon S3 Bucket for Home Folders and Application Settings Persistence<a name="s3-iam-policy"></a>

The following examples show how you can use IAM policies to manage access to the Amazon S3 bucket for home folders and application settings persistence\.

**Topics**
+ [Deleting the Amazon S3 Bucket for Home Folders and Application Settings Persistence](#s3-iam-policy-delete)
+ [Restricting Administrator Access to the Amazon S3 Bucket for Home Folders and Application Settings Persistence](#s3-iam-policy-restricted-access)

## Deleting the Amazon S3 Bucket for Home Folders and Application Settings Persistence<a name="s3-iam-policy-delete"></a>

AppStream 2\.0 adds an Amazon S3 bucket policy to the buckets that it creates to prevent them from being accidentally deleted\. To delete an S3 bucket, you must first delete the S3 bucket policy\. Following are the bucket policies that you must delete for home folders and application settings persistence\.

**Home folders policy**

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

**Application settings persistence policy**

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PreventAccidentalDeletionOfBucket",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:DeleteBucket",
      "Resource": "arn:aws:s3:::appstream-app-settings-region-code-account-id-without-hyphens-unique-identifier"
     }
   ]
}
```

 For more information, see [Deleting or Emptying a Bucket](https://docs.aws.amazon.com/AmazonS3/latest/dev/delete-or-empty-bucket.html) in the *Amazon Simple Storage Service Developer Guide*\.

## Restricting Administrator Access to the Amazon S3 Bucket for Home Folders and Application Settings Persistence<a name="s3-iam-policy-restricted-access"></a>

By default, administrators who can access the Amazon S3 buckets created by AppStream 2\.0 can view and modify content that is part of users' home folders and persistent application settings\. To restrict administrator access to the S3 buckets that contain user files, we recommend applying the S3 bucket access policy based on the following template: 

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
    "Resource": "arn:aws:s3:::home-folder-or-application-settings-persistence-s3-bucket-region-account"
  }
 ]
}
```

This policy allows S3 bucket access only to the users specified and to the AppStream 2\.0 service\. For every IAM user who should have access, replicate the following line:

```
"arn:aws:iam::account:user/IAM-user-name"
```

In the following example, the policy restricts access to the home folder S3 bucket for anyone other than IAM users marymajor and johnstiles\. It also allows access to the AppStream 2\.0 service, in AWS Region US West \(Oregon\) for account ID 123456789012\.

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