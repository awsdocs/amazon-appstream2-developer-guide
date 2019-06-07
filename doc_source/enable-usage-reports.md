# Enable AppStream 2\.0 Usage Reports<a name="enable-usage-reports"></a>

To receive usage reports, you subscribe to them by using the AppStream 2\.0 console, the AWS Command Line Interface \(AWS CLI\), or the `CreateUsageReportSubscription` API operation\. You must enable usage reports separately for each AWS Region for which you want to receive usage data\.

**Note**  
You can start or stop your subscription to usage reports at any time\. There is no charge for subscribing to usage reports, but standard Amazon S3 charges may apply to reports that are stored in your S3 bucket\. For more information, see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)\.

To subscribe to usage reports for AppStream 2\.0 by using the AppStream 2\.0 console, perform the following steps\. 

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose the AWS Region for which you want to enable usage reports\.

1. In the navigation pane, choose **Usage Reports**\.

1. Choose **Enabled**, and then choose **Apply**\.

If you enabled on\-instance session scripts and Amazon S3 logging for your session script configuration, AppStream 2\.0 created an S3 bucket to store the script output\. The bucket is unique to your account and Region\. When you enable usage reporting in this case, AppStream 2\.0 uses the same bucket to store your usage reports\. If you haven't already enabled on\-instance session scripts, when you enable usage reports, AppStream 2\.0 creates a new S3 bucket in the following location:

```
appstream-logs-region-code-account-id-without-hyphens-random-identifier
```

***region\-code***  
The AWS Region code for the Region in which usage reporting is enabled\.

***account\-id\-without\-hyphens***  
Your AWS account identifier\. The random ID ensures that there is no conflict with other buckets in the same Region\. The first part of the bucket name, `appstream-logs`, does not change across accounts or Regions\.

For example, if you enable usage reporting in the US West \(Oregon\) Region \(us\-west\-2\) on account number 123456789012, AppStream 2\.0 creates an Amazon S3 bucket within your account in that Region similar to the name shown in the following example: 

```
appstream-logs-us-west-2-1234567890123-abcdefg
```

Only an administrator with sufficient permissions can delete this bucket\.

## AppStream 2\.0 Sessions Reports<a name="usage-report-types-sessions-reports"></a>

For each day that users launch at least one streaming session in your AWS account, AppStream 2\.0 exports a sessions report to your Amazon S3 bucket\. The report, named **daily\-session\-report\-\[YYYY\]\-\[MM\]\-\[DD\]\.csv**, is stored in a nested folder structure in your Amazon S3 account, using the following folder path:

\[bucket\_name\]/sessions/schedule=DAILY/year=\[YYYY\]/month=\[MM\]/day=\[DD\]/

This nesting structure facilitates partitioning if you choose to query your reports by using Amazon Athena\. Athena is a serverless, interactive query service that you can use to analyze data stored in your S3 buckets using standard SQL\. For more information, see [Create Custom Reports and Analyze AppStream 2\.0 Usage Data](configure-custom-reports-analyze-usage-data.md)\.

Each user session is described in a single record in a sessions report\. Sessions reports are generated daily according to UTC time within 24 hours of the close of the day that is the subject of the report\. If a session spans more than one day, the session record appears in the sessions report corresponding to the day in which the session ends\. For information about the data included in sessions reports, see [Sessions Report Fields](usage-reports-fields.md#usage-reports-fields-sessions-reports)\. 

## AppStream 2\.0 Applications Reports<a name="usage-report-types-applications-reports"></a>

For each day that users launch at least one application during their streaming sessions, AppStream 2\.0 exports an applications report to your Amazon S3 bucket\. The report, named **daily\-app\-report\-\[YYYY\]\-\[MM\]\-\[DD\]\.csv**, is stored in a nested folder structure in your Amazon S3 account, using the following folder path:

\[bucket\_name\]/applications/schedule=DAILY/year=\[YYYY\]/month=\[MM\]/day=\[DD\]/

This nesting structure facilitates partitioning if you choose to query your reports by using Amazon Athena\. Athena is a serverless, interactive query service that you can use to analyze data stored in your S3 buckets using standard SQL\. For more information, see [Create Custom Reports and Analyze AppStream 2\.0 Usage Data](configure-custom-reports-analyze-usage-data.md)\.

Each application launch is described in a single record in an applications report\. For example, if a user launches five separate applications during a session, five separate records appear in the relevant applications report\. An application is recorded as launched if any of the following events occurs:
+ The application is launched directly when the session begins, because the application ID is embedded in either the streaming URL or the relay state\.
+ A user chooses the application from the application catalog when launching a new streaming session\.
+ A user chooses the application from the application catalog list during a streaming session\.

The applications report doesn’t include applications that are launched in other ways\. For example, if you provide users with access to Windows Explorer or PowerShell, and users use those tools to launch applications directly, or if another program or script launches an application, those application launches are not included in the applications report\.

Applications reports are generated daily according to UTC time within 24 hours of the close of the day that is the subject of the report\. If a session spans more than one day, applications launched during the session are reflected in the applications report corresponding to the day in which the session ends\. For information about the data included in applications reports, see [Applications Report Fields](usage-reports-fields.md#usage-reports-fields-applications-reports)\. 