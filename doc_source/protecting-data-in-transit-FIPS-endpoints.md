# Protecting Data in Transit with FIPS Endpoints<a name="protecting-data-in-transit-FIPS-endpoints"></a>

 By default, when you communicate with the AppStream 2\.0 service, whether as an administrator using the AppStream 2\.0 console, the AWS Command Line Interface \(AWS CLI\), or an AWS SDK, or as a user streaming from an image builder or a fleet instance, all data in transit is encrypted using SSL\.

Alternatively, AppStream 2\.0 offers FIPS\-compliant endpoints \(FIPS endpoints\) in all United States AWS Regions where AppStream 2\.0 is available\. When you use a FIPS endpoint, all data in transit is encrypted using cryptographic standards that comply with Federal Information Processing Standard \(FIPS\) 140\-2\. For information about FIPS endpoints, including a list of AppStream 2\.0 endpoints, see [Federal Information Processing Standard \(FIPS\) 140\-2](https://aws.amazon.com/compliance/fips)\.

## FIPS Endpoints for Administrative Use<a name="FIPS-for-administrative-use"></a>

To specify a FIPS endpoint when you run an AWS CLI command for AppStream 2\.0, use the `endpoint-url` parameter\. The following example uses the AppStream 2\.0 FIPS endpoint in the US West \(Oregon\) Region to retrieve a list of all stacks in the Region:

```
aws appstream describe-stacks --endpoint-url https://appstream2-fips.us-west-2.amazonaws.com
```

To specify a FIPS endpoint for AppStream 2\.0 API operations, use the procedure in your AWS SDK for specifying a custom endpoint\.

## FIPS Endpoints for User Streaming Sessions<a name="FIPS-for-user-streaming-sessions"></a>

If you use SAML 2\.0 or a streaming URL to authenticate users, you can configure FIPS\-compliant connections for your users' streaming sessions\.

To use a FIPS\-compliant connection for users who authenticate using SAML 2\.0, specify an AppStream 2\.0 FIPS endpoint when you configure the relay state of your federation\. For more information about constructing a relay state URL for identity federation using SAML 2\.0, see [Setting Up SAML](external-identity-providers-setting-up-saml.md)\.

To configure a FIPS\-compliant connection for users who authenticate through a streaming URL, specify an AppStream 2\.0 FIPS endpoint when you call the [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) or [CreateImageBuilderStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateImageBuilderStreamingURL.html) operation from the AWS CLI or an AWS SDK\. A user who connects to a streaming instance using the resulting URL is connected through a FIPS\-compliant connection\. The following example uses the AppStream 2\.0 FIPS endpoint in the US East \(Virginia\) Region to generate a FIPS\-compliant streaming URL:

```
aws appstream create-streaming-url --stack-name stack-name --fleet-name fleet-name --user-id user-id --endpoint-url https://appstream2-fips.us-east-1.amazonaws.com
```

## Exceptions<a name="FIPS-exceptions"></a>

FIPS\-compliant connections are not supported in the following scenarios:
+ Administration of AppStream 2\.0 through the AppStream 2\.0 console
+ Streaming sessions for users who authenticate using the AppStream 2\.0 user pool feature
+ Streaming using an interface VPC endpoint
+ Generating FIPS\-compliant streaming URLs through the AppStream 2\.0 console
+ Connections to your Google Drive or OneDrive storage accounts where your storage provider does not provide a FIPS endpoint