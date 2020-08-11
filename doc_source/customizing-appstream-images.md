# Default Application and Windows Settings and Application Launch Performance<a name="customizing-appstream-images"></a>

 You can create default application and Windows settings to enable your users to get started with their applications quickly, so that they won't need to create or configure the settings themselves\.

AppStream 2\.0 optimizes the launch performance of your applications for your users' streaming sessions\. To ensure that all of the required files are included in this process, you may need to manually add certain files and folders to the optimization manifest\.

**Topics**
+ [Creating Default Application and Windows Settings for Your AppStream 2\.0 Users](#creating-default-app-Windows-settings)
+ [Optimizing the Launch Performance of Your Applications](#optimizing-app-launch-performance)

## Creating Default Application and Windows Settings for Your AppStream 2\.0 Users<a name="creating-default-app-Windows-settings"></a>

Application customizations and Windows settings that are saved to the Windows user profile folder or the user registry hive can be set as defaults\. When you save the default settings by using the **Template User** in Image Assistant, AppStream 2\.0 replaces the Windows default user profile with the profile that you configure\. The Windows default user profile is then used to create the initial settings for users in the fleet instance\. If the application or Windows settings that you configure don't work in the fleet, confirm that they are saved in the Windows user profile\. For more information, see Step 3: Create Default Application and Windows Settings in [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

Default settings that you can create and configure include:
+ Application preferences, including a browser home page, toolbar customizations, and security settings\.
+ Application data settings, including browser bookmarks and connection profiles\.
+ Windows experience settings, including displaying file name extensions and hidden folders\.

Additionally, you can modify or disable Internet Explorer security settings, such as Enhanced Security Configuration \(ESC\)\. For more information, see [Disable Internet Explorer Enhanced Security Configuration](customize-fleets.md#customize-fleets-disable-ie-esc)\.

## Optimizing the Launch Performance of Your Applications<a name="optimizing-app-launch-performance"></a>

When you create an image, AppStream 2\.0 requires that you optimize the launch performance of your applications for your users' streaming sessions\. When your applications are opened during this process, make sure that they use the initial components required by your users\. Doing so ensures that these components are captured by the optimization process\. In some cases, not all of the files required for the optimizations are detected\. Examples of such files would be plug\-ins or components that aren't opened in the image builder\. To ensure that all of the files needed for your application are captured, you can include them in the optimization manifest\. Adding files to the optimization manifest may increase the time it takes for fleet instances to be created and made available for users\. Doing so, however, reduces the time it takes for the application to be launched the first time on the fleet instance\.

To optimize all the files in a folder, open PowerShell and use the following PowerShell command: 

```
dir -path "C:\Path\To\Folder\To\Optimize" -Recurse -ErrorAction SilentlyContinue | %{$_.FullName} | Out-File "C:\ProgramData\Amazon\Photon\Prewarm\PrewarmManifest.txt" -encoding UTF8 -append
```

By default, Image Assistant replaces the application optimization manifest each time the Image Assistant **Optimize** step runs\. You must run the PowerShell command to optimize all files in a folder:
+ Each time after the **Optimize **step runs\.
+ Before you choose **Disconnect and create image** on the Image Assistant **Review** page\.

Alternatively, you can specify the optimization manifest on a per\-application basis by using the Image Assistant command line interface \(CLI\) operations\. When you specify the optimization manifest by using the Image Assistant CLI operations, AppStream 2\.0 merges the specified application optimization manifest with the files identified by the Image Assistant **Optimize** step\. For more information, see [Create Your AppStream 2\.0 Image Programmatically by Using the Image Assistant CLI Operations](programmatically-create-image.md)\.