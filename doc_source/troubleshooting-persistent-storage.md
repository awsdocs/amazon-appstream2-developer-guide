# Troubleshooting Persistent Storage Issues<a name="troubleshooting-persistent-storage"></a>

Amazon AppStream 2\.0 supports the following options for persistent storage: Home folders, Google Drive for G Suite, and OneDrive for Business\. Because content synchronization behaviors are consistent across these persistent storage solutions, we recommend that you review [Home Folder Content Synchronization](home-folders.md#home-folders-content-synchronization) for information about expected behavior\.

The following are issues that might occur when you or your users use AppStream 2\.0 persistent storage\. 

**Topics**
+ [My stack's home folders aren't working correctly\.](#troubleshooting-s3-failures)
+ [My users can't access their home folder directory from one of our applications\.](#alternate-path-accessing-home-folders)
+ [I removed or replaced a file in a user’s home folder in Amazon S3, but my users don’t see the changes in their home folder on the fleet instance during their streaming sessions\.](#removed-replaced-folder-in-s3-users-dont-see-changes-on-fleet-instance)
+ [Persistent storage isn't performing as expected\. My users' files are taking longer than expected to save to persistent storage\.](#troubleshooting-persistent-storage-applications-take-long-time-to-save-to-home-folder)
+ [My users are getting errors that files are already in use when their files are not in use\.](#troubleshooting-persistent-storage-application-errors-files-already-in-use)
+ [When a folder contains thousands of files, AppStream 2\.0 might take a long time to display the list of files\.](#troubleshooting-persistent-storage-delay-listing-thousands-of-files-in-folder)

## My stack's home folders aren't working correctly\.<a name="troubleshooting-s3-failures"></a>

Problems with home folder backup to an S3 bucket can occur in the following scenarios:
+ There is no internet connectivity from the streaming instance, or there is no access to the private Amazon S3 VPC endpoint, if applicable\.
+ Network bandwidth consumption is too high\. For example, multiple large files are being downloaded or streamed by the user while the service is trying to back up a home folder that contains large files to Amazon S3\.
+ An administrator deleted the bucket created by the service\.
+ An administrator incorrectly edited the Amazon S3 permissions for the `AmazonAppStreamServiceAccess` service role\.

For more information, see the [Amazon Simple Storage Service Console User Guide](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/) and [Amazon Simple Storage Service Developer Guide](https://docs.aws.amazon.com/AmazonS3/latest/dev/)\.

## My users can't access their home folder directory from one of our applications\.<a name="alternate-path-accessing-home-folders"></a>

Some applications do not recognize the redirect that displays the home folder as a top\-level folder in File Explorer\. If this is the case, your users can access their home folder from within an application during a streaming session by choosing **File Open** from the application interface and browsing to either of the following directories: 
+ Non\-domain\-joined: C:\\Users\\PhotonUser\\My Files\\Home Folder
+ Domain\-joined: C:\\Users\\%username%\\My Files\\Home Folder

## I removed or replaced a file in a user’s home folder in Amazon S3, but my users don’t see the changes in their home folder on the fleet instance during their streaming sessions\.<a name="removed-replaced-folder-in-s3-users-dont-see-changes-on-fleet-instance"></a>

Differences between content that is stored in a user’s home folder in an S3 bucket and content that is available to a user on a fleet instance during their streaming sessions may be due to the way in which home folder content stored in Amazon S3 buckets is synchronized with home folder content stored on AppStream 2\.0 fleet instances\. 

At the beginning of a user’s AppStream 2\.0 streaming session, AppStream 2\.0 catalogs the user’s home folder files stored in the Amazon S3 bucket for your AWS account and Region\. When a user uses a streaming application to open a file in their home folder on their fleet instance, AppStream 2\.0 downloads the file to the fleet instance\. 

Changes that a user makes to files on a fleet instance during their active streaming session are uploaded to their home folder in the S3 bucket every few seconds, or at the end of the user’s streaming session\. 

If a user opens a file in their home folder on a fleet instance during a streaming session and then closes the file without making any changes or saving the file, and you remove the file from that user’s home folder in an S3 bucket during the streaming session, the file is removed from the fleet instance if the user refreshes the folder\. If the user modifies the file and saves the file locally, the file remains available to the user on the fleet instance during their current streaming session\. The file is also uploaded to the S3 bucket again\. However, the file may or may not be available to the user on the fleet instance during their next streaming session\. 

The availability of the file on the fleet instance during a user’s next streaming session depends on whether the user changed the file on the fleet instance before or after you changed the file in the S3 bucket\.

For more information, see [Home Folder Content Synchronization](home-folders.md#home-folders-content-synchronization)\.

## Persistent storage isn't performing as expected\. My users' files are taking longer than expected to save to persistent storage\.<a name="troubleshooting-persistent-storage-applications-take-long-time-to-save-to-home-folder"></a>

During AppStream 2\.0 streaming sessions, saving large files and directories associated with compute\-intensive applications to persistent storage can take longer than saving files and directories required for basic productivity applications\. For example, it might take longer for applications to save a large amount of data or frequently modify the same files than it would to save files created by applications that perform a single write action\. It might also take longer to save many small files\.

If your users save files and directories associated with compute\-intensive applications and AppStream 2\.0 persistent storage options aren't performing as expected, we recommend that you use a Server Message Block \(SMB\) solution such as Amazon FSx for Windows File Server or an AWS Storage Gateway file gateway\. Following are examples of files and directories associated with compute\-intensive applications that are more suitable for use with these SMB solutions:
+ Workspace folders for integrated development environments \(IDEs\)
+ Local database files
+ Scratch space folders created by graphics simulation applications

For more information, see:
+  [https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)
+ [Using Amazon FSx with Amazon AppStream 2\.0 ](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-amazon-fsx-with-amazon-appstream-2-0/)
+ [File gateways](https://docs.aws.amazon.com/storagegateway/latest/userguide/StorageGatewayConcepts.html#file-gateway-concepts) in the *AWS Storage Gateway User Guide*

**Note**  
Before proceeding with further troubleshooting, first ensure that the issue your users are experiencing with saving files and directories is associated with AppStream 2\.0 persistent storage only, and not another cause\. To rule out other causes, have your users try saving the files or directories to the Temporary Files directory that is available on their streaming instance\.

## My users are getting errors that files are already in use when their files are not in use\.<a name="troubleshooting-persistent-storage-application-errors-files-already-in-use"></a>

This behavior is typically occurs in the following cases:
+ When users' files are still being uploaded after the files were last saved 
+ Files that are modified frequently \(for example, database files\)

Large file uploads might take significant time\. Also, each attempt to upload the file might result in another file update, which can lead to repeated file upload attempts\.

To resolve this issue, we recommend that you use a Server Message Block \(SMB\) solution such as Amazon FSx for Windows File Server or an AWS Storage Gateway file gateway\. For more information, see:
+  [https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)
+ [Using Amazon FSx with Amazon AppStream 2\.0 ](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-amazon-fsx-with-amazon-appstream-2-0/)
+ [File gateways](https://docs.aws.amazon.com/storagegateway/latest/userguide/StorageGatewayConcepts.html#file-gateway-concepts) in the *AWS Storage Gateway User Guide*

## When a folder contains thousands of files, AppStream 2\.0 might take a long time to display the list of files\.<a name="troubleshooting-persistent-storage-delay-listing-thousands-of-files-in-folder"></a>

AppStream 2\.0 uses API calls to retrieve the content of folders that are stored in AppStream 2\.0 persistent storage\. There is a limit to the number of items that an API call can retrieve each time the call runs\. For this reason, if AppStream 2\.0 must retrieve thousands of files in a single folder, it might take more time to display the list of all the files than it would to display the list of files in a folder that contains fewer files\.

To resolve this issue, if you have thousands of files in one folder, we recommend that you divide this content into groups of fewer files and store each group in a different folder\. Doing so reduces the number of API calls that are required to display the list of files in each folder\. 