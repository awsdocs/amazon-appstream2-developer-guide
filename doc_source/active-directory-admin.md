# AppStream 2\.0 Active Directory Administration<a name="active-directory-admin"></a>

Setting up and using Active Directory with AppStream 2\.0 involves the following administrative tasks\.

**Topics**
+ [Granting Permissions to Create and Manage Active Directory Computer Objects](#active-directory-permissions)
+ [Finding the Organizational Unit Distinguished Name](#active-directory-oudn)
+ [Granting Local Administrator Rights on Image Builders](#active-directory-image-builder-local-admin)
+ [Updating the Service Account Used for Joining the Domain](#active-directory-service-acct)
+ [Locking the Streaming Session When the User is Idle](#active-directory-session-lock)
+ [Editing the Directory Configuration](#active-directory-config-edit)
+ [Deleting a Directory Configuration](#active-directory-config-delete)
+ [Configuring AppStream 2\.0 to Use Domain Trusts](#active-directory-domain-trusts)
+ [Managing AppStream 2\.0 Computer Objects in Active Directory](#active-directory-identify-objects)

## Granting Permissions to Create and Manage Active Directory Computer Objects<a name="active-directory-permissions"></a>

To allow AppStream 2\.0 to perform Active Directory computer object operations, you need an account with sufficient permissions\. As a best practice, use an account that has only the minimum privileges necessary\. The minimum Active Directory organizational unit \(OU\) permissions are as follows:
+ Create Computer Object
+ Change Password
+ Reset Password
+ Write Description

Before setting up permissions, you'll need to do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the Active Directory User and Computers MMC snap\-in\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with appropriate permissions to modify the OU security settings\.
+ Create or identify the user account, service account, or group for which to delegate permissions\.

**To set up minimum permissions**

1. Open **Active Directory Users and Computers** in your domain or on your domain controller\.

1. In the left navigation pane, select the first OU on which to provide domain join privileges, open the context \(right\-click\) menu , and then choose **Delegate Control**\.

1. On the **Delegation of Control Wizard** page, choose **Next**, **Add**\.

1. For **Select Users, Computers, or Groups**, select the pre\-created user account, service account, or group, and then choose **OK**\.

1. On the **Tasks to Delegate** page, choose **Create a custom task to delegate**, and then choose **Next**\.

1. Choose **Only the following objects in the folder**, **Computer objects**\.

1. Choose **Create selected objects in this folder**, **Next**\.

1. For **Permissions**, choose **Read**, **Write**, **Change Password**, **Reset Password**, **Next**\.

1. On the **Completing the Delegation of Control Wizard** page, verify the information and choose **Finish**\.

1. Repeat steps 2\-9 for any additional OUs that require these permissions\.

If you delegated permissions to a group, create a user or service account with a strong password and add that account to the group\. This account will then have sufficient privileges to connect your streaming instances to the directory\. Use this account when creating your AppStream 2\.0 directory configuration\.

## Finding the Organizational Unit Distinguished Name<a name="active-directory-oudn"></a>

When you register your Active Directory domain with AppStream 2\.0, you must provide an organizational unit \(OU\) distinguished name\. Create an OU for this purpose\. The default Computers container is not an OU and cannot be used by AppStream 2\.0\. The following procedure shows how to obtain this name\.

**Note**  
The distinguished name must start with **OU=** or it cannot be used for computer objects\.

Before you complete this procedure, you'll need to do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the Active Directory User and Computers MMC snap\-in\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with appropriate permissions to read the OU security properties\.

**To find the distinguished name of an OU**

1. Open **Active Directory Users and Computers** in your domain or on your domain controller\.

1. Under **View**, ensure that **Advanced Features** is enabled\.

1. In the left navigation pane, select the first OU to use for AppStream 2\.0 streaming instance computer objects, open the context \(right\-click\) menu, and then choose **Properties**\.

1. Choose **Attribute Editor**\.

1. Under **Attributes**, for **distinguishedName**, choose **View**\.

1. For **Value**, select the distinguished name, open the context menu, and then choose **Copy**\.

## Granting Local Administrator Rights on Image Builders<a name="active-directory-image-builder-local-admin"></a>

By default, Active Directory domain users do not have local administrator rights on image builder instances\. You can grant these rights by using Group Policy preferences in your directory, or manually, by using the local administrator account on an image builder\. Granting local administrator rights to a domain user allows that user to install applications on and create images in an AppStream 2\.0 image builder\.

**Topics**
+ [Using Group Policy preferences](#group-policy)
+ [Using the local Administrators group on the image builder](#manual-procedure)

### Using Group Policy preferences<a name="group-policy"></a>

You can use Group Policy preferences to grant local administrator rights to Active Directory users or groups and to all computer objects in the specified OU\. The Active Directory users or groups to which you want to grant local administrator permissions must already exist\. To use Group Policy preferences, you'll need to do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the Group Policy Management Console \(GPMC\) MMC snap\-in\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with permissions to create Group Policy objects \(GPOs\)\. Link GPOs to the appropriate OUs\.

**To use Group Policy preferences to grant local administrator permissions**

1. In your directory or on a domain controller, open the command prompt as an administrator, type `gpmc.msc`, and then press ENTER\.

1. In the left console tree, select the OU where you will create a new GPO or use an existing GPO, and then do either of the following: 
   + Create a new GPO by opening the context \(right\-click\) menu and choosing **Create a GPO in this domain, Link it here**\. For **Name**, provide a descriptive name for this GPO\.
   + Select an existing GPO\.

1. Open the context menu for the GPO, and choose **Edit**\.

1. In the console tree, choose **Computer Configuration**, **Preferences**, **Windows Settings**, **Control Panel Settings**, and **Local Users and Groups**\.

1. Select **Local Users and Groups** selected, open the context menu , and choose **New**, **Local Group**\.

1. For **Action**, choose **Update**\.

1. For **Group name**, choose **Administrators \(built\-in\)**\.

1. Under **Members**, choose **Add…** and specify the Active Directory user accounts or groups to which to assign local administrator rights on the streaming instance\. For **Action**, choose **Add to this group**, and choose **OK**\.

1. To apply this GPO to other OUs, select the additional OU, open the context menu and choose **Link an Existing GPO**\.

1. Using the new or existing GPO name that you specified in step 2, scroll to find the GPO, and then choose **OK**\. 

1. Repeat steps 9 and 10 for additional OUs that should have this preference\.

1. Choose **OK** to close the **New Local Group Properties** dialog box\.

1. Choose **OK** again to close the GPMC\.

To apply the new preference to the GPO, you must stop and restart any running image builders or fleets\. The Active Directory users and groups that you specified in step 8 are automatically granted local administrator rights on the image builders and fleets in the OU to which the GPO is linked\.

### Using the local Administrators group on the image builder<a name="manual-procedure"></a>

To grant Active Directory users or groups local administrator rights on your image builder, you can manually add these users or groups to the local Administrators group on the image builder\. Image builders that are created from images with these rights maintain the same rights\. 

The Active Directory users or groups to which to grant local administrator rights must already exist\.

**To add Active Directory users or groups to the local Administrators group on the image builder**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Connect to the image builder in Administrator mode\. The image builder must be running and domain\-joined\. For more information, see [Tutorial: Setting Up Active Directory](active-directory-directory-setup.md)\.

1. Choose **Start**, **Administrative Tools**, and then double\-click **Computer Management**\.

1. In the left navigation pane, choose **Local Users and Groups** and open the **Groups** folder\.

1. Open the **Administrators** group and choose **Add\.\.\.**\.

1. Select all Active Directory users or groups to which to assign local administrator rights and choose **OK**\. Choose **OK** again to close the **Administrator Properties** dialog box\.

1. Close Computer Management\.

1. To log in as an Active Directory user and test whether that user has local administrator rights on the image builder, choose **Admin Commands**, **Switch user**, and then enter the credentials of the relevant user\.

## Updating the Service Account Used for Joining the Domain<a name="active-directory-service-acct"></a>

To update the service account that AppStream 2\.0 uses for joining the domain, we recommend using two separate service accounts for joining image builders and fleets to your Active Directory domain\. Using two separate service accounts ensures that there is no disruption in service when a service account needs to be updated \(for example, when a password expires\)\. 

**To update a service account**

1. Create an Active Directory group and delegate the correct permissions to the group\.

1. Add your service accounts to the new Active Directory group\.

1. When needed, edit your AppStream 2\.0 Directory Config object by entering the user name and password for the new service account\.

After you've set up the Active Directory group with the new service account, any new streaming instance operations will use the new service account, while in\-process streaming instance operations continue to use the old account without interruption\. 

The service account overlap time while the in\-process streaming instance operations complete is very short, no more than a day\. The overlap time is needed because you shouldn't delete or change the password for the old service account during the overlap period, or existing operations can fail\.

## Locking the Streaming Session When the User is Idle<a name="active-directory-session-lock"></a>

AppStream 2\.0 relies on a setting that you configure in the GPMC to lock the streaming session after your user is idle for specified amount of time\. To use the GPMC, you'll need to do the following first:
+ Obtain access to a computer or an EC2 instance that is joined to your domain\.
+ Install the GPMC\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.
+ Log in as a domain user with permissions to create GPOs\. Link GPOs to the appropriate OUs\.

**To automatically lock the streaming instance when your user is idle**

1. In your directory or on a domain controller, open the command prompt as an administrator, type `gpmc.msc`, and then press ENTER\.

1. In the left console tree, select the OU where you will create a new GPO or use an existing GPO, and then do either of the following: 
   + Create a new GPO by opening the context \(right\-click\) menu and choosing **Create a GPO in this domain, Link it here**\. For **Name**, provide a descriptive name for this GPO\.
   + Select an existing GPO\.

1. Open the context menu for the GPO, and choose **Edit**\. 

1. Under **User Configuration**, expand **Policies**, **Administrative Templates**, **Control Panel**, and then choose **Personalization**\. 

1. Double\-click **Enable screen saver**\.

1. In the **Enable screen saver** policy setting, choose **Enabled**\.

1. Choose **Apply**, and then choose **OK**\.

1. Double\-click **Force specific screen saver**\. 

1. In the **Force specific screen saver** policy setting, choose **Enabled**\.

1. Under **Screen saver executable name**, enter **scrnsave\.scr**\. When this setting is enabled, the system displays a black screen saver on the user's desktop\.

1. Choose **Apply**, and then choose **OK**\.

1. Double\-click **Password protect the screen saver**\.

1. In the **Password protect the screen saver** policy setting, choose **Enabled**\.

1. Choose **Apply**, and then choose **OK**\.

1. Double\-click **Screen saver timeout**\.

1. In the **Screen saver timeout** policy setting, choose **Enabled**\.

1. For **Seconds**, specify the length of time that users must be idle before the screen saver is applied\. To set the idle time to 10 minutes, specify 600 seconds\.

1. Choose **Apply**, and then choose **OK**\.

1. In the console tree, under **User Configuration**, expand **Policies**, **Administrative Templates**, **System**, and then choose **Ctrl\+Alt\+Del Options**\. 

1. Double\-click **Remove Lock Computer**\.

1. In the **Remove Lock Computer** policy setting, choose **Disabled**\.

1. Choose **Apply**, and then choose **OK**\.

## Editing the Directory Configuration<a name="active-directory-config-edit"></a>

After a AppStream 2\.0 directory configuration has been created, you can edit it to add, remove, or modify organizational units, update the service account username, or update the service account password\. 

**To update a directory configuration**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Directory Configs** and select the directory configuration to edit\.

1. Choose **Actions**, **Edit**\.

1. Update the fields to be changed\. To add additional OUs, select the plus sign \(**\+**\) next to the topmost OU field\. To remove an OU field, select the **x** next to the field\.
**Note**  
At least one OU is required\. OUs that are currently in use cannot be removed\.

1. To save changes, choose **Update Directory Config**\.

1. The information in the **Details** tab should now update to reflect the changes\.

Changes to the service account user name and password do not impact in\-process streaming instance operations\. New streaming instance operations use the updated credentials\. For more information, see [Updating the Service Account Used for Joining the Domain](#active-directory-service-acct)\.

## Deleting a Directory Configuration<a name="active-directory-config-delete"></a>

You can delete an AppStream 2\.0 directory configuration that is no longer needed\. Directory configurations that are associated with any image builders or fleets cannot be deleted\.

**To delete a directory configuration**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Directory Configs** and select the directory configuration to delete\.

1. Choose **Actions**, **Delete**\.

1. Verify the name in the pop\-up message, and choose **Delete**\.

1. Choose **Update Directory Config**\.

## Configuring AppStream 2\.0 to Use Domain Trusts<a name="active-directory-domain-trusts"></a>

AppStream 2\.0 supports Active Directory domain environments where network resources such as file servers, applications, and computer objects reside in one domain, and the user objects reside in another\. The domain service account used for computer object operations does not need to be in the same domain as the AppStream 2\.0 computer objects\. 

When creating the directory configuration, specify a service account that has the appropriate permissions to manage computer objects in the Active Directory domain where the file servers, applications, computer objects and other network resources reside\.

Your end user Active Directory accounts must have the "Allowed to Authenticate" permissions for the following:
+ AppStream 2\.0 computer objects
+ Domain controllers for the domain

For more information, see [Granting Permissions to Create and Manage Active Directory Computer Objects](#active-directory-permissions)\.

## Managing AppStream 2\.0 Computer Objects in Active Directory<a name="active-directory-identify-objects"></a>

AppStream 2\.0 does not delete computer objects from Active Directory\. These computer objects can be easily identified in your directory\. Each computer object in the directory is created with the `Description` attribute, which specifies a fleet or an image builder instance and the name\. 


**Computer Object Description Examples**  

| Type | Name | Description Attribute | 
| --- | --- | --- | 
|  Fleet  |  ExampleFleet  |  `AppStream 2.0 - fleet:ExampleFleet`  | 
|  Image builder  |  ExampleImageBuilder  |  `AppStream 2.0 - image-builder:ExampleImageBuilder`  | 

You can identify and delete inactive computer objects created by AppStream 2\.0 by using the following `dsquery computer` and `dsrm` commands\. For more information, see [Dsquery computer](https://technet.microsoft.com/en-us/library/cc730720.aspx) and [Dsrm](https://technet.microsoft.com/en-us/library/cc731865.aspx) in the Microsoft documentation\.

The `dsquery` command identifies inactive computer objects over a certain period of time and uses the following format\. The `dsquery` command should also be run with the parameter `-desc "AppStream 2.0*"` to display only AppStream 2\.0 objects\. 

```
dsquery computer "OU-distinguished-name" -desc "AppStream 2.0*" -inactive number-of-weeks-since-last-login
```
+ `OU-distinguished-name` is the distinguished name of the organizational unit\. For more information, see [Finding the Organizational Unit Distinguished Name](#active-directory-oudn)\. If you don't provide the *OU\-distinguished\-name* parameter, the command searches the entire directory\. 
+ `number-of-weeks-since-last-log-in` is the desired value based on how you want to define inactivity\. 

For example, the following command displays all computer objects in the `OU=ExampleOU,DC=EXAMPLECO,DC=COM` organizational unit that have not been logged into within the past two weeks\.

```
dsquery computer OU=ExampleOU,DC=EXAMPLECO,DC=COM -desc "AppStream 2.0*" -inactive 2
```

If any matches are found, the result is one or more object names\. The `dsrm` command deletes the specified object and uses the following format:

```
dsrm objectname
```

Where `objectname` is the full object name from the output of the `dsquery` command\. For example, if the `dsquery` command above results in a computer object named "ExampleComputer", the `dsrm` command to delete it would be as follows:

```
dsrm "CN=ExampleComputer,OU=ExampleOU,DC=EXAMPLECO,DC=COM"
```

You can chain these commands together by using the pipe \(`|`\) operator\. For example, to delete all AppStream 2\.0 computer objects, prompting for confirmation for each, use the following format\. Add the `-noprompt` parameter to `dsrm` to disable confirmation\.

```
dsquery computer OU-distinguished-name -desc "AppStream 2.0*" –inactive number-of-weeks-since-last-log-in | dsrm
```