# AppStream 2\.0 Active Directory Administration<a name="active-directory-admin"></a>

When setting up and using Active Directory with AppStream 2\.0, refer to the following administrator tasks\.


+ [Granting Permissions to Create and Manage Active Directory Computer Objects](#active-directory-permissions)
+ [Finding the Organizational Unit Distinguished Name](#active-directory-oudn)
+ [Providing Local Administrator Permissions for Image Builders](#active-directory-image-builder-local-admin)
+ [Updating the Service Account Used for Joining the Domain](#active-directory-service-acct)
+ [Locking the Streaming Session When the User is Idle](#active-directory-session-lock)
+ [Editing the Directory Configuration](#active-directory-config-edit)
+ [Deleting a Directory Configuration](#active-directory-config-delete)
+ [Configuring AppStream 2\.0 to Use Domain Trusts](#active-directory-domain-trusts)
+ [Managing AppStream 2\.0 Computer Objects in the Active Directory](#active-directory-identify-objects)

## Granting Permissions to Create and Manage Active Directory Computer Objects<a name="active-directory-permissions"></a>

To allow AppStream 2\.0 to perform Active Directory computer object operations, you need an account with the right permissions\. As a best practice, you should use an account that has only the minimum privileges necessary\. The minimum Active Directory organizational unit \(OU\) permissions are as follows:

+ Create Computer Object

+ Change Password

+ Reset Password

+ Write Description

**Prerequisites**

Before setting up permissions, you must complete the following tasks:

+ Get access to a computer or EC2 instance that is joined to your domain\.

+ Install the Active Directory User and Computers MMC snap\-in\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.

+ Log in as a domain user with appropriate permissions to modify the OU security settings\.

+ Create or identify the user account, service account, or group for which to delegate permissions\.

**To set up minimum permissions**

1. Launch **Active Directory Users and Computers** in your domain or on your domain controller\.

1. In the navigation tree on the left, select the first OU on which to provide domain join privileges, open the context menu \(right\-click\), and choose **Delegate Control**\.

1. On the **Delegation of Control Wizard** page, choose **Next**, **Add**\.

1. For **Select Users, Computers, or Groups**, select the pre\-created user account, service account, or group, and choose **OK**\.

1. On the **Tasks to Delegate** page, choose **Create a custom task to delegate**, **Next**\.

1. Choose **Only the following objects in the folder**, **Computer objects**\.

1. Choose **Create selected objects in this folder**, **Next**\.

1. For **Permissions**, choose **Read**, **Write**, **Change Password**, **Reset Password**, **Next**\.

1. On the **Completing the Delegation of Control Wizard** page, verify the information and choose **Finish**\.

1. Repeat steps 2\-10 for any additional OUs that require these permissions\.

If you delegated permissions to a group, create a user or service account with a strong password and add that account to the group\. This account will then have sufficient privileges to connect your streaming instances to the directory\. Use this account when creating your AppStream 2\.0 directory configuration\.

## Finding the Organizational Unit Distinguished Name<a name="active-directory-oudn"></a>

When you register your Active Directory with AppStream 2\.0, you must provide an organizational unit \(OU\) distinguished name\. Create an OU for this purpose\. The default Computers container is not an OU and cannot be used by AppStream 2\.0\. The following procedure shows how to obtain this name\.

**Note**  
The distinguished name must start with **OU=** or it cannot be used for computer objects\.

**Prerequisites**

+ Get access to a computer or EC2 instance that is joined to your domain\.

+ Install the Active Directory User and Computers MMC snap\-in\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.

+ Log in as a domain user with appropriate permissions to read the OU security properties\.

**To find the distinguished name of an OU**

1. Launch **Active Directory Users and Computers** in your domain or on your domain controller\.

1. Under **View**, ensure that **Advanced Features** is enabled\.

1. In the navigation tree on the left, select the first OU to use for AppStream 2\.0 streaming instance computer objects, open the context menu \(right\-click\), and choose **Properties**\.

1. Choose **Attribute Editor**\.

1. Under **Attributes**, for **distinguishedName**, choose **View**\.

1. For **Value**, select the distinguished name, open the context menu \(right\-click\), and choose **Copy**\.

## Providing Local Administrator Permissions for Image Builders<a name="active-directory-image-builder-local-admin"></a>

By default, Active Directory domain users do not have local administrator permissions on image builder instances\. You can provide these permissions using Group Policy preferences in your directory, or manually using the local administrator account\. This allows a domain user to install applications and create images in an AppStream 2\.0 image builder\.


+ [Using Group Policy Permissions](#group-policy)
+ [Using Local Administrator](#manual-procedure)

### Using Group Policy Permissions<a name="group-policy"></a>

Group Policy can be used to grant local administrator permissions to Active Directory users or groups and automatically to all computer objects in the specified OU\. The Active Directory users or groups to which to grant local administrator permissions must already exist\.

**Prerequisites**

+ Get access to a computer or EC2 instance that is joined to your domain\.

+ Install the Group Policy Management MMC snap\-in\. For more information, see [Installing or Removing Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/en-us/library/ee449483.aspx) in the Microsoft documentation\.

+ Log in as a domain user with appropriate permissions to create Group Policy Objects \(GPO\) and link them to the appropriate OUs\.

**To provide permissions using Group Policy**

1. Launch Group Policy Management in your directory or on your domain controller\.

1. In the navigation tree on the left, select the organizational unit \(OU\) in which to create the GPO, open the context \(right\-click\) menu, and choose **Create a GPO in this domain**, **Link it here…**\.

1. For **Name**, provide a descriptive name for this GPO\.

1. Select the newly created GPO, open the context \(right\-click\) menu , and choose **Edit**\.

1. In the left navigation tree, choose **Computer Configuration**, **Preferences**, **Windows Settings**, **Control Panel Settings**, and **Local Users and Groups**\.

1. Select **Local Users and Groups** selected, open the context \(right\-click\) menu , and choose **New**, **Local Group**\.

1. For **Action**, choose **Update**\.

1. For **Group name**, choose **Administrators \(built\-in\)**\.

1. Under **Members**, choose **Add…** and specify the Active Directory user accounts or groups to which to assign local administrator rights on the streaming instance\. For **Action**, choose **Add to this group**, and choose **OK**\.

1. To apply this GPO to other OUs, select the additional OU, open the context \(right\-click\) menu and choose **Link an Existing GPO**\.

1. Using the name specified in step 3, scroll to find the created GPO, and choose **OK**\. The GPO now shows up in the navigation tree on the left within the OU\.

1. Repeat steps 10\-11 for additional OUs that should have this policy\.

1. Choose **OK** to close the New Local Group Properties window, Choose **OK** again to close the Group Policy Management Editor window\.

Any running image builders or fleets must be stopped then started to apply the new policy\. Streaming image builders and fleets created in the OU in which the specified GPO is linked automatically provide local administrator rights to the specified users or groups\.

### Using Local Administrator<a name="manual-procedure"></a>

Use the pre\-created local administrator account to manually add Active Directory users or groups to the local administrator group to grant administrator rights\. New image builders created from this image builder maintain the permissions\. 

The Active Directory users or groups to which to grant local administrator rights must already exist\.

**To provide permissions using local admin rights**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Select the image builder, and choose **Connect**\. The image builder must be running and domain\-joined\. For more information, see [Tutorial: Setting Up the Active Directory](active-directory-directory-setup.md)\.

1. Log in to the administrator account\.

1. Choose **Start**, **Administrative Tools** and launch the **Computer Management** administrative tool\.

1. In the left navigation pane, choose **Local Users and Groups** and open the **Groups** folder\.

1. Open the **Administrators** group and choose **Add\.\.\.**\.

1. Select all Active Directory users or groups to which to assign local administrator rights and choose **OK**\. Choose **OK** again to close the Administrator Properties window\.

1. Close the Computer Management administrative tool\.

1. To log in as a Active Directory user and test local administrator access rights, choose **Admin Commands**, **Switch user**\.

## Updating the Service Account Used for Joining the Domain<a name="active-directory-service-acct"></a>

To update the service account that AppStream 2\.0 uses for joining the domain, we recommend using two service accounts for joining image builders and fleets to your Active Directory\. Using two separate service accounts ensures that you have no disruption in service when a service account needs to be updated, for example when a password expires\. 

**To update a service account**

1. Create an Active Directory group and delegate the correct permissions to the group\.

1. Add your service accounts to the new Active Directory group\.

1. When needed, edit your AppStream 2\.0 directory configuration to provide the other service account username and password\.

After you've set up the Active Directory group with the new service account, any new streaming instance operations use the new service account, while in\-process streaming instance operations continue using the old account without interruption\. 

The service account overlap time while the in\-process streaming instance operations complete is very short, no more than a day\. The overlap time is needed because you shouldn't delete or change the password for the old service account during the overlap period, or existing operations can fail\.

## Locking the Streaming Session When the User is Idle<a name="active-directory-session-lock"></a>

AppStream 2\.0 relies on Microsoft Active Directory Group Policies to lock the streaming session when your user goes idle\. 

**To automatically lock the streaming instance when your user is idle**

1. Follow the instructions at [Customizing the Desktop](https://technet.microsoft.com/en-us/library/cc938799.aspx) in the Microsoft documentation\.

1. For **Enable screen saver**, choose **Enabled**\.

1. For **Force specific screen saver**, choose **Enabled** and type **scrnsave\.scr**\. This setting shows a black screen when the screen saver comes on\.

1. For **Password protect the screen saver**, choose **Enabled**\.

1. For **Screen saver timeout**, enter the appropriate amount of time, in seconds\. This is the duration of user inactivity before the screen saver applies\. For example, to set an idle duration of 10 minutes idle, specify a value of 600 seconds\.

Additionally, set the following policy to **Disabled**: **User Configuration > Administrative Templates > System > Ctrl\+Alt\+Del Options > Remove Lock Computer**\.

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

Changes to the service account username and password do not impact in\-process streaming instance operations\. New streaming instance operations use the updated credentials\. For more information, see [Updating the Service Account Used for Joining the Domain](#active-directory-service-acct)\.

## Deleting a Directory Configuration<a name="active-directory-config-delete"></a>

You can delete a AppStream 2\.0 directory configuration that is no longer needed\. Directory configurations that are associated with any image builders or fleets cannot be deleted\.

**To delete a directory configuration**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Directory Configs** and select the directory configuration to delete\.

1. Choose **Actions**, **Delete**\.

1. Verify the name in the pop\-up message, and choose **Delete**\.

1. Choose **Update Directory Config**\.

## Configuring AppStream 2\.0 to Use Domain Trusts<a name="active-directory-domain-trusts"></a>

AppStream 2\.0 supports Active Directory domain environments where network resources such as file servers, applications, and computer objects reside in one domain, and the user objects reside in another\. The domain service account used for computer object operations does not need to be in the same domain as the AppStream 2\.0 computer objects\. 

When creating the directory configuration, specify a service account that has the appropriate permissions in the server Active Directory domain to manage computer objects\.

Your end user Active Directory accounts must have the "Allowed to Authenticate" permissions for the following:

+ AppStream 2\.0 computer objects

+ Domain controllers for the domain

For more information, see [Granting Permissions to Create and Manage Active Directory Computer Objects](#active-directory-permissions)\.

## Managing AppStream 2\.0 Computer Objects in the Active Directory<a name="active-directory-identify-objects"></a>

AppStream 2\.0 does not delete computer objects from your Active Directory\. These computer objects can be easily identified in your directory\. Each computer object in the directory is created with the Description attribute specifying a fleet or an image builder instance and the name\. 


**Computer Object Description Examples**  

| Type | Name | Description Attribute | 
| --- | --- | --- | 
|  Fleet  |  ExampleFleet  |  `AppStream 2.0 - fleet:ExampleFleet`  | 
|  Image builder  |  ExampleImageBuilder  |  `AppStream 2.0 - image-builder:ExampleImageBuilder`  | 

You can identify and delete inactive computer objects created by AppStream 2\.0 with the following `dsquery` and `dsrm` commands\. For more information, see [Dsquery](https://technet.microsoft.com/en-us/library/cc732952.aspx) and [Dsrm](https://technet.microsoft.com/en-us/library/cc731865.aspx) in the Microsoft documentation\.

The `dsquery` command is used to identify inactive computer objects over a certain period of time, and uses the following format\. The `dsquery` command should also be run with the parameter `-desc "AppStream 2.0*"` to show only AppStream 2\.0 objects\. 

```
dsquery computer "OU-distinguished-name" -desc "AppStream 2.0*" -inactive number-of-weeks-since-last-login
```

+ `OU-distinguished-name` is the distinguished name of the organizational unit\. For more information, see [Finding the Organizational Unit Distinguished Name](#active-directory-oudn)\. If you don't provide the *OU\-distinguished\-name* parameter, the command searches the entire directory\. 

+ `number-of-weeks-since-last-log-in` is the desired value based on how you'd like to define what's "inactive"\. 

For example, the following command displays all computer objects in the `OU=ExampleOU,DC=EXAMPLECO,DC=COM` organizational unit that have not logged in within the past two weeks\.

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

You can chain these commands together using the pipe \(`|`\) operator\. For example, to delete all AppStream 2\.0 computer objects, prompting for confirmation for each, use the following format\. Add the `-noprompt` parameter to `dsrm` to disable confirmation\.

```
dsquery computer OU-distinguished-name -desc "AppStream 2.0*" –inactive number-of-weeks-since-last-log-in | dsrm
```