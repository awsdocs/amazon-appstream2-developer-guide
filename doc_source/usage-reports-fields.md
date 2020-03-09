# AppStream 2\.0 Usage Reports Fields<a name="usage-reports-fields"></a>

This topic provides information about the fields included in AppStream 2\.0 usage reports\.

**Topics**
+ [Sessions Report Fields](#usage-reports-fields-sessions-reports)
+ [Applications Report Fields](#usage-reports-fields-applications-reports)

## Sessions Report Fields<a name="usage-reports-fields-sessions-reports"></a>

The following table describes the fields included in AppStream 2\.0 sessions reports\.


| Field name | Description | 
| --- | --- | 
| user\_session\_id | The unique identifier \(ID\) for the session\. | 
| aws\_account\_id | The AWS account ID\. | 
| region | The AWS Region\. | 
| session\_start\_time | The date and time that the session started\. Format: ISO 8601 \(UTC\) | 
| session\_end\_time | The date and time that the session ended\. Format: ISO 8601 \(UTC\) | 
| session\_duration\_in\_seconds | The duration of the session in seconds\. | 
| user\_id | The unique ID for the user within the authentication type\. | 
| user\_arn | The Amazon Resource Name \(ARN\) for the user\. | 
| authentication\_type | The method used to authenticate the user\. Possible values: CUSTOM \| SAML \| USERPOOL | 
| authentication\_type\_user\_id | The concatenation of the user ID and authentication type, which uniquely identify the user for the purpose of assessing user fees\. For more information, see [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\. | 
| fleet\_name | The name of the fleet associated with the session\. | 
| stack\_name | The name of the stack associated with the session\. | 
| instance\_type | The AppStream 2\.0 instance type used for the session\. For a list of instance types, see [AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\. | 
| eni\_private\_ip\_address | The IP address of the elastic network interface used by the AppStream 2\.0 instance for network communications\. | 
| connected\_at\_least\_once | Indicates whether the user connected to the session at least once\. Possible values: true \| false | 
| client\_ip\_addresses | The IP addresses associated with the user device or devices used to connect to the session\. If the user connected and then disconnected from the session more than once, up to the last 10 distinct IP addresses are stored, separated by semicolons\. | 
| google\_drive\_enabled | Indicates whether Google Drive was enabled as a persistent storage option for the session\. For more information, see [Enable and Administer Google Drive for Your AppStream 2\.0 Users](google-drive.md)\.  Possible values: true \| false | 
| one\_drive\_enabled | Indicates whether OneDrive was enabled as a persistent storage option for the session\. For more information, see [Enable and Administer Google Drive for Your AppStream 2\.0 Users](google-drive.md)\.  Possible values: true \| false | 
| home\_folders\_storage\_location | The Amazon S3 bucket used for files that are stored using home folders\. | 
| user\_settings\_clipboard\_copy\_from\_local\_device | Indicates whether the user was able to copy data from the local device to the streaming session using the clipboard during the session\. Possible values: ENABLED \| DISABLED | 
| user\_settings\_clipboard\_copy\_to\_local\_device | Indicates whether the user was able to copy data from the streaming session to the local device using the clipboard during the session\. Possible values: ENABLED \| DISABLED | 
| user\_settings\_file\_upload | Indicates whether the user was able to upload files from the local device to the streaming session during the session\. Possible values: ENABLED \| DISABLED | 
| user\_settings\_file\_download | Indicates whether the user was able to download files from the streaming session to the local device during the session\. Possible values: ENABLED \| DISABLED | 
| user\_settings\_printing\_to\_local\_device | Indicates whether the user was able to print files from the streaming session to the local device during the session\. Possible values: ENABLED \| DISABLED | 
| application\_settings\_enabled | Indicates whether application settings persistence was enabled for the session\. Possible values: true \| false  | 
| domain\_joined | Indicates whether the AppStream 2\.0 streaming instance was joined to an Active Directory domain at session launch\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.  Possible values: Y \| N  | 
| max\_session\_duration | The maximum allowed duration of the session in seconds\. | 
| session\_type | The session type\. Possible values: ALWAYS\_ON \| ON\_DEMAND | 
| schedule | The frequency that reports are generated\. Possible value: DAILY | 
| year | The year of the report\.  | 
| month | The month of the report\.  | 
| day | The day of the report\.  | 

## Applications Report Fields<a name="usage-reports-fields-applications-reports"></a>

The following table describes the fields included in AppStream 2\.0 applications reports\.


| Field name | Description | 
| --- | --- | 
| user\_session\_id | The unique identifier \(ID\) for the session\. | 
| application\_name | The name of the application, as specified in Image Assistant\. This value is provided when a user launches an application\.  | 
| schedule | The frequency with which reports are generated\. Possible value: DAILY | 
| year | The year of the report\.  | 
| month | The month of the report\.  | 
| day | The day of the report\.  | 