# General Troubleshooting<a name="troubleshooting-general"></a>

The following are possible general issues you might have while using Amazon AppStream 2\.0\.

**Topics**
+ [SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.](#troubleshooting-13)
+ [After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.](#troubleshooting-adfs-upn)
+ [I get an invalid redirect URI error\.](#troubleshooting-14)
+ [My image builders and fleets never reach the running state\. My DNS servers are in a Simple AD directory\.](#fleets-image-builders-dont-run-simple-ad)
+ [My stack's home folders aren't working correctly\.](#troubleshooting-s3-failures)
+ [My users can't access their home folder directory from one of our applications\.](#alternate-path-accessing-home-folders)
+ [I've enabled application settings persistence for my users, but their persistent application settings aren't being saved or loaded\.](#app-settings-save-load-failure)
+ [I've enabled app settings persistence for my users, but for certain streaming apps, my users’ passwords aren’t persisting across sessions\.](#app-settings-passwords-not-persisting)
+ [Google Chrome data is filling the VHD file that contains my users' persistent application settings\. This is preventing their settings from persisting\. How can I manage the Chrome profile?](#chrome-filling-up-app-settings-VHD)
+ [My users can’t copy and paste between their local device and their streaming session\.](#copy-paste-doesnt-work)
+ [Some keyboard shortcuts aren’t working for users during their streaming sessions\.](#keyboard-shortcuts-dont-work)

## SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.<a name="troubleshooting-13"></a>

This might happen because the inline policy that is embedded for the SAML 2\.0 federation IAM role does not include permissions to the stack ARN\. The IAM role is assumed by the federated user who is accessing an AppStream 2\.0 stack\. Edit the role permissions to include the stack ARN\. For more information, see [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md) and [Troubleshooting SAML 2\.0 Federation with AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_saml.html) in the *IAM User Guide*\.

## After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.<a name="troubleshooting-adfs-upn"></a>

Set the claim rule's **Incoming Claim Type** for the **NameID** SAML attribute to **UPN** and try the connection again\.

## I get an invalid redirect URI error\.<a name="troubleshooting-14"></a>

This error occurs due to a malformed or invalid AppStream 2\.0 stack relay state URL\. Make sure that the relay state configured in your federation setup is the same as the stack relay state that is displayed in the stack details through the AppStream 2\.0 console\. If they are the same and the problem still persists, contact AWS Support\. For more information, see [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md)\.

## My image builders and fleets never reach the running state\. My DNS servers are in a Simple AD directory\.<a name="fleets-image-builders-dont-run-simple-ad"></a>

AppStream 2\.0 relies on the DNS servers within your VPC to return a non\-existent domain \(NXDOMAIN\) response for local domain names that don’t exist\. This enables the AppStream 2\.0\-managed network interface to communicate with the management servers\. 

When you create a directory with Simple AD, AWS Directory Service creates two domain controllers that also function as DNS servers on your behalf\. Because the domain controllers don't provide the NXDOMAIN response, they can't be used with AppStream 2\.0\.

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

## I've enabled application settings persistence for my users, but their persistent application settings aren't being saved or loaded\.<a name="app-settings-save-load-failure"></a>

AppStream 2\.0 automatically saves application settings that are created in certain locations on the Windows instance\. The settings are saved only if your application saves them to one of these locations\. For a list of supported locations, see [How Application Settings Persistence Works](how-it-works-app-settings-persistence.md)\. If your application is configured to save to C:\\Users\\%username% and your users' settings for the application aren’t persisting between sessions, the mount point might not be created\. This prevents the settings from being saved to the VHD file that contains your users’ persistent application settings\. 

To resolve this issue, follow these steps:

1. On the fleet instance, open File Explorer and browse to the user profile directory at C:\\Users\\%username%\.

1. Confirm whether this directory contains a symlink, and then do either of the following: 
   + If there is a symlink, confirm that it points to D:\\%username%\.
   + If there isn't a symlink, try to delete the C:\\Users\\%username% directory\.

     If you can’t delete this directory, identify the file in the directory that is preventing it from being deleted and the application that created the file\. Then contact the application vendor for information about how to change the file permissions or move the file\.

     If you can delete this directory, contact AWS Support for further guidance to resolve this issue\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## I've enabled app settings persistence for my users, but for certain streaming apps, my users’ passwords aren’t persisting across sessions\.<a name="app-settings-passwords-not-persisting"></a>

This issue occurs when:
+ Users are streaming applications such as Microsoft Outlook, which use the [Microsoft Data Protection API](https://docs.microsoft.com/en-us/windows/desktop/seccng/cng-dpapi)\.
+ App settings persistence is enabled for streaming instances that are not joined to Active Directory domains\. 

In cases where a streaming instance is not joined to an Active Directory domain, the Windows user, PhotonUser, is different on each fleet instance\. Due to the way in which the DPAPI security model works, users' passwords don’t persist for applications that use DPAPI in this scenario\. In cases where streaming instances are joined to an Active Directory domain and the user is a domain user, the Windows user name is that of the logged in user, and users’ passwords persist for applications that use DPAPI\.

## Google Chrome data is filling the VHD file that contains my users' persistent application settings\. This is preventing their settings from persisting\. How can I manage the Chrome profile?<a name="chrome-filling-up-app-settings-VHD"></a>

By default, Google Chrome stores both user data and the local disk cache in the Windows user profile\. To prevent the local disk cache data from filling the VHD file that contains users' persistent application settings, configure Chrome to save only the user data\. To do so, on the fleet instance, open the command line as an administrator and start Chrome with the following parameters to change the location of the disk cache:

`chrome.exe --disk-cache-dir C:\`*path\-to\-unsaved\-location*`\`

Running Chrome with these parameters prevents the disk cache from being persisted between AppStream 2\.0 sessions\.

## My users can’t copy and paste between their local device and their streaming session\.<a name="copy-paste-doesnt-work"></a>

AppStream 2\.0 takes advantage of the [W3C specification](https://www.w3.org/TR/2017/WD-clipboard-apis-20170929/) for enabling asynchronous clipboard operations in web applications\. This enables users to copy and paste content between their local device and their streaming session in the same ways that they copy and paste between applications on their local device, including using keyboard shortcuts\. 

The only browser that currently supports the W3C asynchronous clipboard specification is Google Chrome version 66 or later, which supports copying and pasting only for text\. For all other browsers, users can use the clipboard feature in the AppStream 2\.0 web portal, which provides a dialog box for copying or pasting text\.

If your users run into issues using the clipboard during their streaming sessions, you can provide them with the following information: 
+ **I’m using Chrome version 66 or later, and keyboard shortcuts aren’t working\.** 

  Chrome displays a prompt for you to choose whether to allow AppStream 2\.0 to access content copied to the clipboard\. Choose **Allow** to enable pasting to your remote session\. If you’re copying text from your remote session to your local device, both the Chrome application and the tab containing your streaming session must stay in focus on your local device long enough for the text to be copied from your streaming session\. Small amounts of text should be copied almost immediately, but for large amounts of text, you might need to wait 1 to 2 seconds before switching away from Chrome or from the tab containing your streaming session\. The time required to copy the text varies based on network conditions\.
+ **Copying and pasting doesn’t work when I try to copy and paste a large amount of text\.**

  AppStream 2\.0 has a 2 MB limit for the amount of text that you can copy and paste between your local device and your streaming session\. If you try to copy more than 2 MB, no text is copied\. This limit doesn’t apply if you try to copy and paste text between applications on your local device or between applications in your streaming session\. If you need to copy or paste text more than 2 MB between your local device and your streaming session, you can divide it into smaller chunks or upload it as a file instead\.
+ **I’m using the AppStream 2\.0 web portal clipboard feature to paste text to my streaming session and it’s not working\.**

  In some cases, after you paste text into the clipboard dialog box and the dialog box closes, nothing happens when you try to use keyboard shortcuts to paste the text in your streaming session\. This issue occurs because when the clipboard dialog box appears, it takes the focus away from your streaming application\. After the dialog box closes, the focus might not automatically return to your streaming application\. Clicking your streaming application should return the focus to it and enable you to use keyboard shortcuts to paste your text into your streaming session\.

## Some keyboard shortcuts aren’t working for users during their streaming sessions\.<a name="keyboard-shortcuts-dont-work"></a>

The following keyboard shortcuts work on users' local computers, but are not passed to AppStream 2\.0 streaming sessions:

Windows:
+ Win\+L
+ Ctrl\+Alt\+Del

Mac:
+ Ctrl\+F3 
+ All shortcuts that use Alt or Option key combinations

This issue is due to the following limitations on users’ local computers:
+ The keyboard shortcuts are filtered by the operating system that is running on users’ local computers and not propagated to the browsers on which users are accessing AppStream 2\.0\. This behavior applies to the Windows Win\+L and Ctrl\+Alt\+Del keyboard shortcuts and Mac Ctrl\+F3 keyboard shortcut\.
+ When used with web applications, some keyboard shortcuts are filtered by the browser and don’t generate an event for the web applications\. As a result, the web applications can’t respond to the keyboard shortcuts typed by users\. 
+ The keyboard shortcuts are translated by the browser before a keyboard event is generated and so are not translated correctly\. For example, Alt key combinations and Option key combinations on Mac computers are translated as if they are Alt Graph key combinations on Windows\. When this occurs, the results are not as the users intend when they use these key combinations\. 