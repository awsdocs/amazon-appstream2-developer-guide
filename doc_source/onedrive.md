# Enable and Administer OneDrive for Your AppStream 2\.0 Users<a name="onedrive"></a>

AppStream 2\.0 supports the following persistent storage options for users in your organization: 
+ OneDrive for Business
+ Google Drive for G Suite
+ Home folders

You can enable one or more options for your organization\. When you enable OneDrive for Business for an AppStream 2\.0 stack, users of the stack can link their OneDrive for Business account to AppStream 2\.0\. Then they can sign into their OneDrive for Business account and access their OneDrive folder during application streaming sessions\. Any changes that they make to files or folders in OneDrive during those sessions are automatically backed up and synchronized, so that they are available to users outside of their streaming sessions\. 

**Important**  
You can enable OneDrive for Business for accounts in your OneDrive domains only, but not for personal accounts\.

**Topics**
+ [Enable OneDrive for Your AppStream 2\.0 Users](#enable-onedrive)
+ [Disable OneDrive for Your AppStream 2\.0 Users](#disable-onedrive)
+ [Provide Your AppStream 2\.0 Users with Guidance for Working with OneDrive](#onedrive-end-user)

## Enable OneDrive for Your AppStream 2\.0 Users<a name="enable-onedrive"></a>

Before enabling OneDrive, you must do the following:
+ Have an active Microsoft Office 365 or OneDrive for Business account with a valid organizational domain and user accounts in the domain to use with AppStream 2\.0\. 
+ Configure an AppStream 2\.0 stack with an associated fleet\.

   The fleet must use an image that uses a version of the AppStream 2\.0 agent released on or after July 26, 2018\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\. The fleet must also have access to the internet\.

Follow these steps to enable OneDrive for your AppStream 2\.0 users\.

**To enable OneDrive while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), make sure that **Enable OneDrive** is selected, and that you have specified at least one organizational domain that is associated with your OneDrive for Business account\.

**To enable OneDrive for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to enable OneDrive\.

1. Below the stacks list, choose **Storage**, and select **Enable OneDrive for Business**\. 

1. In the **Enable OneDrive for Business** dialog box, in **OneDrive domain name**, type the name of at least one organizational domain that is associated with your OneDrive account\. To specify another domain, choose **Add another domain**, and type the name of the domain\.

1. After you add OneDrive domain names, choose **Enable**\.

Before your users can use OneDrive with AppStream 2\.0, you must provide them with permissions to link their OneDrive account with third\-party web applications\. To do so, follow the steps in the next section\.

**Provide Your Users with Permissions to Link OneDrive with AppStream 2\.0**

1. Sign in to Office 365 or the OneDrive for Business admin console\.

1. In the left navigation pane of the console, choose **Settings**, **Services & add\-ins**\.

1. From the list of services and add\-ins, choose **Integrated Apps**\.

1. On the **Integrated apps** page, turn on the option to allow users in your organization to let third party web apps access their Office 365 information\.

## Disable OneDrive for Your AppStream 2\.0 Users<a name="disable-onedrive"></a>

You can disable OneDrive for a stack without losing user content that is already stored on OneDrive\. Disabling OneDrive for a stack has the following effects:
+ Users who are connected to active streaming sessions for the stack receive an error message\. They are informed that they do not have permissions to access their OneDrive\. 
+ Any new sessions that use the stack with OneDrive disabled do not display OneDrive\. 
+ Only the specific stack for which OneDrive is disabled is affected\.
+ Even if OneDrive is disabled for all stacks, AppStream 2\.0 does not delete the user content stored in their OneDrive\.

Follow these steps to disable OneDrive for an existing stack\.

**To disable OneDrive for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to disable OneDrive\.

1. Below the stacks list, choose **Storage**, and clear **Enable OneDrive for Business** option\.

1. In the **Disable OneDrive for Business** dialog box, type `CONFIRM` \(case\-sensitive\) to confirm your choice, then choose **Disable**\.

   When users of the stack start their next AppStream 2\.0 streaming session, they can no longer access their OneDrive folder from within that session and future sessions\.

## Provide Your AppStream 2\.0 Users with Guidance for Working with OneDrive<a name="onedrive-end-user"></a>

To help your users understand how to work with OneDrive, you can provide them with the information described in this section\. 

**Guidance for Users**

When you add your OneDrive account to AppStream 2\.0 and you are signed in to an AppStream 2\.0 streaming session, you can do the following in OneDrive:
+ Open and edit files and folders that you store in OneDrive\. Content that is stored in OneDrive is specific to you\. Other users cannot access your content unless you choose to share it\.
+ Upload and download files between your local computer and OneDrive\. Any changes that you make to your files and folders in OneDrive during a streaming session are automatically backed up and synchronized\. They are available to you when you sign in to your OneDrive account and access OneDrive outside of your streaming session\.
+ When you are working in an application, you can access your files and folders that are stored in OneDrive\. Choose **File**, **Open** from the application interface and browse to the file or folder that you want to open\. To save your changes in a file to OneDrive, choose **File**, **Save** from the application and browse to the location in OneDrive where you want to save the file\. 
+ You can also access OneDrive by choosing **My Files** from the web view session toolbar\.

**To add your OneDrive account to AppStream 2\.0**

To access your OneDrive during AppStream 2\.0 streaming sessions, you must first add your OneDrive account to AppStream 2\.0\. 

1. In the AppStream 2\.0 web view session, choose the **My Files** icon at the top left of your browser\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-WebView-MyFolders2.png)

1. In the **My Files** dialog box, choose **Add Storage**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AddStorage.png)

1. Choose **OneDrive**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AddOneDrive1.png)

1. Under **Login accounts**, choose the domain for your OneDrive account\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/LoginAccounts.png)

1. The **Sign in** dialog box displays\. Type the user name and password for your account when prompted, then sign in\.

1. After your OneDrive account is added to AppStream 2\.0, your OneDrive folder displays in **My Files**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AddOneDrive2.png)

1. To work with your files and folders in OneDrive, choose the **OneDrive** folder and browse to the file or folder you want\. If you do not want to work with files in OneDrive during this streaming session, close the **My Files** dialog box\. 

**To upload and download files between your local computer and your OneDrive**

1. In the AppStream 2\.0 web view session, choose the **My Files** icon at the top left of your browser\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream2-WebView-MyFolders2.png)

1. In the **My Files** dialog box, choose **OneDrive**\.

1. Navigate to an existing folder, or choose **Add Folder** to create a new folder\.

1. When the folder that you want displays, do one of the following: 
   + To upload a file to the folder, select the file that you want to upload, and choose **Upload**\.
   + To download a file from the folder, select the file that you want to download, choose the down arrow to the right of the file name, and choose **Download**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/GoogleDrive_FileUploadDownload.png)

**To remove OneDrive permissions from AppStream 2\.0**

If you no longer want to use OneDrive during your AppStream 2\.0 streaming sessions, follow these steps to remove OneDrive permissions from AppStream 2\.0\.
**Note**  
You can restore these permissions at any time during an AppStream 2\.0 streaming session\.

1. Sign in to Office 365 or OneDrive for Business\.

1. In the right pane, under **My accounts**, choose **My account**\.

1. On the account dashboard page, in **App permissions**, choose **Change app permissions**\.

1. On the **App permissions** page, under **Amazon AppStream 2\.0**, choose **Revoke**\.