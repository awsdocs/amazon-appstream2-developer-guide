# Customize AppStream 2\.0 Fleets<a name="customize-fleets"></a>

By customizing AppStream 2\.0 fleet instances, you can define specific aspects of your AppStream 2\.0 environment to optimize your users' application streaming experience\. For example, you can persist environment variables to dynamically pass settings across applications and set default file associations that are applied to all of your users\. At a high level, customizing a fleet instance includes the following tasks: 
+ Connecting to an image builder and customizing it as needed\.
+ On the image builder, using Image Assistant to create a new image that includes your customizations\.
+ Creating a new fleet instance or modifying an existing one\. When you configure the fleet instance, select the new customized image that you created\.
+ Creating a new stack or modifying an existing one and associating it with your fleet instance\.

**Note**  
For certain fleet customizations, in Active Directory environments, you might need to use the Group Policy Management Console \(GPMC\) to update Group Policy object \(GPO\) settings on a domain\-joined computer\.

**Topics**
+ [Persist Environment Variables](#customize-fleets-persist-environment-variables)
+ [Set Default File Associations for Your Users](#customize-fleets-set-default-file-associations)
+ [Set Google Chrome as the Default Browser for Users' Streaming Sessions](#customize-fleets-set-chrome-default-browser)
+ [Change the Default Internet Explorer Home Page for Users' Streaming Sessions](#customize-fleets-change-ie-homepage)

## Persist Environment Variables<a name="customize-fleets-persist-environment-variables"></a>

Environment variables enable you to dynamically pass settings across applications\. For example, many engineering applications rely on environment variables to specify the IP address or host name of a license server to locate and check out a license from that server\. 

Follow the steps in these procedures to make environment variables available across your fleet instances\. 

**Note**  
If you are using Active Directory and Group Policy with AppStream 2\.0, keep in mind that streaming instances must be joined to an Active Directory domain to use Group Policy for environment variables\. For information about how to configure the Group Policy **Environment Variable** preference item, see [Configure an Environment Variable Item](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772047(v=ws.11)) in the Microsoft documentation\.

**To change system environment variables on an image builder**

This procedure applies only to system environment variables, not user environment variables\. To change user environment variables that persist across your fleet instances, follow the steps in the next procedure\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Connect in Administrator mode to the image builder on which you want to change system environment variables\. 

1. Choose the Windows **Start** menu, open the context \(right\-click\) menu for **Computer**, and then choose **Properties**\.

1. In the navigation pane, choose **Advanced system settings**\. 

1. In **System variables**, change the environment variables that you want to persist across your fleet instances, and then choose** OK**\.

1. On the image builder desktop, open Image Assistant and install and configure applications as needed\. 

   The changes to the system environment variables persist across your fleet instances and are available to streaming sessions launched from those instances\. 
**Note**  
Setting AWS CLI credentials as system environment variables might prevent AppStream 2\.0 from creating the image\.

**To change user environment variables on an image builder**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Connect in Administrator mode to the image builder on which you want to change user environment variables\.

1. Create a child folder of C:\\ drive for the script \(for example, C:\\Scripts\)\.

1. Open Notepad to create the new script\.

1. In Notepad, enter the following lines:

   `setx `*variable* *value*

   Where:

   *variable* is the variable name to be used

   *value* is the value for the given variable name

1. Choose** File**, **Save**\. Name the file and save it with the \.bat extension to C:\\Scripts\. For example, name the file CreateVariable\.bat\.

1. Open Local Group Policy Editor by opening the command prompt as an administrator, typing `gpedit.msc`, and then pressing ENTER\.

1. In the console tree, under **Computer Configuration**, expand **Administrative Templates**, **System**, and then choose **Group Policy**\. 

1. Double\-click **Configure Logon Script Delay**\.

1. In the **Configure Login Script Delay **dialog box, choose **Enabled**\.

1. Under **Options**, set the value to 0\.

1. Choose **Apply**, **OK**\.

1. In the console tree, under **User Configuration**, expand **Windows Settings**, and then choose **Scripts \(Logon/Logoff\)**\.

1. Double\-click** Logon**\. 

1. In the **Logon Properties** dialog box, on the **Scripts** tab, choose **Add,** and then browse to C:\\Scripts\\CreateVariable\.bat\.

1. Choose **Apply**, **OK**\.

1. Close Local Group Policy Editor\.

1. On the image builder desktop, open Image Assistant and install and configure applications as needed\. 

   The logon script runs when fleet users log in, setting the user environment variable\. This process makes the variable available in the associated streaming sessions\.

**To create an environment variable with limited scope**

Follow these steps to create an environment variable that is limited in scope to the processes that are spawned off the script\. This approach is useful when you need to use the same environment variable name with different values for different applications\. For example, if you have two different applications that use the environment variable "LIC\_SERVER", but each application has a different value for "LIC\_SERVER"\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Connect in Administrator mode to the image builder on which you want to create an environment variable with a limited scope\.

1. Create a child folder of C:\\ drive for the script \(for example, C:\\Scripts\)\.

1. Open Notepad to create the new script, and enter the following lines:

   `set `*variable*=*value*

   `start " "C:\path\to\application.exe` 

   Where:

   *variable* is the variable name to be used

   *value* is the value for the given variable name
**Note**  
If the application path includes spaces, the entire string must be encapsulated within quotation marks\. For example:   
`start " " "C:\Program Files\application.exe"`

1. Choose** File**, **Save**\. Name the file and save it with the \.bat extension to C:\\Scripts\. For example, name the file LaunchApp\.bat\.

1. If needed, repeat steps 4 and 5 to create a script for each additional application that requires its own environment variable and values\. 

1. On the image builder desktop, start Image Assistant\.

1. Choose **Add Application**, browse to C:\\Scripts, and select one of the scripts that you created in step 5\. Choose **Save**\.

1. If you created multiple scripts, repeat step 8 for each script\.

1. Continue installing and configuring applications as needed\.

   The environment variable and specific value are now available for processes that are run from the script\. Other processes cannot access this variable and value\. 

## Set Default File Associations for Your Users<a name="customize-fleets-set-default-file-associations"></a>

The associations for application file extensions are set on a per\-user basis and so are not automatically applied to all users who launch AppStream 2\.0 streaming sessions\. For example, if you set Adobe Reader as the default application for \.pdf files on your image builder, this change is not applied to your users\. 

**To set default file associations for your users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Connect in Administrator mode to the image builder on which you want to set file associations\.

1. Set file associations as needed\.

1. Open the Windows command prompt as an administrator\.

1. At the command prompt, type the following command to export the image builder file associations as an XML file, and then press ENTER: 

   `dism.exe/online/export-DefaultAppAssociations:c:\default_associations.xml`

   If you receive an error message stating that you cannot service a running 64\-bit operating system with a 32\-bit version of DISM, close the command prompt window\. Open File Explorer, browse to C:\\Windows\\System32, right\-click cmd\.exe, choose **Run as Administrator**, and run the command again\.

1. Open Local Group Policy Editor by opening the command prompt as an administrator, typing `gpedit.msc`, and then pressing ENTER\.

1. In the console tree, under **Computer Configuration**, expand **Administrative Templates**, **Windows Components**, and then choose **File Explorer**\. 

1. Double\-click **Set a default associations configuration file**\.

1. In the **Set a default associations configuration file properties** dialog box, choose **Enabled**, and enter this path: `c:\default_associations.xml`\.

1. Choose **Apply**, **OK**\.

1. Close Local Group Policy Editor\.

1. On the image builder desktop, open Image Assistant and install and configure applications as needed\.

   The file associations that you configured are applied to the fleet instances and user streaming sessions that are launched from those instances\. 

## Set Google Chrome as the Default Browser for Users' Streaming Sessions<a name="customize-fleets-set-chrome-default-browser"></a>

By default, new user accounts for Microsoft Windows have Internet Explorer set as the default browser\. Follow these steps to set Google Chrome as the default browser for your fleet instances\.

**To set Google Chrome as the default browser for fleet instances**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Connect in Administrator mode to the image builder on which you want to set Chrome as the default browser\.

1. On the image builder desktop, start Image Assistant\.

1. Choose **Add Application**, browse to the location where Chrome is installed \(for example, C:\\Program Files \(x86\)\\Google\\Chrome\\Application\\\), and select chrome\.exe\. 

1. In the **Edit Application Setting** dialog box, in **Launch Parameters**, enter the following: 

   `--make-default-browser-for-user --no-first-run`

1. Choose **Save**\.

1. Continue installing and configuring applications as needed\. 

   Users who are connected to streaming sessions launched from those fleet instances have Google Chrome as the default browser for http:// and https:// connections\. The users’ existing application preferences for opening files with \.htm and \.html extensions are not changed\.

## Change the Default Internet Explorer Home Page for Users' Streaming Sessions<a name="customize-fleets-change-ie-homepage"></a>

You can use Group Policy to change the default Internet Explorer home page for users' streaming sessions and optionally, enable your users to change the default home page\. To use the GPMC MMC snap\-in to perform this task, do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the GPMC\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with permissions to create GPOs\. Link GPOs to the appropriate organizational units \(OUs\)\.

**To change the default Internet Explorer home page by using a Group Policy administrative template**

You can use an administrative template in Group Policy to set a default home page that users can’t change\. For more information about administrative templates, see [Edit Administrative Template Policy Settings](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771479(v=ws.11)) in the Microsoft documentation\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. If you are not using Active Directory in your environment, open Local Group Policy Editor\. If you are using Active Directory, open the GPMC\. Locate the Scripts \(Logon\\Logoff\) policy setting: 
   + Local Group Policy Editor: 

     On your image builder, open the command prompt as an administrator, type `gpedit.msc`, and then press ENTER\. 

     Under **User Configuration**, expand **Administrative Templates**, **Windows Components**, and then choose **Internet Explorer**\. 
   + GPMC: 

     In your directory or on a domain controller, open the command prompt as an administrator, type `gpmc.msc`, and then press ENTER\.

     In the left console tree, select the OU in which you want to create a new GPO, or use an existing GPO, and then do either of the following: : 
     + Create a new GPO by opening the context \(right\-click\) menu and choosing **Create a GPO in this domain, Link it here**\. For **Name**, provide a descriptive name for this GPO\.
     + Select an existing GPO\.

     Open the context menu for the GPO, and choose **Edit**\.

     Under **User Configuration**, expand **Policies**, **Administrative Templates**, **Windows Components**, and then choose **Internet Explorer**\. 

1. Double\-click **Disable changing home page settings**, choose **Enabled**, and in **Home Page**, enter a URL\.

1. Choose **Apply**, **OK**\.

1. Close Local Group Policy Editor or the GPMC\.

**To change the default Internet Explorer home page by using Group Policy preferences**

You can use Group Policy preferences to set a default home page that users can change\. For more information about working with Group Policy preferences, see [Configure a Registry Item](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)) and [Group Policy Preferences Getting Started Guide ](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731892(v=ws.10)) in the Microsoft documentation\.

1. In your directory or on a domain controller, open the command prompt as an administrator, type `gpmc.msc`, and then press ENTER\.

1. In the left console tree, select the OU in which you want to create a new GPO, or use an existing GPO, and then do either of the following: 
   + Create a new GPO by opening the context \(right\-click\) menu and choosing **Create a GPO in this domain, Link it here**\. For **Name**, provide a descriptive name for this GPO\.
   + Select an existing GPO\.

1. Open the context menu for the GPO, and choose **Edit**\. 

1. Under **User Configuration**, expand **Preferences**, and then choose **Windows Settings**\. 

1. Open the context \(right\-click\) menu for **Registry** and choose **New**, **Registry Item**\.

1. In the **New Registry Properties** dialog box, specify the following registry settings for Group Policy to configure: 
   + For **Action**, choose **Update**\. 
   + For **Hive**, choose **HKEY\_CURRENT\_USER**\.
   + For **Key Path**, browse to and select HKEY\_CURRENT\_USER\\SOFWARE\\Microsoft\\Internet Explorer\\Main\.
   + For **Value Name**, enter **Start Page**\.
   + For **Value Data**, enter your home page URL\.

1. On the **Common **tab, choose **Apply Once**, **Do not Re\-Apply**\. 
**Note**  
To enable your users to choose the **Use Default** button in their Internet Explorer browser settings and reset their default home page to your company home page, you can also set a value for Default\_Page\_URL without choosing **Apply Once** and **Do not Re\-Apply**\. 

1. Choose **OK** and close the GPMC\.