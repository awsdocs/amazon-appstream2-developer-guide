# Use the AppStream 2\.0 Dynamic Application Framework to Build a Dynamic App Provider<a name="build-dynamic-app-provider"></a>

The AppStream 2\.0 dynamic application framework provides API operations within an AppStream 2\.0 streaming instance that you can use to build a dynamic app provider\. Dynamic app providers can use the API operations provided to modify the catalog of applications that your users can access in real time\. The applications managed by the dynamic app providers can be within the image, or they can be off\-instance, such as from a Windows file share or an application virtualization technology\.

**Note**  
This feature requires an AppStream 2\.0 fleet that is joined to a Microsoft Active Directory domain\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

**Topics**
+ [About the Dynamic Application Framework](#about-dynamic-framework)
+ [Dynamic Application Framework Thrift Definitions and Named Pipe Name](#dynamic-application-framework-thrift-definitions)
+ [API Actions for Managing App Entitlement for AppStream 2\.0](#manage-app-entitlement-api-actions)

## About the Dynamic Application Framework<a name="about-dynamic-framework"></a>

The dynamic application framework uses the [Apache Thrift software framework](https://thrift.apache.org/) for inter\-process messaging\. It is exposed through Named Pipes in Windows\. Using the Thrift framework allows you to build your dynamic app provider in your software development language of choice\. The dynamic application framework consists of three API operations: `AddApplications`, `RemoveApplications`, and `ClearApplications`\. 

## Dynamic Application Framework Thrift Definitions and Named Pipe Name<a name="dynamic-application-framework-thrift-definitions"></a>

Thrift enables you to use simple definition files provided by AppStream 2\.0 to compile RPC clients\. The RPC clients let you communicate with the AppStream 2\.0 agent software running on a streaming instance\. For information about how to compile the RPC client for your language, see the [Apache Thrift documentation](https://thrift.apache.org/docs/)\. After you compile the Thrift libraries for the language of your choice, build a Thrift client by using the Named Pipe transport\. Use D56C0258\-2173\-48D5\-B0E6\-1EC85AC67893 as the pipe name\.

### AppStreamServer\.thrift<a name="appstream-server-thrift"></a>

```
namespace csharp AppStream.ApplicationCatalogService.Model

include "AppStreamServerMessages.thrift"

const string ServiceEndpoint = "D56C0258-2173-48D5-B0E6-1EC85AC67893";

service ApplicationCatalogService
{
    AppStreamServerMessages.AddApplicationsResponse AddApplications(1:AppStreamServerMessages.AddApplicationsRequest request)
    throws (1: AppStreamServerMessages.AppStreamClientException ce, 2: AppStreamServerMessages.AppStreamServerException se),

    AppStreamServerMessages.RemoveApplicationsResponse RemoveApplications(1:AppStreamServerMessages.RemoveApplicationsRequest request)
    throws (1: AppStreamServerMessages.AppStreamClientException ce, 2: AppStreamServerMessages.AppStreamServerException se),

    AppStreamServerMessages.ClearApplicationsResponse ClearApplications(1:AppStreamServerMessages.ClearApplicationsRequest request)
    throws (1: AppStreamServerMessages.AppStreamClientException ce, 2: AppStreamServerMessages.AppStreamServerException se),
}
```

### AppStreamServerMessages\.thrift<a name="appstream-server--messages-thrift"></a>

```
namespace csharp AppStream.ApplicationCatalogService.Model

struct AddApplicationsRequest
{
    1: required string userSid;
    2: required list<Application> applications;
}

struct AddApplicationsResponse
{
}

struct RemoveApplicationsRequest
{
    1: required string userSid; 
    2: required list<string> applicationIds;
}

struct RemoveApplicationsResponse
{
}

struct ClearApplicationsRequest
{
    1: required string userSid; 
}

struct ClearApplicationsResponse
{
}

struct Application
{
    1: required string id;
    2: required string displayName;
    3: required string launchPath;
    4: required string iconData;
    5: string launchParams;
    6: string workingDirectory;
}

exception AppStreamClientException
{
    1: string errorMessage,
    2: ErrorCode errorCode
}
	  
exception AppStreamServerException
{
    1: string errorMessage,
    2: ErrorCode errorCode
}

enum ErrorCode
{
}
```

## API Actions for Managing App Entitlement for AppStream 2\.0<a name="manage-app-entitlement-api-actions"></a>

You can use the following API operations to manage application entitlement for AppStream 2\.0\.

### `AddApplicationsRequest` operation<a name="manage-app-entitlement-api-addapplications-request"></a>

Adds applications to the application catalog for AppStream 2\.0 users\. The application catalog displayed by AppStream 2\.0 includes the applications that you add by using this API operation and the applications that you add in the image\. After you add applications by using one or both of these methods, your users can launch the applications\.

**Request syntax**

*string userSid;*

`list<Application> applications;`

**Request parameters**

***userSid***  
The SID of the user who the request applies to\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 208 characters\.

***applications***  
The list of applications that the request applies to\.  
**Type:** String  
**Required**: Yes

### `Application` object<a name="manage-app-entitlement-api-application-object"></a>

Describes the application metadata required to display and launch the application\. The application identifier must be unique and not in conflict with other applications specified through the API operation or the image\.

***id***  
The identifier of the application being specified\. This value, which corresponds to the `application_name` value in an AppStream 2\.0 applications report, is provided when a user launches the application\. When you enable [usage reports](enable-usage-reports.md), for each day that users launch at least one application during their streaming sessions, AppStream 2\.0 exports an applications report to your Amazon S3 bucket\. For more information about applications reports, see [Applications Report Fields](usage-reports-fields.md#usage-reports-fields-applications-reports)\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 512 characters\.

***displayName***  
The display name of the application being specified\. This name is displayed to the user in the application catalog\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 512 characters\.

***launchPath***  
The Windows file system path to the executable of the application to be launched\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 32,767 characters\.

***iconData***  
The base\-64 encoded image to display in the application catalog\. The image must be in one of the following formats: \.png, \.jpeg, or \.jpg\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 1,000,000 characters\.

***launchParams***  
The parameters used to launch the application\.  
**Type**: String  
**Required**: No  
**Length constraints:** Maximum length of 32,000 characters\.

***workingDirectory***  
The Windows file system path to the working directory the application should be launched in\.  
**Type**: String  
**Required**: No  
**Length constraints:** Maximum length of 32,767 characters\.

### `RemoveApplicationsRequest` operation<a name="manage-app-entitlement-api-removeapplications-request"></a>

Removes applications that were added by using the `AddApplicationsRequest` operation\. The applications are removed from the application catalog for the user\. After applications are removed, they can't be launched\. If an application is still running, AppStream 2\.0 does not close it\. Applications that are specified directly in the AppStream 2\.0 image can't be removed\.

**Request syntax**

*string userSid;*

`list<Application> applications;`

**Request parameters**

***userSid***  
The SID of the user the request applies to\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 208 characters\.

***applications***  
The list of applications that the request applies to\.  
**Type:** String  
**Required**: Yes

### `ClearApplicationsRequest` operation<a name="manage-app-entitlement-api-clearapplications-request"></a>

Removes all applications that were added to the application catalog by using the `AddApplicationsRequest` operation\. After applications are removed, they can't be launched\. If the applications are running when the `ClearApplicationsRequest` operation is used, AppStream 2\.0 does not close them\. Applications that are specified directly in the AppStream 2\.0 image can't be removed\.

**Request syntax**

*string userSid;*

**Request parameters**

***userSid***  
The SID of the user the request applies to\.  
**Type**: String  
**Required**: Yes  
**Length constraints:** Minimum length of 1, maximum length of 208 characters\.