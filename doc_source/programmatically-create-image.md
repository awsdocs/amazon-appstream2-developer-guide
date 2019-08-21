# Create Your AppStream 2\.0 Image Programmatically by Using the Image Assistant CLI Operations<a name="programmatically-create-image"></a>

You can create Amazon AppStream 2\.0 images by connecting to an image builder and using the Image Assistant graphical user interface \(GUI\) or command line interface \(CLI\) operations\. The Image Assistant CLI operations provide functionality that is similar to the Image Assistant GUI\. With these operations, you can programmatically do the following:
+ Manage the applications that are included in an image\.
+ Save, update, and reset default application settings\.
+ Enable or disable the AppStream 2\.0 dynamic application framework\.
+ Specify tags\.
+ Create an image\.

 You can use these operations to integrate AppStream 2\.0 image creation with your continuous integration or deployment software development process\.

To work with the Image Assistant CLI operations, use the command line shell of your choice on an image builder\. For example, you can use the Windows command prompt or PowerShell\.

**Note**  
The image builder must use a version of the AppStream 2\.0 agent that is released on or after July 26, 2019\. If you don't have an image builder, you must create one\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

**Topics**
+ [Creating Default Application and Windows Settings with the Image Assistant CLI operations](#create-default-app-windows-settings-image-assistant)
+ [Optimizing the Launch Performance of Your Applications with the Image Assistant CLI Operations](#optimize-app-launch-performance-image-assistant-cli)
+ [Process Overview for Programmatically Creating an AppStream 2\.0 Image](#process-overview-creating-image-programmatically-image-image-assistant-cli)
+ [Image Assistant CLI Operations for Creating and Managing Your AppStream 2\.0 Image](#cli-operations-managing-creating-image-image-assistant)

## Creating Default Application and Windows Settings with the Image Assistant CLI operations<a name="create-default-app-windows-settings-image-assistant"></a>

You can create default application and Windows settings so that your users can get started with their applications quickly\. When you create these settings, AppStream 2\.0 replaces the Windows default user profile with the profile that you configure\. The Windows default user profile is then used to create the initial settings for users in the fleet instance\. If you create these settings by using the Image Assistant CLI operations, your application installer, or the automation, should modify the Windows default user profile directly\.

To overwrite the Windows default user profile with that of another Windows user, you can also use the Image Assistant `update-default-profile` CLI operation\.

For more information about configuring default application and Windows settings, see *Creating Default Application and Windows Settings for Your AppStream 2\.0 Users* in [Default Application and Windows Settings and Application Launch Performance](customizing-appstream-images.md)\.

## Optimizing the Launch Performance of Your Applications with the Image Assistant CLI Operations<a name="optimize-app-launch-performance-image-assistant-cli"></a>

AppStream 2\.0 lets you optimize the launch performance of your applications for your users’ streaming sessions\. When you do so by using the Image Assistant CLI operations, you can specify the files to optimize for your application launch\. Adding files to the application optimization manifest reduces the time that it takes for the application to launch for the first time on a new fleet instance\. However, this also increases the time that it takes for the fleet instances to be made available to users\. The optimization manifest is a line\-delimited text file that is per application\. 

**Note**  
If you onboard application optimization manifests by using both the Image Assistant CLI operations and the Image Assistant GUI, the manifests are merged\.

Following is an example of an application optimization manifest file named C:\\path\\to\\application\-optimization\-manifest\.txt:

```
C:\Program Files (x86)\Notepad++\autoCompletion
C:\Program Files (x86)\Notepad++\localization
C:\Program Files (x86)\Notepad++\plugins
C:\Program Files (x86)\Notepad++\themes
C:\Program Files (x86)\Notepad++\updater
C:\Program Files (x86)\Notepad++\userDefineLangs
C:\Program Files (x86)\Notepad++\change.log
C:\Program Files (x86)\Notepad++\config.xml
C:\Program Files (x86)\Notepad++\contextMenu.xml
C:\Program Files (x86)\Notepad++\doLocalConf.xml
C:\Program Files (x86)\Notepad++\functionList.xml
C:\Program Files (x86)\Notepad++\langs.model.xml
C:\Program Files (x86)\Notepad++\license.txt
C:\Program Files (x86)\Notepad++\notepad++.exe
C:\Program Files (x86)\Notepad++\readme.txt
C:\Program Files (x86)\Notepad++\SciLexer.dll
C:\Program Files (x86)\Notepad++\shortcuts.xml
C:\Program Files (x86)\Notepad++\stylers.model.xml
```

For more information about optimizing the launch performance of your applications, see *Optimizing the Launch Performance of Your Applications* in [Default Application and Windows Settings and Application Launch Performance](customizing-appstream-images.md)\.

## Process Overview for Programmatically Creating an AppStream 2\.0 Image<a name="process-overview-creating-image-programmatically-image-image-assistant-cli"></a>

You can use the Image Assistant CLI operations with your application installation automation to create a fully programmatic AppStream 2\.0 image creation workflow\. After your application installation automation completes, but before the image is created, use the Image Assistant CLI operations to specify the following:
+ The executable files that your users can launch
+ The optimization manifests for your applications
+ Other AppStream 2\.0 image metadata

The following high\-level overview describes the process for programmatically creating an AppStream 2\.0 image\.

1. Use your application installation automation to install the required applications on your image builder\. This installation may include applications that your users will launch, any dependencies, and background applications\.

1. Determine the files and folders to optimize\.

1. If applicable, use the Image Assistant `add-application` CLI operation to specify the application metadata and optimization manifest for the AppStream 2\.0 image\.

1. To specify additional applications for the AppStream 2\.0 image, repeat steps 1 through 3 for each application as needed\.

1. If applicable, use the Image Assistant `update-default-profile` CLI operation to overwrite the default Windows profile and create default application and Windows settings for your users\.

1. Use the Image Assistant `create-image` CLI operation to create the image\.

## Image Assistant CLI Operations for Creating and Managing Your AppStream 2\.0 Image<a name="cli-operations-managing-creating-image-image-assistant"></a>

This section describes the Image Assistant CLI operations that you can use to create and manage your AppStream 2\.0 image\.

The executable file that includes the command line interface is located at: C:\\Program Files\\Amazon\\Photon\\ConsoleImageBuilder\\Image\-Assistant\.exe\. For your convenience, this executable file is included in the Windows PATH variable\. This lets you call the Image Assistant CLI operations without specifying the absolute path to the executable file\. To call these operations, type the image\-assistant\.exe command\.

### `help` operation<a name="help-operation-image-assistant-cli"></a>

Retrieves a list of all Image Assistant CLI operations\. For each operation in the list, a description and usage syntax is provided\. To display help for a specific operation, type the name of the operation and specify the **\-\-help** parameter\. For example:

```
add-application --help
```

**Synopsis**

```
help
```

**Output**

Prints to standard out the list of available operations with a description of their function\.

### `add-application` operation<a name="add-application-operation-image-assistant-cli"></a>

Adds the application to the application list for AppStream 2\.0 users\. Applications in this list are included in the application catalog\. The application catalog displays to users when they sign in to an AppStream 2\.0 streaming session\.

**Synopsis**

```
add-application
--name <value>
--absolute-app-path <value>
[--display-name <value>]
[--absolute-icon-path <value>]
[--working-directory <value>]
[--launch-parameters <""-escaped value>]
[--absolute-manifest-path <value>]
```

**Options**

**`--name` \(string\)**  
A unique name for the application\. The maximum length is 256 characters\. You can add up to 50 applications\. You cannot use whitespace characters\.

**`--absolute-app-path` \(string\)**  
The absolute path to the executable file, batch file, or script for the application\. The path must point to a valid file\.

**`--display-name` \(string\)**  
The name to display for the application in the application catalog\. If you don't specify a display name, AppStream 2\.0 creates a name that is derived from the executable file name\. The name is created without the file extension and with underscores in place of spaces\. The maximum length is 256 characters\.

**`--absolute-icon-path` \(string\)**  
The absolute path to the icon for the application\. The path must point to a valid icon file that is one of the following types: \.jpg, \.png, or \.bmp\. The maximum dimensions are: 256 px x 256 px\. If you don't specify a path, the default icon for the executable file is used, if available\. If a default icon is not available for the executable file, a default AppStream 2\.0 application icon is used\.

**`--working-directory` \(string\)**  
The initial working directory for the application when the application is launched\.

**`--optimization-manifest` \(string\)**  
The path to a new line\-delimited text file\. The file specifies the absolute paths of the files to optimize before the fleet instance is made available to a user for streaming\. The path must point to a valid text file\.

**Message output**


| Exit code | Message printed to standard out | Description | 
| --- | --- | --- | 
| 0 |  \{"status": 0, "message": "Success"\}  |  The application was added successfully\.  | 
| 1 |  \{"status": 1, "message": "Administrator privileges are required to perform this operation"\}  |  Administrator privileges are required to complete the operation\.  | 
| 1 |  \{"status": 1, "message": "Unable to add more than 50 apps to the catalog\."\}  |  The application could not be added because the maximum number of applications that can be added to the AppStream 2\.0 application catalog is 50\.  | 
| 1 |  \{"status": 1, "message": "Name is not unique"\}  |  An application with that name already exists in the AppStream 2\.0 application catalog\.  | 
| 1 |  \{"status": 1, "message": "File not found \(absolute\-app\-path\)"\}  |  The file that was specified for absolute\-app\-path could not be found\.  | 
| 1 |  \{"status": 1, "message": "Unsupported file extension"\}  |  The Absolute\-app\-path parameter only supports the following file types: \.exe and \.bat\.  | 
| 1 |  \{"status": 1, "message": "Directory not found \(working\-directory\)"  |  The directory that was specified for working\-directory could not be found\.  | 
| 1 |  \{"status": 1, "message": "Optimization\-manifest not found: <filename>"\}  |  The file that was specified for optimization\-manifest could not be found\.  | 
| 1 |  \{"status": 1, "message": "File not found: <filename>"\}  |  A file that was specified within the optimization manifest could not be found\.  | 
| 255 |  \{"status": 255, "message": <error message>\}  |  An unexpected error occurred\. Try the request again\. If the error persists, contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  | 

### `remove-application` operation<a name="remove-application-operation-image-assistant-cli"></a>

Removes an application from the application list for the AppStream 2\.0 image\. The application is not uninstalled or modified, but users will not be able to launch it from the AppStream 2\.0 application catalog\.

**Synopsis**

```
remove-application
--name <value>
```

**Options**

**`--name` \(string\)**  
The unique identifier of the application to remove\.

**Message output**


| Exit code | Message printed to standard out | Description | 
| --- | --- | --- | 
| 0 |  \{"status": 0, "message": "Success"\}  |  The application was removed successfully\.  | 
| 1 |  \{"status": 1, "message": "Administrator privileges are required to perform this operation"\}  |  Administrator privileges are required to complete the operation\.  | 
| 1 |  \{"status": 1, "message": "App not found"\}  |  The application that was specified could not be found in the AppStream 2\.0 application catalog\.  | 
| 255 |  \{"status": 255, "message": <error message>\}  |  An unexpected error occurred\. Try the request again\. If the error persists, contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  | 

### `list-applications` operation<a name="list-applications-operation-image-assistant-cli"></a>

Lists all of the applications that are specified in the application catalog\.

**Synopsis**

```
list-applications
```

**Message output**


| Exit code | Message printed to standard out | Description | 
| --- | --- | --- | 
| 0 |  \{"status": 0, "message": "Success", "applications": \[ \{\.\.app1\.\. \}, \{ \.\.app2\.\. \}\]\}  |  List of applications in the AppStream 2\.0 application catalog\.  | 
| 255 |  \{"status": 255, "message": <error message>\}  |  An unexpected error occurred\. Try the request again\. If the error persists, contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  | 

### `update-default-profile` operation<a name="update-default-profile-image-assistant-cli"></a>

Copies the specified Windows user’s profile to the Windows default user profile\. New users who stream inherit the settings stored in the specified profile\.

**Synopsis**

```
update-default-profile
[--profile <value>]
```

**Options**

**`--profile` \(string\)**  
The name of the user whose Windows profile will be copied to the Windows default user profile\. Use the following format for the name:  
"<domain>\\<username>"  
If your image builder isn’t joined to a Microsoft Active Directory domain, enter a period "\." for the domain\. If you don’t specify a user, the AppStream 2\.0 Template User account is used\.

**Message output**


| Exit code | Message printed to standard out | Description | 
| --- | --- | --- | 
| 0 |  \{"status": 0, "message": "Success"\}  |  The user settings were successfully copied to the default Windows profile\.  | 
| 1 |  \{"status": 1, "message": "Administrator privileges are required to perform this operation"\}  |  Administrator privileges are required to complete the operation\.  | 
| 1 |  \{"status": 1, "message": "Unable to copy file or folder: <path>\. <reason>"\}  |  The user settings could not be copied because a file or folder was unavailable\.  | 
| 1 |  \{"status": 1, "message": "Cannot copy a domain user when not joined to a domain""\}  |  A Microsoft Active Directory domain user was specified, but the image builder is not joined to an Active Directory domain\.  | 
| 255 |  \{"status": 255, "message": <error message>\}  |  An unexpected error occurred\. Try the request again\. If the error persists, contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  | 

### `reset-user-profile` operation<a name="reset-user-profile-image-assistant-cli"></a>

Deletes the Windows user profile for the specified user\.

**Synopsis**

```
reset-user-profile
[--profile <value>]
```

**Options**

**`--profile` \(string\)**  
The name of the Windows user whose Windows profile will be deleted\. Use the following format for the name:  
"<domain>\\<username>"  
If your image builder isn’t joined to a Microsoft Active Directory domain, enter a period "\." for the domain\.

**Message output**


| Exit code | Message printed to standard out | Description | 
| --- | --- | --- | 
| 0 |  \{"status": 0, "message": "Success"\}  |  The specified user settings were deleted successfully\.  | 
| 1 |  \{"status": 1, "message": "Administrator privileges are required to perform this operation"\}  |  Administrator privileges are required to complete the operation\.  | 
| 1 |  \{"status": 1, "message": "Unable to copy file or folder: <path>\. <reason>"\}  |  The user settings could not be reset because a file or folder was unavailable\.  | 
| 1 |  \{"status": 1, "message": "Cannot copy a domain user when not joined to a domain""\}  |  A Microsoft Active Directory domain user was specified, but the image builder is not joined to an Active Directory domain\.  | 
| 255 |  \{"status": 255, "message": <error message>\}  |  An unexpected error occurred\. Try the request again\. If the error persists, contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  | 

### `create-image` operation<a name="create-image-operation-image-assistant-cli"></a>

Starts the image creation workflow, resulting in an AppStream 2\.0 image that can be used for AppStream 2\.0 fleets\.

**Synopsis**

```
create-image
--name <value>
[--description <value>]
[--display-name <value>]
[--enable-dynamic-app-catalog] | [--no-enable-dynamic-app-catalog]
[--use-latest-agent-version] | [--no-use-latest-agent-version]            
[--tags <value>]
[--dry-run]
```

**Options**

**`--name` \(string\)**  
The name for the AppStream 2\.0 image\. The name must be unique within the AWS account and AWS Region\. The maximum length is 100 characters\. Allowed characters are:  
a\-z, A\-Z, 0\-9, and underscores \(\_\)  
The image name cannot start with any of the following prefixes: 'aws', 'appstream', and 'amazon’\. These prefixes are reserved for AWS use\.

**`--description` \(string\)**  
The description to display for the image\. The maximum length is 256 characters\.

**`--display-name` \(string\)**  
The name to display for the image\. The maximum length is 256 characters\.

**`--enable-dynamic-app-catalog` \| `--no-enable-dynamic-app-catalog`**  
Enables or disables support for the AppStream 2\.0 dynamic application framework\. If you don't specify either parameter, support for the dynamic application framework is not enabled\.  
The dynamic application framework provides operations within an AppStream 2\.0 streaming instance that you can use to build a dynamic app provider\. Dynamic app providers can use these operations to modify the catalog of applications that your users can access in real time\. For more information, see [Use the AppStream 2\.0 Dynamic Application Framework to Build a Dynamic App Provider](build-dynamic-app-provider.md)\.

**`--use-latest-agent-version` \| `--no-use-latest-agent-version`**  
Specifies whether to pin the image to the version of the AppStream 2\.0 agent that is currently installed, or to always use the latest agent version\. If you don't specify either parameter, the image is pinned to the version of the AppStream 2\.0 agent that is currently installed\. For more information, see [Manage AppStream 2\.0 Agent Versions](base-images-agent.md)\.

**`--tags` \(string\)**  
The tags to associate with the image\. A tag is a key\-value pair\. Use the following format:  
\-\-tags "mykey" "myval" "mykey2" "myval2"  
For more information about tags, see [Tagging Your Amazon AppStream 2\.0 Resources](tagging-basic.md)\.

**`--dry-run` \(string\)**  
Performs validation without creating the image\. Use this command to identify whether your image has any issues before you create it\.

**Message output**


| Exit code | Message printed to standard out | Description | 
| --- | --- | --- | 
| 0 |  \{"status": 0, "message": "Success"\}  |  The workflow to create the image was initiated successfully\.  | 
| 1 |  \{"status": 1, "message": "Administrator privileges are required to perform this operation"\}  |  Administrator privileges are required to complete the operation\.  | 
| 1 |  \{"status": 1, "message": "An image with the given name already exists"\}  |  An image with the specified name already exists in the AWS account\.  | 
| 1 |  \{"status": 1, "message": "Invalid value \(tags\)"\}  |  The specified tags are not valid\.  | 
| 255 |  \{"status": 255, "message": <error message>\}  |  An unexpected error occurred\. Try the request again\. If the error persists, contact AWS Support for assistance\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  | 