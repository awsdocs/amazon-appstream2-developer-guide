# App Blocks<a name="app-blocks"></a>

App blocks represent a virtual hard disk \(VHD\) that is stored within an Amazon S3 bucket within your account that contains the application files and binaries necessary to launch the applications your users will use\. App blocks also include the setup script that informs the operating system how to handle the VHD file\.

## Create the VHD<a name="create-vhd"></a>

A VHD is a single file that when mounted to the operating system is treated like a hard disk\. The VHD can be mounted as a drive letter, to a folder path, or both\. When the VHD is mounted, you can treat it as you would any other hard disk, including installing your application or copying files to it that your user will need\.

To create the app block, you will need to create the VHD, install your applications to it, then detach it\. Once detached you can test your VHD on another PC, an EC2 instance, or an AppStream 2\.0 image builder to validate the applications work as expected\. Once completed, upload to an Amazon S3 bucket in your account and create the app block\.

**Note**  
This page describes using a VHD to deliver your application; however, the AppStream 2\.0 streaming instance will download any object from Amazon S3\. The object you store in Amazon S3 can also be a zip file, application installer, or the application executable itself\. You can use the setup script to configure it correctly on the streaming instance before a user launches their application\.  
The AppStream 2\.0 streaming instance waits up to 90 seconds for the VHD to complete downloading before the setup script runs\. If the VHD does not complete downloading within this duration, the download stops, and the setup script will not run\.   
We recommend a maximum size of 1\.5 gigabyte for the VHD\. You might be able to reduce the size of the VHD by compressing\. You must use the setup script to decompress it before mounting it, because the file needs to be fully downloaded from Amazon S3 before it can be mounted and the application is launched\. Larger VHDs increase the time it takes for the application to launch and the streaming session to begin\.

**To create a VHD for Microsoft Windows**

1. From a Windows PC or Windows Amazon Elastic Compute Cloud \(Amazon EC2\) instance, open a command prompt with administrative privileges\.

1. Launch the Microsoft diskpart utility by entering the following command:

   diskpart

1. Create the unformatted and uninitialized VHD file by entering the following command, where *<maximum file size>* is the size of the VHD file, in MB:

   create vdisk file=C:\\path\\to\\new\\file\.vhdx maximum=*<maximum file size>* type=expandable 

1. Select the newly created VHD by entering the following command:

   select vdisk file=C:\\path\\to\\new\\file\.vhdx

1. Attach the newly created VHD by entering the following command:

   attach vdisk

1. Initialize the newly created VHD by entering the following command:

   convert mbr

1. Create the primary partition spanning the entire VHD by entering the following command:

   create partition primary

1. Format the newly created partition by entering the following command:

   format fs=ntfs quick

1. You can mount your newly created VHD to an unused drive letter, a folder path on the root volume, or both\.

   To mount a drive letter, enter: assign letter=*<unused drive letter>*

   To mount a folder, enter: assign mount=*C:\\path\\to\\empty\\folder\\to\\mount\\*
**Note**  
To mount to a folder path, the folder must already exist and must be empty\.

1. You can now install your application to the VHD, using either the drive letter or the folder mount path chosen in step 9\.

After you finish installing your application\(s\) to the VHD, you need to detach it before you can safely upload it to an Amazon S3 bucket\.

**To detach a VHD for Microsoft Windows**

1. Launch the Microsoft diskpart utility by entering the following command:

   diskpart

1. Select the VHD by entering the following command:

   select vdisk file=*C:\\path\\to\\new\\file\.vhdx*

1. Detach the VHD by entering the following command:

   detach vdisk

1. The VHD has now been detached, and can be tested on another Windows PC, Amazon EC2 instance, or an AppStream 2\.0 image builder\.

**To create a VHD for Linux**

1. From an Amazon Linux 2 EC2 instance, Amazon Linux 2 AppStream 2\.0 image builder, or Amazon Linux 2 WorkSpaces, open a terminal session\.

1. Create the unformatted and uninitialized VHD file:

   dd if=/dev/zero of=*<name of file>* bs=*<size of VHD>* count=1

1. Add a file system to the created VHD by entering the following command:

   sudo mkfs \-t ext4 *<name of file>*
**Note**  
You might see a message stating that the file is not a block special device\. You can select to proceed anyway\.

