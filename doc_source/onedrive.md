# Enable and Administer OneDrive for Business for Your AppStream 2\.0 Users<a name="onedrive"></a>

AppStream 2\.0 supports the following persistent storage options for users in your organization: 
+ OneDrive for Business
+ Google Drive for G Suite
+ Home folders

You can enable one or more options for your organization\. When you enable OneDrive for Business for an AppStream 2\.0 stack, users of the stack can link their OneDrive for Business account to AppStream 2\.0\. Then they can sign into their OneDrive for Business account and access their OneDrive folder during application streaming sessions\. Any changes that they make to files or folders in OneDrive during those sessions are automatically backed up and synchronized, so that they are available to users outside of their streaming sessions\. 

**Important**  
You can enable OneDrive for Business for accounts in your OneDrive domains only, but not for personal accounts\. AppStream 2\.0 requires that you configure your Microsoft Azure Active Directory environment to allow end\-user consent to applications\. For more information, see [Configure how end\-users consent to applications](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-user-consent) in the Azure Active Directory [Application management](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/) documentation\.   
 The admin consent workflow lets administrators grant access to applications that require administrator approval\. If the admin consent workflow is configured in your Azure Active Directory environment, contact AWS Support\. For information about how to contact AWS Support, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

**Topics**
+ [Enable OneDrive for Your AppStream 2\.0 Users](#enable-onedrive)
+ [Disable OneDrive for Your AppStream 2\.0 Users](#disable-onedrive)

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

**Important**  
You must configure your Microsoft Azure Active Directory environment to allow end\-user consent to applications\. For more information, see [Configure how end\-users consent to applications](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-user-consent) in the Azure Active Directory [Application management](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/) documentation\.

**Provide Your Users with Permissions to Link OneDrive with AppStream 2\.0**

You must enable Integrated Apps in your Office 365 or OneDrive for Business admin console before users can link their OneDrive for Business account to AppStream 2\.0\.

1. Sign in to Office 365 or the OneDrive for Business admin console\.

1. In the left navigation pane of the console, choose **Settings**, **Services & add\-ins**\.

1. From the list of services and add\-ins, choose **Integrated Apps**\.

1. On the **Integrated apps** page, turn on the option to allow users in your organization to let third party web apps access their Office 365 information\.

**Note**  
For guidance that you can provide your users to help them get started with using OneDrive during AppStream 2\.0 streaming sessions, see [Use OneDrive for Business](onedrive-end-user.md)\.

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