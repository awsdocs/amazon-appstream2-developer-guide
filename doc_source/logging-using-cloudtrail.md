# Logging AppStream 2\.0 API Calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

Amazon AppStream 2\.0 is integrated with AWS CloudTrail\. CloudTrail is a service that provides a record of actions taken by a user, role, or an AWS service in AppStream 2\.0\. CloudTrail captures API calls for AppStream 2\.0 as events\. The calls captured include calls from the AppStream 2\.0 console and code calls to the AppStream 2\.0 API operations\. If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, including events for AppStream 2\.0\. If you don't configure a trail, you can still view the most recent events in the CloudTrail console in **Event history**\. You can use the information collected by CloudTrail to determine details such as request information\. For example, CloudTrail collects the following information: What request was made to AppStream 2\.0, the IP address from which the request was made, who made the request, and when it was made\. 

To learn more about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

## AppStream 2\.0 Information in CloudTrail<a name="service-name-info-in-cloudtrail"></a>

CloudTrail is enabled on your AWS account when you create the account\. When supported event activity occurs in AppStream 2\.0, that activity is recorded in a CloudTrail event along with other AWS service events in **Event history**\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing Events with CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\. 

For an ongoing record of events in your AWS account, including events for AppStream 2\.0, create a trail\. A *trail* enables CloudTrail to deliver log files to an Amazon S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all Regions in the AWS partition and delivers the log files to the Amazon S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs\. For more information, see the following: 
+ [Overview for Creating a Trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html#cloudtrail-aws-service-specific-topics-integrations)
+ [Configuring Amazon SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)
+ [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

AppStream 2\.0 supports logging the following actions as events in CloudTrail log files:
+ [AssociateFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_AssociateFleet.html)
+ [BatchAssociateUserStack](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_BatchAssociateUserStack.html)
+ [BatchDisassociateUserStack](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_BatchDisassociateUserStack.html)
+ [CopyImage](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CopyImage.html)
+ [CreateDirectoryConfig](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateDirectoryConfig.html)
+ [CreateFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateFleet.html)
+ [CreateImageBuilder](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateImageBuilder.html)
+ [CreateImageBuilderStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateImageBuilderStreamingURL.html)
+ [CreateStack](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStack.html)
+ [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html)
+ [DeleteDirectoryConfig](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteDirectoryConfig.html)
+ [DeleteFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteFleet.html)
+ [DeleteImage](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteImage.html)
+ [DeleteImageBuilder](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteImageBuilder.html)
+ [DeleteImagePermissions](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteImagePermissions.html)
+ [DeleteStack](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteStack.html)
+ [DescribeDirectoryConfigs](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeDirectoryConfigs.html)
+ [DescribeFleets](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeFleets.html)
+ [DescribeImageBuilders](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeImageBuilders.html)
+ [DescribeImagePermissions](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeImagePermissions.html)
+ [DescribeImages](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeImages.html)
+ [DescribeSessions](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeSessions.html)
+ [DescribeStacks](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeStacks.html)
+ [DescribeUserStackAssociations](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeUserStackAssociations.html)
+ [ExpireSession](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_ExpireSession.html)
+ [ListAssociatedFleets](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_ListAssociatedFleets.html)
+ [ListAssociatedStacks](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_ListAssociatedStacks.html)
+ [ListTagsForResource](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_ListTagsForResource.html)
+ [StartFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_StartFleet.html)
+ [StartImageBuilder](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_StartImageBuilder.html)
+ [StopFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_StopFleet.html)
+ [StopImageBuilder](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_StopImageBuilder.html)
+ [TagResource](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_TagResource.html)
+ [UntagResource](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UntagResource.html)
+ [UpdateDirectoryConfig](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UpdateDirectoryConfig.html)
+ [UpdateFleet](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UpdateFleet.html)
+ [UpdateImagePermissions](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UpdateImagePermissions.html)
+ [UpdateStack](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_UpdateStack.html)

Every event or log entry contains information about who generated the request\. The identity information helps you determine the following: 
+ Whether the request was made with root or AWS Identity and Access Management \(IAM\) user credentials\.
+ Whether the request was made with temporary security credentials for a role or federated user\.
+ Whether the request was made by another AWS service\.

For more information, see the [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

## Example: AppStream 2\.0 Log File Entries<a name="understanding-service-name-entries"></a>

 A trail is a configuration that enables delivery of events as log files to an Amazon S3 bucket that you specify\. CloudTrail log files contain one or more log entries\. An event represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. CloudTrail log files aren't an ordered stack trace of the public API calls, so they don't appear in any specific order\.

The following example shows a CloudTrail log entry that demonstrates the `AssociateFleet` event\.

```
{
  "eventVersion": "1.05",
  "userIdentity": {
    "type": "AssumedRole",
    "principalId": "AIDACKCEVSQ6C2EXAMPLE:janeroe",
    "arn": "arn:aws:sts:: 123456789012:assumed-role/Admin/janeroe",
    "accountId": "123456789012",
    "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
    "sessionContext": {
      "attributes": {
        "mfaAuthenticated": "false",
        "creationDate": "2019-03-12T06:41:50Z"
      },
      "sessionIssuer": {
        "type": "Role",
        "principalId": "AIDACKCEVSQ6C2EXAMPLE",
        "arn": "arn:aws:iam:: 123456789012:role/Admin",
        "accountId": "123456789012",
        "userName": "Admin"
      }
    }
  },
  "eventTime": "2019-03-12T06:58:09Z",
  "eventSource": "appstream.amazonaws.com",
  "eventName": "AssociateFleet",
  "awsRegion": "us-east-1",
  "sourceIPAddress": "198.51.100.15",
  "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.121 Safari/537.36",
  "requestParameters": {
    "fleetName": "ExampleFleet1",
    "stackName": "ExampleStack1"
  },
  "responseElements": null,
  "requestID": "3210a159-4494-11e9-8017-873084baf125",
  "eventID": "a6fbde60-a55a-46fe-87d4-89ead558dffd",
  "eventType": "AwsApiCall",
  "recipientAccountId": "123456789012"
}
```

The following example shows a CloudTrail log entry that demonstrates the `CreateImage` event when an image is created using the AppStream 2\.0 image builder\.

```
{
  "eventVersion": "1.05",
  "userIdentity": {
    "arn": "arn:aws:appstream:us-east-1: 123456789012:image-builder/ExampleImageBuilder",
    "accountId": "123456789012"
  },
  "eventTime": "2019-03-21T22:32:05Z",
  "eventSource": "appstream.amazonaws.com",
  "eventName": "CreateImage",
  "awsRegion": "us-east-1",
  "requestParameters": null,
  "responseElements": null,
  "eventID": "12b2d6e2-c9a9-402e-8886-2c388d3df610",
  "readOnly": false,
  "eventType": "AwsServiceEvent",
  "recipientAccountId": "123456789012",
  "serviceEventDetails": {
    "ImageName": "ExampleImage1",
    "ImagePlatform": "WINDOWS",
    "PublicBaseImageReleasedDate": "Tue Jan 15 22:19:56 UTC 2019",
    "ImageDisPlayName": "Example Image 1",
    "ImageBuilderSupported": "True",
    "ImageCreatedTime": "Thu Mar 21 22:32:05 UTC 2019",
    "ImageDescription": "Example image for testing",
    "ImageState": "PENDING"
  }
}
```