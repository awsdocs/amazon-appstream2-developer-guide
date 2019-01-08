# Example API Operations Work Flow for the Dynamic Application Framework<a name="manage-app-entitlement-sample-api-workflow"></a>

The following diagram is an example of the API operations flow between AppStream 2\.0 and a third\-party application provider\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/dynamic-app-provider-process-diagram4.png)

1. The user connects to AppStream 2\.0\. A fleet streaming instance is assigned to the user and Windows login occurs\.

1. Your service or agent detects the Windows logon event and determines the user who is logging in to Windows\.

1. The service or agent fetches the application entitlements for the user\. In the example diagram, the application entitlements are stored in a database\. This information can be stored and retrieved in different ways\. For example, application entitlements may be fetched from server software, or group names in Active Directory may be parsed to locate the application identifiers \(IDs\)\.

1. Your dynamic app provider calls the AppStream 2\.0 agent `AddApplications` API operation with the application metadata for the applications that the user should have\.

1. The AppStream 2\.0 agent dynamically updates the application catalog with the modified application list\.

1. The user selects an application to launch\. 

1. The application is launched by using the application metadata specified by your service or agent\.

From the user’s perspective, the process happens transparently\. The user connects to AppStream 2\.0 and logs in to the fleet instance\. After login, the list of applications specified in the image and provided by your dynamic app provider displays for the user\.