1. Create an empty folder to use for the mount point by entering the following command:

   sudo mkdir */path/to/mount/point*

1. Mount the newly created VHD to a file system path by running the following command:

   sudo mount \-t auto \-o loop *<name of file>* */path/to/mount/point*

1. You can now install your application to the VHD using the folder mount path chosen in step 4\.
**Note**  
The default permissions for files and folders created on the VHD can prevent non\-administrator users from launching applications or reading files\. Validate the permissions and change them, if necessary\.

After you finish installing your application\(s\) to the VHD, you need to detach it before you can safely upload it to an Amazon S3 bucket\.

**To detach a VHD for Linux**

1. Open a terminal session, and enter the following command:

   sudo umount */path/to/mount/point*

1. The VHD has now been detached, and can be tested on another Amazon Linux 2 Amazon EC2 instance, Amazon Linux 2 AppStream 2\.0 image builder, or Amazon Linux 2 WorkSpaces\.

## Create the Setup Script for the VHD<a name="create-setup-script"></a>

AppStream 2\.0 uses a setup script that you provide to mount the VHD before the application launches\. You can also use the setup script to complete other tasks required to make your application work\. For example, you can configure registry keys, register DLLs, manage pre\-requisites, or modify the user profile from the setup script\. AppStream 2\.0 provides script examples that you can use to mount your VHD\. You will need to modify these scripts for your VHD and application needs\.

Use the following links to download the example scripts:
+ [Amazon Linux 2 bash script](samples/Linux-mount-vhd-script.zip)
+ [Microsoft Windows Powershell script](samples/Windows-mount-vhd-script2.zip)
**Note**  
AppStream 2\.0 and the Microsoft Windows operating system reserve drive letters A through E\. Don't mount VHDs or network shares to these drive letters\.

AppStream 2\.0 downloads the setup script and VHD to a directory on the fleet streaming instance, then runs the setup script\. The setup script runs on the operating system with full administrator rights\. The setup script runs in the `SYSTEM` context on Microsoft Windows, and as the `root` user on Amazon Linux 2\.

File system location for the VHD and setup script:
+ Amazon Linux 2: 

  `/opt/appstream/AppBlocks/appblock-name/`  
