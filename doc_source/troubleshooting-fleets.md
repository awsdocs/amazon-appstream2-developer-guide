# Troubleshooting Fleets<a name="troubleshooting-fleets"></a>

The following are possible issues that might occur when users connect to streaming sessions launched from fleet instances\.

**Topics**
+ [My applications won't work correctly unless I use the Internet Explorer defaults\. How do I restore the Internet Explorer default settings?](#troubleshooting-restore-ie-defaults)
+ [I need to persist environment variables across my fleet instances\.](#troubleshooting-persist-environment-variables)
+ [I want to change the default Internet Explorer home page for my users\.](#troubleshooting-change-homepage)

## My applications won't work correctly unless I use the Internet Explorer defaults\. How do I restore the Internet Explorer default settings?<a name="troubleshooting-restore-ie-defaults"></a>

If your AppStream 2\.0 environment includes applications that render elements, you might need to restore the Internet Explorer default settings to enable full enable access to the internet\. To do this, follow these steps to create a logon script and use Group Policy to enable the script\. The logon script runs as the user and restores these settings\. To use the Group Policy Management Console \(GPMC\) MMC snap\-in to perform this task, do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the GPMC\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with permissions to create Group Policy objects \(GPOs\)\. Link GPOs to the appropriate organizational units \(OUs\)\.

**To automatically restore the Internet Explorer default settings**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On your image builder, create a child folder of C:\\ \(for example, use C:\\Scripts\)\.

1. Copy the reset\-ie\.bat batch file from the location where you extracted the zip file in the previous procedure to C:\\Scripts\.

1. If you are not using Active Directory in your environment, open Local Group Policy Editor\. If you are using Active Directory, open the GPMC\. Locate the Scripts \(Logon\\Logoff\) policy setting: 
   + Local Group Policy Editor: 

     On your image builder, open the command prompt as an administrator, type `gpedit.msc`, and then press ENTER\. 

     Under **User Configuration**, expand **Windows Settings**, and then choose **Scripts \(Logon\\Logoff\)**\. 
   + GPMC: 

     In your directory or on your domain controller, open the command prompt as an administrator, type `gpmc.msc`, and then press ENTER\.

     In the left console tree, select the OU in which you want to create a new GPO, or use an existing GPO, and then do either of the following: : 
     + Create a new GPO by opening the context \(right\-click\) menu and choosing **Create a GPO in this domain, Link it here**\. For **Name**, provide a descriptive name for this GPO\.
     + Select an existing GPO\.

     Open the context menu for the GPO, and choose **Edit**\.

     Under **User Configuration**, expand **Policies**, **Windows Settings**, and then choose **Scripts \(Logon\\Logoff\)**\. 

1. In the **Logon Properties** dialog box, on the **Scripts** tab, choose **Add**, browse to and select C:\\Scripts\\reset\-ie\.bat, and then choose **OK**\. 

1. Choose **Apply**, **OK**\. 

1. To set the script as a Windows Logon script in either Local Group Policy Editor or the GPMC, locate the Group Policy administrative templates: 
   + Local Group Policy Editor: 

     Under **Computer Configuration**, expand **Administrative Templates**, **System**, and then choose **Group Policy**\. 
   + GPMC: 

     Under **Computer Configuration**, expand **Policies**, **Administrative Templates**, **System**, and then choose **Group Policy**\. 

1. Double\-click **Configure Logon Script Delay**\. 

1. In the **Configure Login Script Delay** policy setting, choose **Enabled**\.

1. Under **Options**, set the value to 0\.

1. Choose **Apply**, **OK**\.

1. Close Local Group Policy Editor or the GPMC\.

When end users connect to streaming sessions that are launched from the associated fleet instance, this batch file runs and restores the Internet Explorer default settings\.

## I need to persist environment variables across my fleet instances\.<a name="troubleshooting-persist-environment-variables"></a>

Environment variables enable you to dynamically pass settings across applications\. You can make user environment variables and system environment variables available across your fleet instances\. You can also create environment variables with limited scope, which is useful when you need to use the same environment variable with different values across different applications\. For more information, see [Persist Environment Variables](customize-fleets.md#customize-fleets-persist-environment-variables)\.

## I want to change the default Internet Explorer home page for my users\.<a name="troubleshooting-change-homepage"></a>

You can use Group Policy to set the default home page in Internet Explorer for your users\. You can also enable users to change the default page that you set\. For more information, see [Change the Default Internet Explorer Home Page for Users' Streaming Sessions](customize-fleets.md#customize-fleets-change-ie-homepage)\.