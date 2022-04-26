# Using Amazon S3 VPC Endpoints for AppStream 2\.0 Features<a name="managing-network-vpce-iam-policy"></a>

When you enable Application Settings Persistence or Home folders on a stack, AppStream 2\.0 uses the VPC you specify for your fleet to provide access to Amazon Simple Storage Service \(Amazon S3\) buckets\. For Elastic fleets, AppStream 2\.0 will use the VPC to access the Amazon S3 bucket containing applications assigned to the fleet's app block\. To enable AppStream 2\.0 access to your private S3 endpoint, attach the following custom policy to your VPC endpoint for Amazon S3\. For more information about private Amazon S3 endpoints, see [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html) and [Endpoints for Amazon S3](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-s3.html) in the *Amazon VPC User Guide*\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-AppStream-to-access-S3-buckets",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:sts::account-id-without-hyphens:assumed-role/AmazonAppStreamServiceAccess/AppStream2.0"
      },
      "Action": [
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject",
        "s3:GetObjectVersion",
        "s3:DeleteObjectVersion"
      ],
      "Resource": [
        "arn:aws:s3:::appstream2-36fb080bb8-*",
        "arn:aws:s3:::appstream-app-settings-*",
	"arn:aws:s3:::bucket-with-application-or-app-block-objects"
      ]
    }
  ]
}
```