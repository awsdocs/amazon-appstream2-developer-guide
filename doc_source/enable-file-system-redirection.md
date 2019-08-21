# Enable File System Redirection for Your AppStream 2\.0 Users<a name="enable-file-system-redirection"></a>

AppStream 2\.0 file system redirection lets users who have the AppStream 2\.0 client installed access files on their local computer from within their streaming session\. When you enable file system redirection, you can specify the list of local drives and folders that your users can choose to access\. When users sign in to AppStream 2\.0 and start a streaming session, they can choose the drive or folder that they want to access from the list\. Then they can share the drive or folder with AppStream 2\.0\. The drive or folder remains available for them to access during their streaming sessions\. Users can stop sharing their local drives or folders at any time\.

## Prerequisites for File System Redirection<a name="file-system-redirection-prerequisites"></a>

To enable AppStream 2\.0 file redirection, you must meet the following prerequisites:
+ You must use an image that uses a version of the AppStream 2\.0 agent released on or after August 8, 2019\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.
+ Your users must have AppStream 2\.0 client version 1\.0\.480 or later installed\. For more information, see [AppStream 2\.0 Client Version History](client-release-versions.md)\.
+ File upload and download must be enabled on the stack that your users access for streaming sessions\. For instructions, see the next section\.

## How to Enable File System Redirection<a name="-how-to-enable-file-system-redirection"></a>

Perform the following steps to enable both file upload and download on the stack that your users access for streaming sessions\. 

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**\.

1. Choose the stack for which you want to enable file system redirection\.

1. Choose the **User Settings** tab, and then expand the **Clipboard, file transfer, and local print permissions** section\.

1. Verify that **Upload and download** is selected for **File transfer**\. If not, choose **Edit**, and then choose **Upload and download**\.

1. Choose **Update**\.

## Make default drives and folders available for your users to share<a name="prepopulate-drives-folders-system-redirection"></a>

By default, when you enable file direction for users of a stack, the following drives and folders are made available for those users to share within their streaming session:
+ Drives:
  + All local hard disks \(physical drives, such as the C Drive and D Drive\)
  + All virtual drives \(network and virtual drives such as mapped drive letters, Google Drive, and OneDrive\)
  + All local USB drives
+ Folders:
  + %USERPROFILE%\\Desktop
  + %USERPROFILE%\\Documents
  + %USERPROFILE%\\Downloads

These drive and folder paths prepopulate the **Share your local drives and folders** dialog box\. This dialog box displays when users sign in to AppStream 2\.0, start a streaming session, and choose **Settings**, **Local Resources**, and **Local Drives and Folders**\. 

You can change or define your own default drive and folder paths by modifying the registry\. You can also use the administrative template file that is provided in the AppStream 2\.0 client Enterprise Deployment Tool\. This template lets you configure the client by using Group Policy\. For more information, see *Configure the AppStream 2\.0 Client for Your Users* in [Install and Configure the AppStream 2\.0 Client](install-configure-client.md)\.

When users access their shared local drives and folders during a streaming session, the corresponding paths appear with backslashes replaced by underscores\. They are also suffixed with the name of the local computer and a drive letter\. For example, for a user with the user name janedoe and a computer name of ExampleCorp\-123456, the default Desktop, Documents, and Downloads folder paths appear as follows:

C\_Users\_janedoe\_Desktop \(\\\\ExampleCorp\-123456\) \(F:\)

C\_Users\_janedoe\_Documents \(\\\\ExampleCorp\-123456\) \(G:\)

C\_Users\_janedoe\_Downloads \(\\\\ExampleCorp\-123456\) \(H:\)

## Provide Your AppStream 2\.0 Users with Guidance for Working with File System Redirection<a name="end-user-guidance-file-system-direction"></a>

To help your users understand how to work with file redirection during their streaming sessions, you can provide them with the following information\. 

**Guidance for Users**

AppStream 2\.0 file redirection lets you access files on your local computer from within your AppStream 2\.0 streaming session\. To use file redirection, open the AppStream 2\.0 client, connect to a streaming session, and choose the drives and folders that you want to share\. After you share a local drive or folder, you can access all files in the shared drive or folder from within your streaming session\. You can stop sharing local drives and folders at any time\.

