# Enable and Administer Google Drive for Your AppStream 2\.0 Users<a name="google-drive"></a>

Amazon AppStream 2\.0 supports the following persistent storage options for users in your organization: 
+ Google Drive for G Suite
+ OneDrive for Business
+ Home folders

You can enable one or more options for your organization\. When you enable Google Drive for G Suite for an AppStream 2\.0 stack, users of the stack can link their Google Drive for G Suite account to AppStream 2\.0\. Then they can sign into their Google Drive for G Suite account and access their Google Drive folder during application streaming sessions\. Any changes that they make to files or folders in Google Drive during those sessions are automatically backed up and synchronized, so that they are available to users outside of their streaming sessions\. 

**Important**  
You can enable Google Drive for G Suite for accounts in your G Suite domains only, but not for personal Gmail accounts\.

**Topics**
+ [Enable Google Drive for Your AppStream 2\.0 Users](#enable-google-drive)
+ [Disable Google Drive for Your AppStream 2\.0 Users](#disable-google-drive)

## Enable Google Drive for Your AppStream 2\.0 Users<a name="enable-google-drive"></a>

Before enabling Google Drive, you must do the following:
+ Have an active G Suite account with a valid organizational domain and user accounts in the domain to use with AppStream 2\.0\.
+ Configure an AppStream 2\.0 stack with an associated fleet\. 

   The fleet must use an image that uses a version of the AppStream 2\.0 agent released on or after May 31, 2018\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\. The fleet must also have access to the internet\.
+ Add Amazon AppStream 2\.0 as a trusted app in one or more domains associated with your G Suite account\. You can enable Google Drive for up to 10 domains\.

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
| US East \(N\. Virginia\) | 266080779488\-15n5q5nkiclp6m524qibnmhmbsg0hk92\.apps\.googleusercontent\.com | 
| US West \(Oregon\) | 1026466167591\-i4jmemrggsjomp9tnkkcs5tniggfiujb\.apps\.googleusercontent\.com | 
| Asia Pacific \(Mumbai\) | 325827353178\-coqs1c374mf388ctllrlls374dc1bmb2\.apps\.googleusercontent\.com  | 
| Asia Pacific \(Seoul\) | 562383781419\-am1i2dnvt050tmdltsvr36i8l2js40dj\.apps\.googleusercontent\.com  | 
| Asia Pacific \(Singapore\) | 856871139998\-4eia2n1db5j6gtv4c1rdte1fh1gec8vs\.apps\.googleusercontent\.com | 
| Asia Pacific \(Sydney\) | 151535156524\-b889372osskprm4dt1clpm53mo3m9omp\.apps\.googleusercontent\.com  | 
| Asia Pacific \(Tokyo\) | 922579247628\-qpl9kpihg3hu5dul2lphbjs4qbg6mjm2\.apps\.googleusercontent\.com  | 
| Europe \(Frankfurt\) | 643727794574\-1se5360a77i84je9j3ap12obov1ib76q\.apps\.googleusercontent\.com | 
| Europe \(Ireland\) | 599492309098\-098muc7ofjfo9vua5rm5u9q2k3mlok3j\.apps\.googleusercontent\.com  | 
| AWS GovCloud \(US\-West\) | `996065833880-litfkb2vfd7c65nt7s24r7t8le5bc9bl.apps.googleusercontent.com` For more information about using AppStream 2\.0 in AWS GovCloud \(US\-West\), see [Amazon AppStream 2\.0](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-appstream2.html) in the *AWS GovCloud \(US\) User Guide*\. | 

Follow these steps to enable Google Drive for your AppStream 2\.0 users\.

**To enable Google Drive while creating a stack**
+ Follow the steps in [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install), make sure that **Enable Google Drive** is selected, and that you have specified at least one organizational domain associated with your G Suite account\.

**To enable Google Drive for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to enable Google Drive\.

1. Below the stacks list, choose **Storage** and select **Enable Google Drive for G Suite**\.

1. In the **Enable Google Drive for G Suite** dialog box, in **G Suite domain name**, type the name of at least one organizational domain that is associated with your G Suite account\. To specify another domain, choose **Add another domain**, and type the name of the domain\.

1. After you add domain names, choose **Enable**\.

**Note**  
For guidance that you can provide your users to help them get started with using Google Drive during AppStream 2\.0 streaming sessions, see [Use Google Drive](google-drive-end-user.md)\.

## Disable Google Drive for Your AppStream 2\.0 Users<a name="disable-google-drive"></a>

You can disable Google Drive for a stack without losing user content that is already stored on Google Drive\. Disabling Google Drive for a stack has the following effects:
+ Users who are connected to active streaming sessions for the stack receive an error message\. They are informed that they do not have permissions to access their Google Drive\. 
+ Any new sessions that use the stack with Google Drive disabled do not display Google Drive\. 
+ Only the specific stack for which Google Drive is disabled is affected\.
+ Even if Google Drive is disabled for all stacks, AppStream 2\.0 does not delete the user content stored in their Google Drive\.

Follow these steps to disable Google Drive for an existing stack\.

**To disable Google Drive for an existing stack**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to disable Google Drive\.

1. Below the stacks list, choose **Storage**, and clear the **Enable Google Drive for G Suite** option\.

1. In the **Disable Google Drive for G Suite** dialog box, type `CONFIRM` \(case\-sensitive\) to confirm your choice, then choose **Disable**\.

   When users of the stack start their next AppStream 2\.0 streaming session, they can no longer access their Google Drive folder from within that session and future sessions\.