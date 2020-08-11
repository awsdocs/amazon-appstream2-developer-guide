# How Application Settings Persistence Works<a name="how-it-works-app-settings-persistence"></a>

Persistent application settings are saved to a Virtual Hard Disk \(VHD\) file\. This file is created the first time a user streams an application from a stack on which application settings persistence is enabled\. If the fleet associated with the stack is based on an image that contains default application and Windows settings, the default settings are used for the user's first streaming session\. For more information about default settings, see *Step 3: Create Default Application and Windows Settings* in [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

When the streaming session ends, the VHD is unmounted and uploaded to an Amazon S3 bucket within your account\. The bucket is created when you enable persistent application settings for the first time for a stack in an AWS Region\. The bucket is unique to your AWS account and the Region\. The VHD is encrypted in transit using Amazon S3 SSL endpoints, and at rest using [AWS Managed CMKs](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#aws-managed-cmk)\.

The VHD is mounted to the streaming instance in both C:\\Users\\%username% and D:\\%username%\. If your instance is not joined to an Active Directory domain, the Windows user name is PhotonUser\. If your instance is joined to an Active Directory domain, the Windows user name is that of the logged in user\. 

Application settings persistence does not work across different operating system versions\. For example, if you enable application settings persistence on a stack and the stack is associated with a fleet that uses a Windows Server 2012 R2 image, if you update the fleet to use an image that runs a different operating system \(such as Windows Server 2016\), settings from previous streaming sessions are not saved for users of the stack\. Instead, after you update the fleet to use the new image, when users launch a streaming session from a fleet instance, a new Windows user profile is created\. However, if you apply an update to the same operating system on the image, users' customizations and settings from previous streaming sessions are saved\. When updates to the same operating system are applied to an image, the same Windows user profile is used when users launch a streaming session from the fleet instance\. 

**Important**  
AppStream 2\.0 supports applications that rely on the [Microsoft Data Protection API](https://docs.microsoft.com/en-us/windows/desktop/seccng/cng-dpapi) only when the streaming instance is joined to a Microsoft Active Directory domain\. In cases where a streaming instance is not joined to an Active Directory domain, the Windows user, PhotonUser, is different on each fleet instance\. Due to the way in which the DPAPI security model works, users' passwords don’t persist for applications that use DPAPI in this scenario\. In cases where streaming instances are joined to an Active Directory domain and the user is a domain user, the Windows user name is that of the logged in user, and users’ passwords persist for applications that use DPAPI\.

AppStream 2\.0 automatically saves all files and folders in this path, except for the following folders:
+ Contacts
+ Desktop
+ Documents
+ Downloads
+ Links
+ Pictures
+ Saved Games
+ Searches
+ Videos

Files and folders created outside of these folders are saved within the VHD and synced to Amazon S3\. The default VHD maximum size is 1GB\. The size of the saved VHD is the total size of the files and folders that it contains\. AppStream 2\.0 automatically saves the HKEY\_CURRENT\_USER registry hive for the user\.

**Note**  
The entire VHD must be downloaded to the streaming instance before a streaming session can begin\. For this reason, a VHD that contains a large amount of data can delay the start of the streaming session\. For more information, see [Best Practices for Enabling Application Settings Persistence](enabling-app-settings-persistence.md#best-practices-app-settings-persistence)\.

When you enable application settings persistence, you must specify a settings group\. The settings group determines which saved application settings are used for a streaming session from this stack\. AppStream 2\.0 creates a new VHD file for the settings group that is stored separately within the S3 bucket in your AWS account\. If the settings group is shared between stacks, the same application settings are used in each stack\. If a stack requires its own application settings, specify a unique settings group for the stack\.