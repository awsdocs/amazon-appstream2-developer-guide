# Applications<a name="applications-elastic"></a>

Applications contain the details necessary to launch your application after the VHD has been mounted\. Applications also include the name and icon that are displayed to your user on the application catalog\. Applications are associated with the app block resource that contains the files and binaries for that application\.

You can use the AppStream 2\.0 console to create the application resource once you have uploaded your application icon to an Amazon S3 bucket and created the app block that contains the files and folders necessary to launch the application\. To learn more about uploading the application icon to an Amazon S3 bucket, see [Store Application Icon, Setup Script, Session Script, and VHD in S3 Bucket](store-s3-bucket.md)\.

**Note**  
You must have IAM permissions to perform the `S3:GetObject` action on the application icon object in the S3 bucket to create the application resource\.

**To create the application resource**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. From the left\-hand navigation menu, choose **Applications** and **Create application**\.

1. For **Name** under **Application details**, enter a unique identifier for the application\.

1. \(Optional\) For **Display name** under **Application details**, enter a friendly name that users will see in the application catalog\.

1. \(Optional\) For **Description** under **Application details**, enter a description for the application\.

1. For **Application icon object in S3** under **Application details**, either enter the S3 URI that represents the VHD object, or choose **Browse S3** to navigate to your S3 buckets and find the application icon object\.

1. For **Application executable launch path** under **Application settings**, enter the path on the streaming instance to the application’s executable\.

1. \(Optional\) For **Application working directory** in the **Application settings** section, enter the directory on the streaming instance to use for the application's working directory\.

1. \(Optional\) For **Application launch parameters** in the **Application settings** section, enter the parameters to provide to the application executable when launching the application\.

1. For **Supported operating systems \(OS\)** in the **Application settings** section, choose which operating systems can launch this application\.

1. For **Supported instance families** in the **Application settings** section, choose which instance families can launch this application\.

1. For **App block** in the **Application settings** section, choose which app block contains the files and folders necessary for this application\.

1. \(Optional\) In the **Tags** section, create tags for the app block resource\.

1. Review the information that you entered, then choose **Create**\.

1. If your application was created successfully, you will see a success message at the top of the console\. If an error occurred, a descriptive error message will be provided and you will need to try creating the application again\.