**Important**  
To use AppStream 2\.0 file redirection, you must have the AppStream 2\.0 client installed on your local computer\. File redirection is not available when you connect to AppStream 2\.0 by using a web browser\.

**To share local drives and folders**

1. Open the AppStream 2\.0 client and connect to a streaming session\.

1. In your AppStream 2\.0 session, in the top left area, choose the **Settings** icon, and then choose **Local Resources**, **Local Drives and Folders**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-MenuOptions.png)

   The **Share your local drives and folders** dialog box displays the drives and folders that your administrator has made available for you to share\. You can share all or specific drives and folders, or just one\. You can also add your own drives and folders\. To share drives and folders, do one of the following:
   + To share all local drives and folders displayed in the **Share your local drives and folders** dialog box, in the upper right of the dialog box, choose **Share All**\. To apply your changes to future streaming sessions, in the lower right of the dialog box, choose **Save my configuration** to save your changes\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-ShareAll.png)
   + To share a specific local drive or folder, select the drive or folder that you want to access, and choose **Share**, **Save my configuration**\. To share another local drive or folder, repeat these steps as needed\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-Share-Specific.png)
   + If the local drive or folder that you want to share doesn't display, you can add it\. For example, your administrator may make your entire local C Drive available for you to share\. However, you may only need to access a specific folder on that drive\. In this case, you can add the folder that you need and share the folder only\. To choose a specific folder, do the following:
     + In the lower left of the **Share your local drives and folders** dialog box, choose the **Add Folder** icon\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-Add-Specific-Folder.png)
     + Browse to the folder that you want to share, and choose **OK**\.
     + The folder that you selected is now available to share\. Select the folder, and choose **Share**, **Save my configuration**\. To add another local drive or folder, repeat these steps as needed\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drive-Folders-SpecificFolderAdded.PNG)

After you share a local drive or folder, perform the following steps to access files in the shared drive or folder from within your streaming session\. 

**To access files in a shared local drive or folder**

1. Open the AppStream 2\.0 client and connect to a streaming session\.

1. In your AppStream 2\.0 session, open the application that you want to use\.

1. From your application interface, choose **File Open**, and browse to the file that you want to access\. The following screenshot shows how shared local drives and folders appear in the Notepad\+\+ browse dialog box for Jane Doe, when she browses for a file\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-Access-Shared-Drives-Folders.png)

   In the browse dialog box, the corresponding paths for her shared drives and folders are shown in the red box\. The paths appear with backslashes replaced by underscores\. At the end of each path is the name of Jane's computer, ExampleCorp\-123456, and a drive letter\.

1. When you're done working with the file, use the **File Save** or **File Save As** command to save it to the location that you want\.

If you want to stop sharing a local drive or folder, perform the following steps\.

**To stop sharing local drives and folders**

1. Open the AppStream 2\.0 client and connect to a streaming session\.

1. In your AppStream 2\.0 session, in the top left area, choose the **Settings** icon, and then choose **Local Resources**, **Local Drives and Folders**\. 

   The **Share your local drives and folders** dialog box displays the drives and folders that your administrator has made available for you to share, and any that you added, if applicable\. To stop sharing one or more local drives and folders, do either of the following:
   + To stop sharing all shared local drives and folders, choose **Unshare All**, **Save my configuration**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-UnshareAll.png)
   + To stop sharing a specific shared local drive or folder, select the drive or folder, and choose **Unshare**, **Save my configuration**\. To stop sharing another local drive or folder, repeat these steps as needed\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drives-Folders-UnshareAll.png)

You can delete local drives and folders that you add to the **Share your local drives and folders** dialog box\. However, you can't delete local drives or folders that your administrator has made available for you to share\. Also, if you have already shared a local drive or folder, you must stop sharing it before you can delete it\.

**To delete local drives and folders**

1. Open the AppStream 2\.0 client and connect to a streaming session\.

1. In your AppStream 2\.0 session, in the top left area, choose the **Settings** icon, and then choose **Local Resources**, **Local Drives and Folders**\. 

   The **Share your local drives and folders** dialog box displays the drives and folders that your administrator has made available for you to share\. If you added any drives or folders, they display as well\.

1. Select the local drive or folder that you want to delete, and then choose **Delete**, **Save my configuration**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-Client-Local-Drive-Folders-SpecificFolderAdded-Delete.png)