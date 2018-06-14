# Enable and Administer Google Drive for Your AppStream 2\.0 Users<a name="google-drive"></a>

AppStream 2\.0 supports persistent storage for your users with Google Drive and home folders\. You can enable one or both options as needed for your organization\. When you enable Google Drive for an AppStream 2\.0 stack, end users of the stack can link their Google Drive account to AppStream 2\.0\. After their account is linked to AppStream 2\.0, your users can sign into their Google Drive account and access their Google Drive folder during application streaming sessions\. Any changes that your users make to files or folders in their Google Drive during application streaming sessions are automatically backed up and synchronized so that they are available to users outside their streaming session\. 

**Important**  
You can enable Google Drive for accounts in G Suite domains only, not for personal Gmail accounts\.

**Topics**
+ [Enable Google Drive for Your AppStream 2\.0 Users](#enable-google-drive)
+ [Disable Google Drive for Your AppStream 2\.0 Users](#disable-google-drive)
+ [Provide Your AppStream 2\.0 Users with Guidance for Working with Google Drive](#google-drive-end-user)

## Enable Google Drive for Your AppStream 2\.0 Users<a name="enable-google-drive"></a>

Before enabling Google Drive, you must do the following:
+ Make sure that the stack on which you enable Google Drive is associated with a fleet based on an image that uses a version of the AppStream 2\.0 agent released on or after May 31, 2018\. For more information, see [Amazon AppStream 2\.0 Agent Version History](agent-software-versions.md)\. The fleet must also have access to the internet\.
+ Add Amazon AppStream 2\.0 as a trusted app in one or more G Suite domains\. You can enable Google Drive for up to 10 G Suite domains\.

Follow these steps to add Amazon AppStream 2\.0 as a trusted app in your G Suite domains\.

**To add Amazon AppStream 2\.0 as a trusted app in your G Suite domains**

1. Sign in to the G Suite Admin console at [https://admin.google.com/](https://admin.google.com/)\.

1. Choose **Dashboard**\.

1. Choose the main menu in the upper left of the window \(to the left of the **Google Admin** title\), then choose **Security**, **Settings**\.

1. Choose **API Permissions**\.

1. At the bottom of the **API Access** list, choose the **Trusted Apps** link\.

1. Choose the **Whitelist an App** \[plus sign \(\+\) icon\] in the bottom right of the window\. 

1. In the **Add APP to Trusted List** dialog box, do the following\. When you're done, choose **Add**:
   + For **Select App Type**, choose **Web Application**\.
   + For **OAuth2 Client ID**, type the Amazon AppStream 2\.0 OAuth client ID for your AWS Region\. For a list of client IDs, see the table that follows this procedure\.

1. Confirm that Amazon AppStream 2\.0 appears in the list of trusted apps\.


**Amazon AppStream 2\.0 OAuth2 client IDs**  

| Region | Amazon AppStream 2\.0 OAuth client ID | 
| --- | --- | 
| us\-east\-1 \(N\.Virginia\) | 266080779488\-15n5q5nkiclp6m524qibnmhmbsg0hk92\.apps\.googleusercontent\.com | 
| us\-west\-2 \(Oregon\) | 1026466167591\-i4jmemrggsjomp9tnkkcs5tniggfiujb\.apps\.googleusercontent\.com | 
| ap\-northeast\-1 \(Tokyo\) | 922579247628\-qpl9kpihg3hu5dul2lphbjs4qbg6mjm2\.apps\.googleusercontent\.com  | 
| ap\-southeast\-1 \(Singapore\) | 856871139998\-4eia2n1db5j6gtv4c1rdte1fh1gec8vs\.apps\.googleusercontent\.com | 
| ap\-southeast\-2 \(Sydney\) | 151535156524\-b889372osskprm4dt1clpm53mo3m9omp\.apps\.googleusercontent\.com  | 
| eu\-central\-1 \(Frankfurt\) | 643727794574\-1se5360a77i84je9j3ap12obov1ib76q\.apps\.googleusercontent\.com | 
| eu\-west\-1 \(Ireland\) | 599492309098\-098muc7ofjfo9vua5rm5u9q2k3mlok3j\.apps\.googleusercontent\.com  | 

Follow these steps to enable Google Drive for your AppStream 2\.0 users\.

**To enable Google Drive while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), and ensure that **Enable Google Drive** is selected and that you have specified at least one G Suite domain\.

**To enable Google Drive for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to enable Google Drive\.

1. Below the stacks list, choose **Storage** and select **Enable Google Drive**\.

1. In the **Enable Google Drive** dialog box, in **G Suite domain name**, type the name of at least one G Suite domain\. To specify another domain, choose **Add another domain**, and type the name of the G Suite domain\.

1. After you finish adding G Suite domain names, choose **Enable**\.

## Disable Google Drive for Your AppStream 2\.0 Users<a name="disable-google-drive"></a>

You can disable Google Drive for a stack without losing user content that is already stored on Google Drive\. Disabling Google Drive for a stack has the following effects:
+ For any users who are connected to active streaming sessions for the stack, an error message displays during the session to inform these users that they do not have permissions to access their Google Drive\. 
+ Any new sessions that use the stack with Google Drive disabled do not display Google Drive\. 
+ Disabling Google Drive for one stack does not disable it for other stacks\. Only the specific stack for which Google Drive is disabled is affected\.
+ Even if Google Drive is disabled for all stacks, AppStream 2\.0 does not delete the user content\.

Follow these steps to disable Google Drive for an existing stack\.

**To disable Google Drive for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to disable Google Drive\.

1. Below the stacks list, choose **Storage** and clear **Enable Google Drive**\.

1. In the **Disable Google Drive** dialog box, type `CONFIRM` \(case\-sensitive\) to confirm your choice, then choose **Disable**\.

## Provide Your AppStream 2\.0 Users with Guidance for Working with Google Drive<a name="google-drive-end-user"></a>

To help your users understand how to work with Google Drive, you can provide them with the following information\. 

**Guidance for Users**

When you add your Google Drive account to AppStream 2\.0 and you are signed in to an AppStream 2\.0 streaming session, you can do the following with your Google Drive:
+ Open and edit files and folders that you store in your Google Drive\. Content that is stored in your Google Drive is specific to you and cannot be accessed by other users unless you choose to share it\.
+ Upload and download files between your local computer and your Google Drive\. Any changes that you make to files and folders in your Google Drive during a streaming session are automatically backed up and synchronized so that they are available to you when you sign in to your Google account and access Google Drive outside your streaming session\.
+ When you are working in an application, you can access files and folders that are stored in your Google Drive by choosing **File Open** from the application interface and browsing to the file or folder that you want to open\. To save changes to a file that you are working in to your Google Drive, choose **File Save** from the application interface and browse to the location in your home folder where you want to save the file\. 
+ You can also access your Google Drive by choosing **My Files** from the web view session toolbar\.

**To add your Google Drive account to AppStream 2\.0**

To access your Google Drive during AppStream 2\.0 streaming sessions, you must first add your Coogle Drive account to AppStream 2\.0\. 

1. In the AppStream 2\.0 web view session, choose the **My Files** icon at the top left of your browser\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-WebView-MyFolders2.png)

1. In the **My Files** dialog box, choose **Add Google Drive**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AddGoogleDrive3.png)

1. Choose the domain for your Google Drive account\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/ChooseGSuiteDomain.png)

1. The **Sign in with Google** dialog box displays\. Enter the user name and password for your Google Drive account when prompted\. 

1. After your Google Drive account is added to AppStream 2\.0, your Google Drive folder displays in **My Files**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/GoogleDriveAdded.png)

1. To work with files and folders in your Google Drive, choose the **Google Drive** folder and browse to a folder or file as needed\. If you do not want to work with files in your Google Drive during this streaming session, close the **My Files** dialog box\. 

**To upload and download files between your local computer and your Google Drive**

1. In the AppStream 2\.0 web view session, choose the **My Files** icon at the top left of your browser\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-WebView-MyFolders2.png)

1. In the **My Files** dialog box, choose **Google Drive**\.

1. Navigate to an existing folder, or choose **Add Folder** to create a new folder\.

1. When the folder that you want displays, do one of the following: 
   + To upload a file to the folder, select the file that you want to upload, and choose **Upload**\.
   + To download a file from the folder, select the file that you want to download, choose the down arrow to the right of the file name, and choose **Download**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/GoogleDrive_FileUploadDownload.png)