# Customize an AppStream 2\.0 Fleet to Optimize Your Users' Application Streaming Experience<a name="customize-fleets"></a>

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
+ [Disable Internet Explorer Enhanced Security Configuration](#customize-fleets-disable-ie-esc)
+ [Change the Default Internet Explorer Home Page for Users' Streaming Sessions](#customize-fleets-change-ie-homepage)
+ [User and Instance Metadata for AppStream 2\.0 Fleets](#customize-fleets-user-instance-metadata)

## Persist Environment Variables<a name="customize-fleets-persist-environment-variables"></a>

Environment variables enable you to dynamically pass settings across applications\. For example, many engineering applications rely on environment variables to specify the IP address or host name of a license server to locate and check out a license from that server\. 

Follow the steps in these procedures to make environment variables available across your fleet instances\. 

**Topics**
+ [Change System Environment Variables](#customize-fleets-system-environment-variables)
+ [Change User Environment Variables](#customize-fleets-user-environment-variables)
+ [Create an Environment Variable That is Limited in Scope](#customize-fleets-environment-variable-limited-scope)

**Note**  
If you are using Active Directory and Group Policy with AppStream 2\.0, keep in mind that streaming instances must be joined to an Active Directory domain to use Group Policy for environment variables\. For information about how to configure the Group Policy **Environment Variable** preference item, see [Configure an Environment Variable Item](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772047(v=ws.11)) in the Microsoft documentation\.

### Change System Environment Variables<a name="customize-fleets-system-environment-variables"></a>

Follow these steps to change system environment variables across your fleet instances\. 

**To change system environment variables on an image builder**

This procedure applies only to system environment variables, not user environment variables\. To change user environment variables that persist across your fleet instances, follow the steps in the next procedure\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder on which to change system environment variables, verify that it is in the **Running** state, and choose **Connect**\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, specify the credentials for a domain user account that has local administrator permissions on the image builder, then choose **Log in**\.

1. Choose the Windows **Start** button, open the context \(right\-click\) menu for **Computer**, and then choose **Properties**\.

1. In the navigation pane, choose **Advanced system settings**\. 

1. In **System variables**, change the environment variables that you want to persist across your fleet instances, and then choose** OK**\.

1. On the image builder desktop, open Image Assistant\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   The changes to the system environment variables persist across your fleet instances and are available to streaming sessions launched from those instances\. 
**Note**  
Setting AWS CLI credentials as system environment variables might prevent AppStream 2\.0 from creating the image\.

### Change User Environment Variables<a name="customize-fleets-user-environment-variables"></a>

Follow these steps to change user environment variables across your fleet instances\. 

**To change user environment variables**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder on which to change user environment variables, verify that it is in the **Running** state, and choose **Connect**\.

1. On the **Local User** tab, choose **Template User**\. 

   **Template User** lets you create default application and Windows settings for your users\. For more information, see "Creating Default Application and Windows Settings for Your AppStream 2\.0 Users" in [Default Application and Windows Settings and Application Launch Performance](customizing-appstream-images.md)\.

1. On the image builder, choose the Windows **Start** button, **Control Panel**, **User Accounts**\. 

1. Choose **User Accounts** again\. In the left navigation pane, choose **Change my environment variables\.**

1. Under **User environment variables** for **DefaultProfileUser**, set or create the user environment variables as needed, then choose **OK**\.

1. This disconnects your current session and opens the login menu\. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, and log in as a domain user who has local administrator permissions on the image builder\.

1. On the image builder desktop, open Image Assistant\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

### Create an Environment Variable That is Limited in Scope<a name="customize-fleets-environment-variable-limited-scope"></a>

Follow these steps to create an environment variable that is limited in scope to the processes that are spawned off the script\. This approach is useful when you need to use the same environment variable name with different values for different applications\. For example, if you have two different applications that use the environment variable "LIC\_SERVER", but each application has a different value for "LIC\_SERVER"\.

**To create an environment variable that is limited in scope**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder on which to create an environment variable that is limited in scope, verify that it is in the **Running** state, and choose **Connect**\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, specify the credentials for a domain user account that has local administrator permissions on the image builder, then choose **Log in**\.

1. Create a child folder of C:\\ drive for the script \(for example, C:\\Scripts\)\.

1. Open Notepad to create the new script, and enter the following lines:

   `set `*variable*=*value*

   `start " " "C:\path\to\application.exe"` 

   Where:

   *variable* is the variable name to be used

   *value* is the value for the given variable name
**Note**  
If the application path includes spaces, the entire string must be encapsulated within quotation marks\. For example:   
`start " " "C:\Program Files\application.exe"`

1. Choose** File**, **Save**\. Name the file and save it with the \.bat extension to C:\\Scripts\. For example, name the file LaunchApp\.bat\.

1. If needed, repeat steps 4 and 5 to create a script for each additional application that requires its own environment variable and values\. 

1. On the image builder desktop, start Image Assistant\.

1. Choose **Add App**, navigate to C:\\Scripts, and select one of the scripts that you created in step 5\. Choose **Open**\.

1. In the **App Launch Settings** dialog box, keep or change the settings as needed\. When you're done, choose **Save**\.

1. If you created multiple scripts, repeat steps 8 and 9 for each script\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   The environment variable and specific value are now available for processes that are run from the script\. Other processes cannot access this variable and value\. 

## Set Default File Associations for Your Users<a name="customize-fleets-set-default-file-associations"></a>

The associations for application file extensions are set on a per\-user basis and so are not automatically applied to all users who launch AppStream 2\.0 streaming sessions\. For example, if you set Adobe Reader as the default application for \.pdf files on your image builder, this change is not applied to your users\. 

**Note**  
The following steps must be performed on an image builder that is joined to an Active Directory domain\. In addition, your fleet must be joined to an Active Directory domain\. Otherwise, the default file associations that you set are not applied\.

**To set default file associations for your users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose the image builder on which to set default file associations, verify that it is in the **Running** state, and choose **Connect**\.

1. Choose the **Directory User** tab, specify the credentials for a domain user account that has local administrator permissions on the image builder, then choose **Log in**\.

1. Set default file associations as needed\.

1. Open the Windows command prompt as an administrator\.

1. At the command prompt, type the following command to export the image builder file associations as an XML file, and then press ENTER: 

   `dism.exe /online /export-DefaultAppAssociations:c:\default_associations.xml`

   If you receive an error message stating that you cannot service a running 64\-bit operating system with a 32\-bit version of DISM, close the command prompt window\. Open File Explorer, browse to C:\\Windows\\System32, right\-click cmd\.exe, choose **Run as Administrator**, and run the command again\.

1. You can use either Local Group Policy Editor or the GPMC to set a default associations configuration file:
   + Local Group Policy Editor:

     On your image builder, open the command prompt as an administrator, type `gpedit.msc`, and then press ENTER\. 

     In the console tree, under **Computer Configuration**, expand **Administrative Templates**, **Windows Components**, and then choose **File Explorer**\.
   + GPMC: 

     In your directory or on a domain controller, open the command prompt as an administrator, type `gpmc.msc`, and then press ENTER\.

     In the left console tree, select the OU in which you want to create a new GPO, or use an existing GPO, and then do either of the following:
     + Create a new GPO by opening the context \(right\-click\) menu and choosing **Create a GPO in this domain, Link it here**\. For **Name**, provide a descriptive name for this GPO\.
     + Select an existing GPO\.

     Open the context menu for the GPO, and choose **Edit**\.

     Under **User Configuration**, expand **Policies**, **Administrative Templates**, **Windows Components**, and then choose **File Explorer**\. 

1. Double\-click **Set a default associations configuration file**\.

1. In the **Set a default associations configuration file properties** dialog box, choose **Enabled**, and do one of the following:
   + If you are using Local Group Policy Editor, enter this path: `c:\default_associations.xml`\. 
   + If you are using the GPMC, enter a network path\. For example, `\\networkshare\default_associations.xml`\.

1. Choose **Apply**, **OK**\.

1. Close Local Group Policy Editor or the GPMC\.

1. On the image builder desktop, open Image Assistant\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   The file associations that you configured are applied to the fleet instances and user streaming sessions that are launched from those instances\. 

## Disable Internet Explorer Enhanced Security Configuration<a name="customize-fleets-disable-ie-esc"></a>

Internet Explorer Enhanced Security Configuration \(ESC\) places servers and Internet Explorer in a configuration that limits exposure to the internet\. However, this configuration can impact the AppStream 2\.0 end user experience\. Users who are connected to AppStream 2\.0 streaming sessions may find that websites do not display or perform as expected when: 
+ Internet Explorer ESC is enabled on fleet instances from which users' streaming sessions are launched
+ Users run Internet Explorer during their streaming sessions
+ Applications use Internet Explorer to load data

**To disable Internet Explorer Enhanced Security Configuration**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder on which to disable Internet Explorer ESC, verify that it is in the **Running** state, and choose **Connect**\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, specify the credentials for a domain user account that has local administrator permissions on the image builder, then choose **Log in**\.

1. On the image builder, disable Internet Explorer ESC by doing the following:

   1. Open Server Manager\. Choose the Windows **Start** button, and then choose **Server Manager**\.

   1. In the left navigation pane, choose **Local Server**\. 

   1. In the right properties pane, choose the **On** link next to IE Enhanced Security Configuration****\.

   1. In the **Internet Explorer Enhanced Configuration** dialog box, choose the **Off** option under **Administrators** and **Users**, then choose **OK**\.

1. In the upper right area of the image builder desktop, choose **Admin Commands**, **Switch User**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/admin-commands-switch-user.png)

1. This disconnects your current session and opens the login menu\. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Template User**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, and log in as a domain user who does not have local administrator permissions on the image builder\.

1. Open Internet Explorer and reset your settings by doing the following:

   1. In the upper right area of the Internet Explorer browser window, choose the **Tools** icon, then choose **Internet options**\.

   1. Choose the **Advanced **tab, then choose **Reset**\.

   1. When prompted to confirm your choice, choose **Reset** again\.

   1. When the **Reset Internet Explorer Settings** message displays, choose **Close**\.

1. Choose **Admin Commands**, **Switch User**, and then do either of the following: 
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, and log in with the same domain user account that you used in step 4\.

1. On the image builder desktop, open Image Assistant\.

1. In **Step 2\. Configure Apps**, choose **Save settings**\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

## Change the Default Internet Explorer Home Page for Users' Streaming Sessions<a name="customize-fleets-change-ie-homepage"></a>

You can use Group Policy to change the default Internet Explorer home page for users' streaming sessions\. Alternatively, if you do not have Group Policy in your environment or prefer not to use Group Policy, you can use the AppStream 2\.0 Template User account instead\.

**Topics**
+ [Use Group Policy to Change the Default Internet Explorer Home Page](#customize-fleets-change-ie-homepage-group-policy)
+ [Use the AppStream 2\.0 Template User Account to Change the Default Internet Explorer Home Page](#customize-fleets-change-ie-homepage-template-user)

### Use Group Policy to Change the Default Internet Explorer Home Page<a name="customize-fleets-change-ie-homepage-group-policy"></a>

In Active Directory environments, you use the Group Policy Management \(GPMC\) MMC\-snap\-in to set a default home page that users can't change\. If Active Directory is not in your environment, you can use Local Group Policy Editor to perform this task\. To set a home page that users can change, you must use the GPMC\. 

To use the GPMC, do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the GPMC\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with permissions to create GPOs\. Link GPOs to the appropriate organizational units \(OUs\)\.

**To change the default Internet Explorer home page by using a Group Policy administrative template**

You can use a Group Policy administrative template to set a default home page that users can't change\. For more information about administrative templates, see [Edit Administrative Template Policy Settings](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771479(v=ws.11)) in the Microsoft documentation\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. If you are not using Active Directory in your environment, open Local Group Policy Editor\. If you are using Active Directory, open the GPMC\. Locate the **Scripts \(Logon\\Logoff\) **policy setting: 
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

### Use the AppStream 2\.0 Template User Account to Change the Default Internet Explorer Home Page<a name="customize-fleets-change-ie-homepage-template-user"></a>

Follow these steps to use the Template User account to change the default Internet Explorer home page\. 

**To change the default Internet Explorer Home page by using the Template User account**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder on which to change the default Internet Explorer home page, verify that it is in the **Running** state, and choose **Connect**\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Template User**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, specify the credentials for a domain user account that does not have local administrator permissions on the image builder, then choose **Log in**\.

1. Open Internet Explorer and complete the necessary steps to change the default home page\.

1. In the upper right area of the image builder desktop, choose **Admin Commands**, **Switch User**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/admin-commands-switch-user.png)

1. This disconnects your current session and opens the login menu\. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, and log in as a domain user who has local administrator permissions on the image builder\.

1. On the image builder desktop, open Image Assistant\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

## User and Instance Metadata for AppStream 2\.0 Fleets<a name="customize-fleets-user-instance-metadata"></a>

AppStream 2\.0 fleet instances have user and instance metadata available through Windows environment variables\. You can use the following environment variables in your applications and scripts to modify your environment based on the fleet instance details\.


| Environment Variable | Context | Description | 
| --- | --- | --- | 
| AppStream\_Stack\_Name | User | The name of the stack that the streaming session started from\. | 
| AppStream\_User\_Access\_Mode | User | The access mode that the user is using to stream\. The values are custom, userpool, or saml\. | 
| AppStream\_Session\_Reservation\_DateTime | User | The date and time when the user's streaming session started\. | 
| AppStream\_UserName | User | The user name for the user\. | 
| AppStream\_Session\_ID | User | The session identifier for the user's streaming session\. | 
| APPSTREAM\_SESSION\_CONTEXT | Machine | The session context that was provided when the streaming URL was created\.  This environment variable is only available after the first application launch\. | 
| AppStream\_Image\_Arn | Machine | The ARN of the image that was used to create the streaming instance\. | 
| AppStream\_Instance\_Type | Machine | The instance type of the streaming instance\. For example, stream\.standard\.medium\. | 
| AppStream\_Resource\_Type | Machine | The type of AppStream 2\.0 resource\. The value is either fleet or imagebuilder\. | 
| AppStream\_Resource\_Name | Machine | The name of the fleet\. | 