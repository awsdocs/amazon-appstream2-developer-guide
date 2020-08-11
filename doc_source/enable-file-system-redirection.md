# Enable File System Redirection for Your AppStream 2\.0 Users<a name="enable-file-system-redirection"></a>

AppStream 2\.0 file system redirection lets users who have the AppStream 2\.0 client installed access files on their local computer from within their streaming session\. When you enable file system redirection, you can specify the list of local drives and folders that your users can choose to access\. When users sign in to AppStream 2\.0 and start a streaming session, they can choose the drive or folder that they want to access from the list\. Then they can share the drive or folder with AppStream 2\.0\. The drive or folder remains available for them to access during their streaming sessions\. Users can stop sharing their local drives or folders at any time\.

## Prerequisites for File System Redirection<a name="file-system-redirection-prerequisites"></a>

To enable AppStream 2\.0 file redirection:
+ You must use an image that uses a version of the AppStream 2\.0 agent released on or after August 8, 2019\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.
+ Your users must have AppStream 2\.0 client version 1\.0\.480 or later installed\. For more information, see [AppStream 2\.0 Client Version History](client-release-versions.md)\.
+ File upload and download must be enabled on the stack that your users access for streaming sessions\. See the following procedure\.

## How to Enable File System Redirection<a name="how-to-enable-file-system-redirection"></a>

Perform the following steps to enable both file upload and download on the stack that your users access for streaming sessions\. 

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**\.

1. Choose the stack for which you want to enable file system redirection\.

1. Choose the **User Settings** tab, and then expand the **Clipboard, file transfer, and local print permissions** section\.

1. For **File transfer**, verify that **Upload and download** is selected\. If not, choose **Edit**, and then choose **Upload and download**\.

1. Choose **Update**\.

## Make Default Drives and Folders Available for Your Users to Share<a name="prepopulate-drives-folders-system-redirection"></a>

By default, when you enable file direction for users of a stack, the following drives and folders are made available for those users to share in their streaming session:
+ Drives:
  + All local hard disks \(physical drives, such as the C Drive and D Drive\)
  + All virtual drives \(network and virtual drives such as mapped drive letters, Google Drive, and OneDrive\)
  + All local USB drives
+ Folders:
  + %USERPROFILE%\\Desktop
  + %USERPROFILE%\\Documents
  + %USERPROFILE%\\Downloads

These drive and folder paths prepopulate the **Share your local drives and folders** dialog box\. This dialog box is displayed when users sign in to AppStream 2\.0, start a streaming session, and choose **Settings**, **Local Resources**, and **Local Drives and Folders**\. 

You can change or define your own default drive and folder paths by editing the registry\. You can also use the administrative template file that is provided in the AppStream 2\.0 client Enterprise Deployment Tool\. This template lets you configure the client by using Group Policy\. For more information, see [Install and Configure the AppStream 2\.0 Client](install-configure-client.md)\.

When users access their shared local drives and folders during a streaming session, the corresponding paths appear with backslashes replaced by underscores\. They are also suffixed with the name of the local computer and a drive letter\. For example, for a user with the user name janedoe and a computer name of ExampleCorp\-123456, the default Desktop, Documents, and Downloads folder paths appear as follows:

C\_Users\_janedoe\_Desktop \(\\\\ExampleCorp\-123456\) \(F:\)

C\_Users\_janedoe\_Documents \(\\\\ExampleCorp\-123456\) \(G:\)

C\_Users\_janedoe\_Downloads \(\\\\ExampleCorp\-123456\) \(H:\)

## Provide Your AppStream 2\.0 Users with Guidance for Working with File System Redirection<a name="end-user-guidance-file-system-redirection"></a>

To help your users understand how to work with file redirection during their streaming sessions, you can provide them with the information in [How to Access Files on Your Local Computer](client-application-windows-user.md#client-application-windows-file-system-redirection)\. 