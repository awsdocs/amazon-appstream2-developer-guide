# Troubleshooting Notification Codes<a name="troubleshooting-notification-codes"></a>

The following are notification codes and resolution steps for notifications you may see while setting up and using Amazon AppStream 2\.0\. These notifications can be found in the **Notifications** tab in the AppStream 2\.0 console, after selecting an image builder or fleet\. Fleet notifications can also be obtained using the AppStream 2\.0 API operation [DescribeFleets](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeFleets.html), or using the [describe\-fleets](http://docs.aws.amazon.com/cli/latest/reference/appstream/describe-fleets.html) CLI command\.

## Active Directory Domain Join<a name="troubleshooting-notification-codes-ad"></a>

The following are notification codes and resolution steps for codes you might encounter while setting up and using Active Directory with Amazon AppStream 2\.0\. 

**DOMAIN\_JOIN\_ERROR\_ACCESS\_DENIED**  
**Message**: Access is denied\.  
**Resolution**: The service account specified in the directory configuration does not have permissions to create the computer object, or reuse an existing one\. Validate the permissions and start the image builder or fleet\. For more information, see [Granting Permissions to Create and Manage Active Directory Computer Objects](active-directory-admin.md#active-directory-permissions)\.

**DOMAIN\_JOIN\_ERROR\_LOGON\_FAILURE**  
**Message**: The username or password is incorrect\.  
**Resolution**: The service account specified in the directory configuration has an invalid username or password\. Update the configuration and re\-create the image builder or fleet that had the error\.

**DOMAIN\_JOIN\_NERR\_PASSWORD\_EXPIRED**  
**Message**: The password of this user has expired\.  
**Resolution**: The password for the service account specified in the AppStream 2\.0 directory configuration has expired\. Change the password for the service account in your Active Directory domain, then update the configuration, and re\-create the image builder or fleet that had the error\.

**DOMAIN\_JOIN\_ERROR\_DS\_MACHINE\_ACCOUNT\_QUOTA\_EXCEEDED**  
**Message**: Your computer could not be joined to the domain\. You have exceeded the maximum number of computer accounts you are allowed to create in this domain\. Contact your system administrator to have this limit reset or increased\.  
**Resolution**: The service account specified on the directory configuration does not have permissions to create the computer object, or reuse an existing one\. Validate the permissions and start the image builder or fleet\. For more information, see [Granting Permissions to Create and Manage Active Directory Computer Objects](active-directory-admin.md#active-directory-permissions)\.

**DOMAIN\_JOIN\_ERROR\_INVALID\_PARAMETER**  
**Message**: A parameter is incorrect\. This error is returned if the LpName parameter is NULL or the NameType parameter is specified as NetSetupUnknown or an unknown nametype\.  
**Resolution**: This error can occur when the distinguished name for the OU is incorrect\. Validate the OU chosen\. If you continue to encounter this error, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**DOMAIN\_JOIN\_ERROR\_MORE\_DATA**  
**Message**: More data is available\.  
**Resolution**: This error can occur when the distinguished name for the OU is incorrect\. Validate the OU chosen\. If you continue to encounter this error, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**DOMAIN\_JOIN\_ERROR\_NO\_SUCH\_DOMAIN**  
**Message**: The specified domain either does not exist or could not be contacted\.  
**Resolution**: The streaming instance was unable to contact your Active Directory domain\. To ensure network connectivity, confirm your VPC, subnet, and security group settings\. For more information, see [My AppStream 2\.0 streaming instances aren't joining the Active Directory domain\.](troubleshooting-active-directory.md#troubleshooting-active-directory-5)\.

**DOMAIN\_JOIN\_NERR\_WORKSTATION\_NOT\_STARTED**  
**Message**: The Workstation service has not been started\.  
**Resolution**: An error occurred starting the Workstation service\. Ensure that the service is enabled in your image\. If you continue to encounter this error, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**DOMAIN\_JOIN\_ERROR\_NOT\_SUPPORTED**  
**Message**: The request is not supported\. This error is returned if a remote computer was specified in the lpServer parameter and this call is not supported on the remote computer\.  
**Resolution**: Contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**DOMAIN\_JOIN\_ERROR\_FILE\_NOT\_FOUND**  
**Message**: The system cannot find the file specified\.  
**Resolution**: This error occurs when an invalid organizational unit \(OU\) distinguished name is provided\. The distinguished name must start with **OU=**\. Validate the OU distinguished name and try again\. For more information, see [Finding the Organizational Unit Distinguished Name](active-directory-admin.md#active-directory-oudn)\.