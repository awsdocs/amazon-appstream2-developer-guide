# Store Application Icon, Setup Script, Session Script, and VHD in S3 Bucket<a name="store-s3-bucket"></a>

You must store the application icons, setup scripts, session scripts, and VHDs that you use for your applications and app blocks in an Amazon Simple Storage Service \(Amazon S3\) bucket in your AWS account\. AppStream 2\.0 Elastic fleets download the application icon, setup script, and VHD from the S3 bucket when your user starts their streaming session\. The S3 bucket must reside in the AWS Region that you intend to create AppStream 2\.0 Elastic fleets within\.

We recommend that you create a new S3 bucket that is used to store only the application icons, setup scripts, session scripts, and VHDs that you intend to use with Elastic fleets\. We also recommend enabling versioning on the S3 bucket\. This allows reverting to previous object versions if necessary\. For more information about how to create a new S3 bucket, see [Creating a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)\. For more information about how to manage object versioning, see [Using versioning in S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)\.

**Note**  
AppStream 2\.0 uses your VPC to access the S3 bucket you select\. The VPC you choose for your fleet must provide sufficient network access to the S3 bucket\.

## S3 Bucket Permissions<a name="s3-permissions"></a>

The S3 bucket that you choose must have a bucket policy that provides sufficient access to the AppStream 2\.0 service principal to access and download objects from the S3 bucket\. You will need to modify the below bucket policy then apply it to the S3 bucket you intend to use for application icons, setup scripts, and VHDs\. For more information about how to apply a policy to an S3 bucket, see [Adding a bucket policy using the Amazon S3 console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html)\.

```
{ 
  "Version": "2012-10-17",
  "Statement": [     
      { 
       "Sid": "AllowAppStream2.0ToRetrieveObjects", 
       "Effect": "Allow", 
       "Principal": { 
          "Service": ["appstream.amazonaws.com"]         
        },
        "Action": ["s3:GetObject"],
        "Resource": [           
           "arn:aws:s3:::bucket/VHD object",
           "arn:aws:s3:::bucket/Setup script object",
           "arn:aws:s3:::bucket/Application icon object"
           "arn:aws:s3:::bucket/Session scripts zip file object"
         ]         
      }      
  ]
}
```

**Note**  
The bucket policy example defines specific objects in the S3 bucket that AppStream 2\.0 can access\. You can also use prefixes and wildcards to simplify policy management as you increase your app blocks\. For more information about bucket policies, see [Using bucket policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html)\. For more information about common bucket examples, see [Bucket policy examples](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html)\.