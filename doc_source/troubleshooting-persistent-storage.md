# Troubleshooting Persistent Storage Issues<a name="troubleshooting-persistent-storage"></a>

Amazon AppStream 2\.0 supports the following options for persistent storage: Home folders, Google Drive for G Suite, and OneDrive for Business\. Because content synchronization behaviors are consistent across these persistent storage solutions, we recommend that you review [Home Folder Content Synchronization](home-folders.md#home-folders-content-synchronization) for information about expected behavior\.

The following are issues that might occur when you or your users use AppStream 2\.0 persistent storage\. 

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