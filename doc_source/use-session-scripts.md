# Use Session Scripts to Manage Your AppStream 2\.0 Users' Streaming Experience<a name="use-session-scripts"></a>

AppStream 2\.0 provides on\-instance session scripts\. You can use these scripts to run your own custom scripts when specific events occur in users' streaming sessions\. For example, you can use custom scripts to prepare your AppStream 2\.0 environment before your users' streaming sessions begin\. You can also use custom scripts to clean up streaming instances after users complete their streaming sessions\. 

Session scripts are specified within an AppStream 2\.0 image\. These scripts are run within the user context or the system context\. If your session scripts use the standard out to write information, error, or debugging messaging, these can be optionally saved to an Amazon S3 bucket within your AWS account\.

**Topics**
+ [Run Scripts Before Streaming Sessions Begin](#run-scripts-before-streaming-sessions-begin)
+ [Run Scripts After Streaming Sessions End](#run-scripts-after-streaming-sessions-end)
+ [Create and Specify Session Scripts](#create-specify-session-scripts)
+ [Session Scripts Configuration File](#session-script-configuration-file)
+ [Using Windows PowerShell Files](#using-powershell-files-with-session-scripts)
+ [Logging Session Script Output](#logging-session-output)
+ [Use Storage Connectors with Session Scripts](#use-storage-connectors-with-session-scripts)
+ [Enable Amazon S3 Bucket Storage for Session Script Logs](#enable-S3-bucket-storage-session-script-logs)

## Run Scripts Before Streaming Sessions Begin<a name="run-scripts-before-streaming-sessions-begin"></a>

You can configure your scripts to run for a maximum of 60 seconds before your users' applications launch and their streaming sessions begin\. Doing so enables you to customize the AppStream 2\.0 environment before users start streaming their applications\. When the session scripts run, a loading spinner displays for your users\. When your scripts complete successfully or the maximum waiting time elapses, your users' streaming session will begin\. If your scripts don't complete successfully, an error message displays for your users\. However, your users are not prevented from using their streaming session\.

When you specify a file name, you must use a double backslash\. For example:

C:\\\\Scripts\\\\Myscript\.bat

If you don't use a double backslash, an error displays to notify you that the \.json file is incorrectly formatted\.

**Note**  
When your scripts complete successfully, they must return a value of 0\. If your scripts return a value other than 0, AppStream 2\.0 displays the error message to the user\. 

When you run scripts before streaming sessions begin and the AppStream 2\.0 dynamic application framework is not enabled, the following process occurs:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/session-scripts-without-DAF-non-domain-joined2.png)

1. Your users connect to an AppStream 2\.0 fleet instance that is not domain\-joined\. They connect by using one of the following access methods:
   + AppStream 2\.0 user pool
   + SAML 2\.0
   + AppStream 2\.0 API

1. The application catalog displays in the AppStream 2\.0 portal, and your users choose an application to launch\.

1. One of the following occurs:
   + If application settings persistence is enabled for your users, the application settings Virtual Hard Disk \(VHD\) file that stores your users' customizations and Windows settings is downloaded and mounted\. Windows user login is required in this case\.

     For information about application settings persistence, see [Enable Application Settings Persistence for Your AppStream 2\.0 Users](app-settings-persistence.md)\.
   + If application settings persistence is not enabled, the Windows user is already logged in\.

1. Your session scripts start\. If persistent storage is enabled for your users, storage connector mounting also starts\. For information about persistent storage, see [Enable and Administer Persistent Storage for Your AppStream 2\.0 Users](persistent-storage.md)\.
**Note**  
The storage connector mount doesn't need to complete for the streaming session to start\. If the session scripts complete before the storage connector mount completes, the streaming session starts\.   
For information about monitoring the mount status of storage connectors, see [Use Storage Connectors with Session Scripts](#use-storage-connectors-with-session-scripts)\.

1. Your session scripts complete or time out\.

1. The users' streaming session starts\. 

1. The application that your users chose launches\.

For information about the AppStream 2\.0 dynamic application framework, see [Use the AppStream 2\.0 Dynamic Application Framework to Build a Dynamic App Provider](build-dynamic-app-provider.md)\.

When you run scripts before streaming sessions begin and the AppStream 2\.0 dynamic application framework is enabled, the following process occurs:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/session-scripts-with-DAF-domain-joined2.png)

1. Your users visit the SAML 2\.0 application portal for your organization, and they choose the AppStream 2\.0 stack\.

1. They connect to an AppStream 2\.0 fleet instance that is domain\-joined\.

1. If application settings persistence is enabled for your users, the application settings VHD file that stores your users' customizations and Windows settings is downloaded and mounted\.

1. Windows user logon occurs\.

1. The application catalog displays in the AppStream 2\.0 portal and your users choose an application to launch\.

1. Your session scripts start\. If persistent storage is enabled for your users, storage connector mounting also starts\.
**Note**  
The storage connector mount doesn't need to complete for the streaming session to start\. If the session scripts complete before the storage connector mount completes, the streaming session starts\.   
For information about monitoring the mount status of storage connectors, see [Use Storage Connectors with Session Scripts](#use-storage-connectors-with-session-scripts)\.

1. Your session scripts complete or time out\.

1. The users' streaming session starts\.

1. The application that your users chose launches\.

## Run Scripts After Streaming Sessions End<a name="run-scripts-after-streaming-sessions-end"></a>

You can also configure your scripts to run after users' streaming sessions end\. For example, you can run a script when users select **End Session** from the AppStream 2\.0 toolbar, or when they reach the maximum allowed duration for the session\. You can also use these session scripts to clean up your AppStream 2\.0 environment before a streaming instance is terminated\. For example, you can use scripts to release file locks or upload log files\. When you run scripts after streaming sessions end, the following process occurs:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/session-scripts-termination.png)

1. Your users' AppStream 2\.0 streaming session ends\.

1. Your session termination scripts start\.

1. The session termination scripts complete or time out\.

1. Windows user logout occurs\. 

1. One or both of the following occur in parallel, if applicable:
   + If application settings persistence is enabled for your users, the application settings VHD file that stores your users' customizations and Windows settings is unmounted and uploaded to an Amazon S3 bucket in your account\.
   + If persistent storage is enabled for your users, the storage connector completes a final synchronization and is unmounted\.

1. The fleet instance is terminated\.

## Create and Specify Session Scripts<a name="create-specify-session-scripts"></a>

Session scripts are configured, specified, and stored within an AppStream 2\.0 image\. After you create your session scripts, perform the following steps on an image builder to specify the scripts\.

**To configure and specify session scripts**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Builder**\.

1. Choose an image builder that is in the **Running** state, and choose **Connect**\.

1. When prompted, choose **Administrator**\.

1. Navigate to C:\\AppStream\\SessionScripts, and open the **config\.json** configuration file\.

   For information about session script parameters, see [Session Scripts Configuration File](#session-script-configuration-file)\.

1. After you finish making your changes, save and close the **config\.json** file\.

1. On the image builder desktop, open Image Assistant\.

1. Optionally, specify any other applications that you want to include in the image\.

1. Follow the necessary steps in Image Assistant to finish creating your image\.

   If the session scripts configuration can't be validated \(for example, if the \.json file is not correctly formatted\), you are notified when you choose **Disconnect and create image**\. 

## Session Scripts Configuration File<a name="session-script-configuration-file"></a>

To locate the session scripts configuration file, navigate to C:\\AppStream\\SessionScripts\\config\.json\. The file is formatted as follows\.

**Note**  
The configuration file is in \.json format\. Verify that any text you type in this file is in valid \.json format\.

```
{
  "SessionStart": {
    "executables": [
      {
        "context": "system",
        "filename": "",
        "arguments": "",
        "s3LogEnabled": true
      },
      {
        "context": "user",
        "filename": "",
        "arguments": "",
        "s3LogEnabled": true
      }
    ],
    "waitingTime": 30
  },
  "SessionTermination": {
    "executables": [
      {
        "context": "system",
        "filename": "",
        "arguments": "",
        "s3LogEnabled": true
      },
      {
        "context": "user",
        "filename": "",
        "arguments": "",
        "s3LogEnabled": true
      }
    ],
    "waitingTime": 30
  }
}
```

You can use the following parameters in the session scripts configuration file\.

***SessionStart/SessionTermination ***  
The session scripts to run in the appropriate session event based on the name of the object\.   
**Type**: String  
**Required**: No  
**Allowed values:** **SessionStart**, **SessionTermination**

***WaitingTime***  
The maximum duration of the session scripts in seconds\.  
**Type**: Integer  
**Required**: No  
**Constraints:** The maximum duration is 60 seconds\. If the session scripts don't complete within this duration, they will be stopped\. If you require a script to continue running, launch it as a separate process\.

***Executables***  
The details for the session scripts to run\.  
**Type**: String  
**Required**: Yes  
**Constraints:** The maximum number of scripts that can run per session event is 2 \(one for the user context, one for the system context\)\.

***Context***  
The context in which to run the session script\.   
**Type**: String  
**Required**: Yes  
**Allowed values:** **user**, **system**

***Filename***  
The full path to the session script to run\. If this parameter is not specified, the session script is not run\.   
**Type**: String  
**Required**: No  
**Constraints:** The maximum length for the file name and full path is 1,000 characters\.  
**Allowed values:** **\.bat**, **\.exe**  
You can also use Windows PowerShell files\. For more information, see [Using Windows PowerShell Files](#using-powershell-files-with-session-scripts)\.

***Arguments***  
The arguments for your session script or executable file\.  
**Type**: String  
**Required**: No  
**Length constraints:** The maximum length is 1,000 characters\.

***S3LogEnabled***  
When the value for this parameter is set to **True**, an S3 bucket is created within your AWS account to store the logs created by the session script\. By default, this value is set to **True**\. For more information, see the *Logging Session Script Output* section later in this topic\.   
**Type**: Boolean  
**Required**: No  
**Allowed values:** **True**, **False**

## Using Windows PowerShell Files<a name="using-powershell-files-with-session-scripts"></a>

To use Windows PowerShell files, specify the full path to the PowerShell file in the **filename** parameter:

```
"filename": 
"C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
```

Then specify your session script in the **arguments** parameter:

```
"arguments": "-File \"C:\\path\\to\\session\\script.ps1\"",
```

Finally, verify that the PowerShell Execution Policy allows your PowerShell file to run\.

## Logging Session Script Output<a name="logging-session-output"></a>

When this option is enabled in the configuration file, AppStream 2\.0 automatically captures the output from the session script that is written to the standard out\. This output is uploaded to an Amazon S3 bucket in your account\. You can review the log files for troubleshooting or debugging purposes\. 

**Note**  
The log files are uploaded when the session script returns a value, or the value set in **WaitingTime** has elapsed, whichever comes first\.

## Use Storage Connectors with Session Scripts<a name="use-storage-connectors-with-session-scripts"></a>

When AppStream 2\.0 storage connectors are enabled, they begin mounting when the session start scripts run\. If your script relies on the storage connectors being mounted, you can wait for the connectors to be available\. AppStream 2\.0 maintains the mount status of the storage connectors in the Windows registry, at the following key:

HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Amazon\\AppStream\\Storage\\<provided user name>\\<Storage connector>

The registry key values are as follows:
+ Provided user name — The user ID provided through the access mode\. The access modes and value for each mode are as follows:
  + User Pool — The email address for the user
  + Streaming URL — The UserID
  + SAML — The NameID\. If the user name includes a slash \(for example, a domain user’s SAMAccountName\), the slash is replaced by a "\-" character\.
+ Storage connector — The connector for the persistent storage option that is enabled for the user\. The storage connector values are as follows:
  + HomeFolder
  + GoogleDrive
  + OneDrive

Each storage connector registry key contains a **MountStatus** DWORD value\. The following table lists the possible values for **MountStatus**\.

**Note**  
To view these registry keys, you must have Microsoft \.NET Framework version 4\.7\.2 or later installed on your image\.


| Value | Description | 
| --- | --- | 
| 0 | Storage connector not be enabled for this user | 
| 1 | Storage connector mounting is in progress | 
| 2 | Storage connector mounted successfully | 
| 3 | Storage connector mounting failed | 
| 4 | Storage connector mounting is enabled, but not mounted yet | 

## Enable Amazon S3 Bucket Storage for Session Script Logs<a name="enable-S3-bucket-storage-session-script-logs"></a>

When you enable Amazon S3 logging in your session script configuration, AppStream 2\.0 captures standard output from your session script\. The output is periodically uploaded to an S3 bucket within your AWS account\. For every AWS Region, AppStream 2\.0 creates a bucket in your account that is unique to your account and the Region\.

You do not need to perform any configuration tasks to manage these S3 buckets\. They are fully managed by the AppStream 2\.0 service\. The log files that are stored in each bucket are encrypted in transit using Amazon S3's SSL endpoints and at rest using Amazon S3\-managed encryption keys\. The buckets are named in a specific format as follows:

```
appstream-logs-region-code-account-id-without-hyphens-random-identifier
```

***region\-code***  
This is the AWS Region code in which the stack is created with Amazon S3 bucket storage enabled for session script logs\.

***account\-id\-without\-hyphens***  
Your AWS account identifier\. The random ID ensures that there is no conflict with other buckets in that Region\. The first part of the bucket name, `appstream-logs`, does not change across accounts or Regions\.

For example, if you specify session scripts in an image in the US West \(Oregon\) Region \(us\-west\-2\) on account number 123456789012, AppStream 2\.0 creates an Amazon S3 bucket within your account in that Region with the name shown\. Only an administrator with sufficient permissions can delete this bucket\.

```
appstream-logs-us-west-2-1234567890123-abcdefg
```

Disabling session scripts does not delete any log files stored in the S3 bucket\. To permanently delete log files, you or another administrator with adequate permissions must do so by using the Amazon S3 console or API\. AppStream 2\.0 adds a bucket policy that prevents accidental deletion of the bucket\. For more information, see *IAM Policies and the Amazon S3 Bucket for Application Settings Persistence* in [Identity and Access Management for Amazon AppStream 2\.0](controlling-access.md)\.

When session scripts are enabled, a unique folder is created for each streaming session that is started\. 

 The path for the folder where the log files are stored in the S3 bucket in your account uses the following structure:

```
bucket-name/stack-name/fleet-name/access-mode/user-id-SHA-256-hash/session-id/SessionScriptsLogs/session-event
```

***bucket\-name***  
The name of the S3 bucket in which the session scripts are stored\. The name format is described earlier in this section\.

***stack\-name***  
The name of the stack the session came from\.

***fleet\-name***  
The name of the fleet the session script is running on\.

***access\-mode***  
The identity method of the user: `custom` for the AppStream 2\.0 API or CLI, `federated` for SAML, and `userpool` for users in the user pool\.

***user\-id\-SHA\-256\-hash***  
The user\-specific folder name\. This name is created using a lowercase SHA\-256 hash hexadecimal string generated from the user identifier\.

***session\-id***  
The identifier of the user's streaming session\. Each user streaming session generates a unique ID\.

***session\-event***  
The event that generated the session script log\. The event values are: `SessionStart` and `SessionTermination`\.

The following example folder structure applies to a streaming session started from the test\-stack and test\-fleet\. The session uses the API of user ID `testuser@mydomain.com`, from an AWS account ID of `123456789012`, and the settings group `test-stack` in the US West \(Oregon\) Region \(us\-west\-2\):

```
appstream-logs-us-west-2-1234567890123-abcdefg/test-stack/test-fleet/custom/a0bcb1da11f480d9b5b3e90f91243143eac04cfccfbdc777e740fab628a1cd13/05yd1391-4805-3da6-f498-76f5x6746016/SessionScriptsLogs/SessionStart/
```

This example folder structure contains one log file for a user context session start script, and one log file for a system context session start script, if applicable\.