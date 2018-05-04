# Persistent Storage with AppStream 2\.0 Home Folders<a name="home-folders"></a>

AppStream 2\.0 supports persistent storage for your end users with Home Folders\. When this option is enabled for an AppStream 2\.0 stack, end users of the stack are presented with a persistent storage folder in their AppStream 2\.0 sessions\. No further conﬁguration is required on your users' part to access their Home Folder\. Data stored by users in their Home Folder is automatically backed up to an Amazon S3 bucket in your AWS account and is made available in subsequent sessions for those users\.

**Note**  
As an administrator, you can access the Home Folder in the following location on an image builder instance: C:\\Users\\PhotonUser\\My Files\\Home Folder\. Use this path if you are configuring your applications to save to the Home Folder\.  
For your users, some applications do not recognize the redirect that displays the Home Folder as a top\-level folder in File Explorer\. If this is the case, your users can access their Home Folder when they are working in an application during a streaming session by choosing **File Open** from the application interface and browsing to the following directory: C:\\Users\\PhotonUser\\My Files\\Home Folder\. 

## Home Folder End User Experience<a name="home-folders-end-user"></a>

For end users, the Home Folder behaves like a normal Windows folder\. Users experience the following Home Folder access features when they are working in an application during a streaming session\.
+ Users can save their documents and project files to their Home Folder\. AppStream 2\.0 continuously checks for the most recently modified files and backs them up to each user's folder in persistent storage\.
+ Data content in each user's Home Folder is specific to that user and cannot be accessed by other users\.
+ Users can easily access their Home Folder when they are working in an application by choosing **File Open** or **File Save** from the application interface\. 
+ A web view is available to access the Home Folder by choosing **My Files** from the web view session toolbar\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/home-folder-ul-dl.png)

  Using the web view, users can navigate to Home Folder files, create new folders within their Home Folder, upload files from their local computer to their Home Folder, download files from their Home Folder to their local computer, and rename any of the existing files or folders within their Home Folder\.

**To upload and download files between your local computer and your Home Folder**

1. In the AppStream 2\.0 web view session, choose the **My Files** icon at the top left of your browser\.

1. Navigate to an existing folder, or choose **Add Folder** to create a new folder\.

1. When the desired folder is displayed, choose **Upload** to upload a local file to the currently displayed location in the session's Home Folder\. To download a specific file, choose the down arrow on the right of the file name and choose **Download**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/home-folder-ex1.png)