**`appblock-name` **  
The name of the app block that the VHD and setup script correspond to\.
+ Microsoft Windows:

  `C:\AppStream\AppBlocks\appblock-name\`  
**`appblock-name` **  
The name of the app block that the VHD and setup script correspond to\.

AppStream 2\.0 maintains the file name as they are on the object\. For example, if your app block is named `MyApps`, with a VHD named `apps.vhd` and setup script named `mount-apps.ps1`, then the full path on a Windows streaming instance is:
+ VHD

  `C:\AppStream\AppBlocks\MyApps\apps.vhd`
+ Setup script

  `C:\AppStream\AppBlocks\MyApps\mount-apps.ps1`

AppStream 2\.0 captures the standard error and standard output from your setup script when it runs on a fleet streaming instance and uploads the output to an Amazon S3 bucket within your account\. You can use these logs to identify and resolve issues you may have with your setup script\. The buckets are named in a specific format as follows:

```
appstream-logs-region-code-account-id-without-hyphens-random-identifier
```

**`region-code` **  
This is the AWS Region code in which the elastic fleet is created within\.

**`account-id-without-hyphens` **  
Your AWS account identifier\. The random ID ensures that there is no conflict with other buckets in that Region\. The first part of the bucket name, appstream\-logs, does not change across accounts or Regions\.

For example, if you create an elastic fleet in the US West \(Oregon\) Region \(us\-west\-2\) on account number 123456789012, AppStream 2\.0 creates an Amazon S3 bucket within your account in that Region with the name shown\. Only an administrator with sufficient permissions can delete this bucket\.

```
appstream-logs-us-west-2-1234567890123-abcdefg
```

The path for the folder where the log files are stored in the S3 bucket in your account uses the following structure:

```
bucket-name/fleet-name/instance-id/appblock-name/
```

**`bucket-name` **  
The name of the Amazon S3 bucket in which the setup script logs are stored\. The name format is described earlier in this section\.

**`Instance-id` **  
The unique identifier for the streaming instance that the setup script ran on

**`appblock-name` **  
The name of the appblock that the setup script corresponds to\. 

The following example folder structure applies to a streaming session started from `test-fleet`\. The session is from an AWS account ID of 123456789012, and appblock name is testappblock in the US West \(Oregon\) Region \(us\-west\-2\):

`appstream-logs-us-west-2-1234567890123-abcdefg/test-fleet/i-084427ab4a1cff7f5/testappblock/`

This example folder structure contains one log file for the standard output, and one log file for the standard error\.

### App block setup script execution<a name="script-execution"></a>

The following diagrams indicate where in the process the setup script runs\. The run order is dependent upon whether Application Settings Persistence is enabled on the stack associated with the elastic fleet\.

**Note**  
AppStream 2\.0 uses your VPC details to download the VHD and setup script from the Amazon S3 bucket\. Your VPC must provide access to the Amazon S3 bucket\. For more information, see [Using Amazon S3 VPC Endpoints for AppStream 2\.0 Features](managing-network-vpce-iam-policy.md)\.

Application Settings Persistence is enabled:

![\[Application Settings Persistence is enabled.\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/app-settings-enabled.png)

Application Settings Persistence is disabled:

![\[Application Settings Persistence is disabled.\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/app-settings-disabled.png)

## Create the App Block Resource<a name="create-app-block"></a>

You can use the AppStream 2\.0 console to create the app block resource once you have your VHD and setup script created and uploaded to an S3 bucket in your AWS account\. To learn more about storing the VHD and setup script in an Amazon S3 bucket, see [Store Application Icon, Setup Script, Session Script, and VHD in S3 Bucket](store-s3-bucket.md)\.

**Note**  
You must have IAM permissions to perform the `S3:GetObject` action on the VHD and setup script objects in the Amazon S3 bucket to create the app block resource\.

**To create the app block resource**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. From the left\-hand navigation menu, choose **Applications**, **App block**, and **Create app block**\.

1. For **App block details**, type a unique name identifier for the app block\. Optionally, you can also specify the following:
   + **Display name** – A friendly name for the app block\.
   + **Description** – A description for the app block\.

1. For **Virtual hard disk object in S3** under **Script settings**, either enter the S3 URI that represents the VHD object, or choose **Browse S3** to navigate to your S3 buckets and find the VHD object\.

1. For **Setup script object in S3** under **Script settings**, either enter the S3 URI that represents the setup script object, or choose **Browse S3** to navigate to your S3 buckets and find the setup script object\.

1. For **Setup script executable** under **Script settings**, enter the executable necessary for your setup script\.
**Note**  
If your setup script can execute directly, enter the filename of the setup script\. If your setup script relies on another executable \(for example, Microsoft PowerShell\) to execute, enter the path to that executable\.  
Path to Microsoft PowerShell on Microsoft Windows:  
`C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`

1. Optionally, for **Setup script executable arguments** under **Script settings**, enter in the arguments that need to be provided to the setup script executable to execute your setup script\.
**Note**  
If you are using a Microsoft PowerShell script, you must specify the "\-File" parameter with the name of your setup script as an executable argument\. Additionally, ensure that the Execution Policy allows your script to be run\. To learn more, see [about\_Execution\_Policies](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2) and [What is PowerShell?](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2)\.

1. For **Execution duration in seconds** under **Script settings**, enter the timeout duration for your setup script\.
**Note**  
The execution duration in seconds is how long AppStream 2\.0 waits for the setup script to run before continuing\. If your setup script doesn’t complete within this duration, an error is displayed to your user and the application will attempt to launch\. The setup script is terminated after the execution duration has elapsed\.

1. \(Optional\) For **Tags**, create tags for the app block resource

1. Review the information that you entered, and choose **Create**\.

1. If your app block was created successfully, you see a success message at the top of the console\. If an error occurred, you see a descriptive error message and will need to try creating the app block again\.

## Update the App Block, VHD, and Setup Script<a name="update-app-block"></a>

App block resources are immutable and do not allow you to change them once created\. If you need to make backwards compatible updates to the VHD or setup script, it is recommended that you upload a new version of the file to the Amazon S3 bucket, overwriting the current version\. New Elastic fleet streaming sessions will download the latest version of the objects, and use them\.

If you need to make backwards incompatible updates to the VHD or setup script, it is recommended that you upload them as new objects to the Amazon S3 bucket, and create a new app block and application resource\. You can then manage the deployment to your users as part of a change window or other outage\.