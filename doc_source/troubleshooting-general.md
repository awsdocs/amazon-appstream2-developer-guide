# General Troubleshooting<a name="troubleshooting-general"></a>

The following are general issues that might occur when you use Amazon AppStream 2\.0\.

**Topics**
+ [SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.](#troubleshooting-13)
+ [After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.](#troubleshooting-adfs-upn)
+ [I get an invalid redirect URI error\.](#troubleshooting-14)
+ [My image builders and fleets never reach the running state\. My DNS servers are in a Simple AD directory\.](#fleets-image-builders-dont-run-simple-ad)
+ [I've enabled application settings persistence for my users, but their persistent application settings aren't being saved or loaded\.](#app-settings-save-load-failure)
+ [I've enabled application settings persistence for my users, but for certain streaming applications, my users’ passwords aren’t persisting across sessions\.](#app-settings-passwords-not-persisting)
+ [Google Chrome data is filling the VHD file that contains my users' persistent application settings\. This is preventing their settings from persisting\. How can I manage the Chrome profile?](#chrome-filling-up-app-settings-VHD)
+ [I set up a custom domain for my embedded AppStream 2\.0 streaming sessions, but my AppStream 2\.0 streaming URLs aren't redirecting to my custom domain\.](#embedded-streaming-sessions-streaming-urls-not-redirected-to-custom-domain)
+ [I set up a custom domain for my embedded AppStream 2\.0 streaming sessions, but my custom domain isn't being maintained \(it doesn't display for users\)\.](#embedded-streaming-sessions-streaming-urls-not-displaying-for-users)

## SAML federation is not working\. The user is not authorized to view AppStream 2\.0 applications\.<a name="troubleshooting-13"></a>

This might happen because the inline policy that is embedded for the SAML 2\.0 federation IAM role does not include permissions to the stack ARN\. The IAM role is assumed by the federated user who is accessing an AppStream 2\.0 stack\. Edit the role permissions to include the stack ARN\. For more information, see [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md) and [Troubleshooting SAML 2\.0 Federation with AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_saml.html) in the *IAM User Guide*\.

## After federating from an ADFS portal, my streaming session doesn't start\. I am getting the error "Sorry connection went down"\.<a name="troubleshooting-adfs-upn"></a>

Set the claim rule's **Incoming Claim Type** for the **NameID** SAML attribute to **UPN** and try the connection again\.

## I get an invalid redirect URI error\.<a name="troubleshooting-14"></a>

This error occurs due to a malformed or invalid AppStream 2\.0 stack relay state URL\. Make sure that the relay state configured in your federation setup is the same as the stack relay state that is displayed in the stack details through the AppStream 2\.0 console\. If they are the same and the problem still persists, contact AWS Support\. For more information, see [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md)\.

## My image builders and fleets never reach the running state\. My DNS servers are in a Simple AD directory\.<a name="fleets-image-builders-dont-run-simple-ad"></a>

AppStream 2\.0 relies on the DNS servers within your VPC to return a non\-existent domain \(NXDOMAIN\) response for local domain names that don’t exist\. This enables the AppStream 2\.0\-managed network interface to communicate with the management servers\. 

When you create a directory with Simple AD, AWS Directory Service creates two domain controllers that also function as DNS servers on your behalf\. Because the domain controllers don't provide the NXDOMAIN response, they can't be used with AppStream 2\.0\.

## I've enabled application settings persistence for my users, but their persistent application settings aren't being saved or loaded\.<a name="app-settings-save-load-failure"></a>

AppStream 2\.0 automatically saves application settings that are created in certain locations on the Windows instance\. The settings are saved only if your application saves them to one of these locations\. For a list of supported locations, see [How Application Settings Persistence Works](how-it-works-app-settings-persistence.md)\. If your application is configured to save to C:\\Users\\%username% and your users' settings for the application aren’t persisting between sessions, the mount point might not be created\. This prevents the settings from being saved to the VHD file that contains your users’ persistent application settings\. 

To resolve this issue, follow these steps:

1. On the fleet instance, open File Explorer and browse to the user profile directory at C:\\Users\\%username%\.

1. Confirm whether this directory contains a symlink, and then do either of the following: 
   + If there is a symlink, confirm that it points to D:\\%username%\.
   + If there isn't a symlink, try to delete the C:\\Users\\%username% directory\.

     If you can’t delete this directory, identify the file in the directory that is preventing it from being deleted and the application that created the file\. Then contact the application vendor for information about how to change the file permissions or move the file\.

     If you can delete this directory, contact AWS Support for further guidance to resolve this issue\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## I've enabled application settings persistence for my users, but for certain streaming applications, my users’ passwords aren’t persisting across sessions\.<a name="app-settings-passwords-not-persisting"></a>

This issue occurs when:
+ Users are streaming applications such as Microsoft Outlook, which use the [Microsoft Data Protection API](https://docs.microsoft.com/en-us/windows/desktop/seccng/cng-dpapi)\.
+ App settings persistence is enabled for streaming instances that are not joined to Active Directory domains\. 

In cases where a streaming instance is not joined to an Active Directory domain, the Windows user, PhotonUser, is different on each fleet instance\. Due to the way in which the DPAPI security model works, users' passwords don’t persist for applications that use DPAPI in this scenario\. In cases where streaming instances are joined to an Active Directory domain and the user is a domain user, the Windows user name is that of the logged in user, and users’ passwords persist for applications that use DPAPI\.

## Google Chrome data is filling the VHD file that contains my users' persistent application settings\. This is preventing their settings from persisting\. How can I manage the Chrome profile?<a name="chrome-filling-up-app-settings-VHD"></a>

By default, Google Chrome stores both user data and the local disk cache in the Windows user profile\. To prevent the local disk cache data from filling the VHD file that contains users' persistent application settings, configure Chrome to save only the user data\. To do so, on the fleet instance, open the command line as an administrator and start Chrome with the following parameters to change the location of the disk cache:

`chrome.exe --disk-cache-dir C:\`*path\-to\-unsaved\-location*`\`

Running Chrome with these parameters prevents the disk cache from being persisted between AppStream 2\.0 sessions\.

## I set up a custom domain for my embedded AppStream 2\.0 streaming sessions, but my AppStream 2\.0 streaming URLs aren't redirecting to my custom domain\.<a name="embedded-streaming-sessions-streaming-urls-not-redirected-to-custom-domain"></a>

To resolve this issue, verify that when you created your AppStream 2\.0 streaming URL, you replaced the AppStream 2\.0 endpoint with your custom domain\. By default, AppStream 2\.0 streaming URLs are formatted as follows:

```
https://appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode
```

To replace the default AppStream 2\.0 endpoint in your streaming URL, replace **https://appstream2\.***region* in the URL with your custom domain\. For example, if your custom domain is **training\.example\.com**, your new streaming URL must follow this format:

```
https://training.example.com/authenticate?parameters=authenticationcode
```

For more information about configuring custom domains for embedded AppStream 2\.0 streaming sessions, see [Configuration Requirements for Using Custom Domains](embed-streaming-sessions.md#configuration-requirements-custom-domains)\.

## I set up a custom domain for my embedded AppStream 2\.0 streaming sessions, but my custom domain isn't being maintained \(it doesn't display for users\)\.<a name="embedded-streaming-sessions-streaming-urls-not-displaying-for-users"></a>

This issue occurs when the reverse proxy that you use to set up your AppStream 2\.0 custom domain doesn't forward the custom header **appstream\-custom\-url\-domain**\. 

When this issue occurs, run a network trace\. The trace might show that the streaming URL that uses your custom domain redirects to a URL that follows this format:

```
https://random-string.appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode
```

For example, rather than **training\.example\.com** displaying in your streaming URL as follows:

```
https://training.example.com/authenticate?parameters=authenticationcode
```

The following URL, which contains a random string, might display for users:

```
https://a7c7cace68bef535c93583de4526f359082092651569a7d12aca825b.appstream2.us-west-2.aws.amazon.com/authenticate?parameters=authenticationcode
```

To resolve this issue, make sure that the value of the custom header of the webpage that hosts the embedded streaming sessions matches your custom domain name\. For example, if your custom domain name is **training\.example\.com**, the custom header must match this value, as shown in the following example\. 

```
Header name: appstream-custom-url-domain
Header value: training.example.com
```

For more information about configuring custom domains for embedded AppStream 2\.0 streaming sessions, see [Configuration Requirements for Using Custom Domains](embed-streaming-sessions.md#configuration-requirements-custom-domains)\.