# Configure Default Regional Settings for Your AppStream 2\.0 Users<a name="configure-default-regional-settings"></a>

In AppStream 2\.0, users can configure their streaming sessions to use settings that are specific to their location or language\. For more information, see [Enable Your AppStream 2\.0 Users to Configure Their Regional Settings](regional-settings.md)\. You can also configure your fleets to use default settings that are specific to your users’ location or language\. In particular, you can apply the following Windows settings to your fleets:
+ **Time Zone** — Determines the system time used by Windows and any applications that rely on the operating system time\. AppStream 2\.0 makes available the same options for this setting as Windows Server 2012 R2, Windows Server 2016, and Windows Server 2019\. 
+ **Display Language** — Determines the display language used by the Windows operating system and certain Windows applications\.
+ **System Locale** — Determines the code pages \(ANSI, MS\-DOS, and Macintosh\) and bitmap font files that Windows uses for non\-Unicode applications in different languages\.
+ **User Locale** \(also known as culture\) — Determines the conventions used by Windows and any applications that query the Windows culture when formatting dates, numbers, or currencies or when sorting strings\. 
+ **Input Method** — Determines the keystroke combinations that can be used to enter characters in another language\.

Currently, AppStream 2\.0 supports English and Japanese only for these language settings\.

**Topics**
+ [Specify a Default Time Zone](#configure-default-time-zone)
+ [Specify a Default Display Language](#configure-default-dsiplay-language)
+ [Specify a Default System Locale](#configure-default-system-locale)
+ [Specify a Default User Locale](#configure-default-user-locale)
+ [Specify a Default Input Method](#configure-default-display-language)
+ [Special Considerations for Application Settings Persistence](#special-considerations-app-settings-persistence)
+ [Special Considerations for Japanese Language Settings](#special-considerations-japanese-language-settings)

## Specify a Default Time Zone<a name="configure-default-time-zone"></a>

To specify a default time zone to be used in your users’ streaming sessions, perform the steps in either of the following two procedures\.

**Topics**
+ [Specify a Default Time Zone \(Windows Server 2012 R2\)](#configure-default-time-zone)
+ [Specify a Default Time Zone \(Windows Server 2016 and Windows Server 2019\)](#configure-default-time-zone-2016-2019)

**Note**  
Currently, AppStream 2\.0 supports only **UTC** and **\(UTC\+9:00\) Osaka, Sapporo, Tokyo**\.

### Specify a Default Time Zone \(Windows Server 2012 R2\)<a name="configure-default-time-zone"></a>

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder that you want to use, choose **Connect**, and log in as **Administrator**\. 

1. On the image builder desktop, choose the Windows **Start** button, and choose **Control Panel**\.

1. Choose **Clock, Language, and Region**, then **Date and Time**, then **Change time zone**\.

1. In the **Time zone** list, choose a time zone, and choose **OK**\.

1. To apply any change to the time zone setting, restart your image builder\. To do so, choose the Windows **Start** button, and choose **Windows PowerShell**\. In PowerShell, use the restart\-computer cmdlet\.

1. While Windows restarts, the AppStream 2\.0 login prompt displays\. Wait for 10 minutes before you log in to the image builder again\. Otherwise, you may receive an error\. After 10 minutes, you can log in as **Administrator**\.

1. If required, configure additional default regional or language settings\. Otherwise, on the image builder desktop, open Image Assistant and install and configure applications for streaming\. 

1. After you finish configuring your image builder, follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\. 

1. Do one of the following:
   + Create a new fleet and choose your new image for the fleet\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
   + Update an existing fleet to use the new image\.

1. Associate your fleet with the stack that is assigned to the users for whom you are configuring the default settings\. 

   The default time zone setting that you configured is applied to the fleet instances and user streaming sessions that are launched from those instances\.

### Specify a Default Time Zone \(Windows Server 2016 and Windows Server 2019\)<a name="configure-default-time-zone-2016-2019"></a>

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder that you want to use, choose **Connect**, and log in as **Administrator**\. 

1. On the image builder desktop, choose the Windows **Start** button, and choose **Control Panel**\.

1. Specify the default time zone by using PowerShell or the Windows user interface:
   + **PowerShell**
     + Open PowerShell and run the following command: 

       ```
       Run Set-TimeZone -Id "Tokyo Standard Time"
       ```
**Note**  
To run this command, you must be logged in to the applicable computer as **Administrator**\.
   + **Windows user interface**

     1. On the image builder desktop, choose the Windows **Start** button, and type **timedate\.cpl** to open the **Date and Time **control panel item\.

     1. Right\-click the **Date and Time** icon, and choose **Run as administrator**\.

     1. When prompted by User Account Control to choose whether you want to allow the app to make changes to your device, choose **Yes**\.

     1. Choose **Change time zone**\.

     1. In the **Time zone** list, choose a time zone, and choose **OK**\.

1. To apply any change to the time zone setting, restart your image builder\. To do so, choose the Windows **Start** button, and choose **Windows PowerShell**\. In PowerShell, use the restart\-computer cmdlet\.

1. While Windows restarts, the AppStream 2\.0 login prompt displays\. Wait for 10 minutes before you log in to the image builder again\. Otherwise, you might receive an error\. After 10 minutes, you can log in as **Administrator**\.

1. If required, configure additional default regional or language settings\. Otherwise, on the image builder desktop, open Image Assistant and install and configure applications for streaming\. 

1. After you finish configuring your image builder, follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\. 

1. Do one of the following:
   + Create a new fleet and choose your new image for the fleet\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
   + Update an existing fleet to use the new image\.

1. Associate your fleet with the stack that is assigned to the users for whom you are configuring the default settings\. 

   The default time zone setting that you configured is applied to the fleet instances and user streaming sessions that are launched from those instances\.

**Note**  
Your users can change their time zone from the default setting that you configured\. They can configure their regional settings during an application streaming session, as described in [Enable Your AppStream 2\.0 Users to Configure Their Regional Settings](regional-settings.md)\. Also, if a user previously selected a time zone when streaming from any fleet instance in the same AWS Region, the user\-specified time zone setting automatically overrides any default time zone setting you specify through your image builder\.

## Specify a Default Display Language<a name="configure-default-dsiplay-language"></a>

There are two ways to specify the default display language for your users’ streaming sessions\. Use the AppStream 2\.0 default application and Windows settings feature, or configure your image builder while logged in as Administrator\.

**Note**  
Changing the display language in Windows also automatically changes the user locale and input method to match the language and region of the display language\. If you want all three settings to match, you do not need to separately change the user locale or input method\.

To specify a default display language by using the AppStream 2\.0 default application and Windows settings feature, perform the following steps\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder that you want to use, choose **Connect**, and log in as **Template User**\. 

1. On the image builder desktop, choose the Windows **Start** button, and choose **Control Panel**\.

1. Choose **Clock, Language, and Region**, then **Language**, **Add a language**\.

1. Choose a language, and choose **Add**\.
**Note**  
Currently, AppStream 2\.0 supports only **English \(United States\)** and **Japanese**\.

1. The language that you selected appears in the list of languages you added to Windows\. Choose the language that you just added\. Then choose **Move up** until the language appears at the top of the language list\.

1. Choose **Advanced Settings**\. Under **Override for Windows display language**, choose your language from the list\.

1. If you want to use the input method associated with the language that you added, under **Override for default input method**, choose the input method for the language\.

1. Choose **Save**\. When prompted to log off, choose **Log off now**\.

1. When prompted, log in again to the image builder as **Template User**\. Confirm that Windows is using the display language that you selected\. 

1. In the upper right area of the image builder desktop, choose **Admin Commands**, **Switch User**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/admin-commands-switch-user.png)

1. When prompted, log in as **Administrator**\.

1. If required, configure additional default regional or language settings\. Otherwise, on the image builder desktop, open Image Assistant and install and configure applications for streaming\. 

1. In Step 2 of the Image Assistant process, choose **Save settings**\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

1. Do one of the following:
   + Create a new fleet and choose your new image for the fleet\. For information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
   + Update an existing fleet to use the new image\.

1. Associate your fleet with the stack that is assigned to the users for whom you are configuring the default settings\. 

   The default display language and associated user locale and input method settings that you configured are applied to the fleet instances and user streaming sessions that are launched from those instances\.

   Alternatively, you can configure a default display language while logged in to the image builder as **Administrator**\. If you chose different display languages while you were logged in under the **Template User** and **Administrator** accounts and you chose **Save settings** in Step 2 of the Image Assistant process, the **Template User** settings take precedence\.

**Note**  
Your users can change their user locale and input method from the default settings that you configured\. They can change to any one of 11 different supported locales and nine different supported input methods\. To do so, they can configure their regional settings during application streaming sessions, as described in [Enable Your AppStream 2\.0 Users to Configure Their Regional Settings](regional-settings.md)\. Also, if a user previously selected a user locale or input method when streaming from any fleet instance in the same Region, those user\-specified settings automatically override any default user locale and input method that you specify through your image builder\.

## Specify a Default System Locale<a name="configure-default-system-locale"></a>

To specify a default system locale for your users’ streaming sessions, perform the following steps\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder that you want to use, choose **Connect**, and log in as **Administrator**\. 

1. On the image builder desktop, choose the Windows **Start** button, and choose **Control Panel**\.

1. Choose **Clock, Language, and Region**, then **Region**\.

1. In the **Region** dialog box, choose the **Formats** tab\.

1. Choose **Change system locale**\. 

1. In the **Region Settings** dialog box, in the **Current system locale** list, choose a language and region\. 
**Note**  
Currently, AppStream 2\.0 supports only **English \(United States\) **and **Japanese \(Japan\)**\.

1. Choose **OK **to close the **Region Settings** dialog box, and choose **OK** again to close the **Region **dialog box\.

1. When prompted to restart your computer, allow Windows to restart\.

1. While Windows restarts, the AppStream 2\.0 login prompt displays\. Wait for 10 minutes before you log in to the image builder again\. Otherwise, you may receive an error\. After 10 minutes, you can log in as **Administrator**\.

1. If required, configure additional default regional or language settings\. Otherwise, on the image builder desktop, open Image Assistant and install and configure applications for streaming\. After you finish configuring your image builder, follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\. 

1. Do one of the following:
   + Create a new fleet and choose your new image for the fleet\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
   + Update an existing fleet to use the new image\.

1. Associate your fleet with the stack that is assigned to the users for whom you are configuring the default settings\. 

   The default system locale setting that you configured is applied to the fleet instances and user streaming sessions that are launched from those instances\.

## Specify a Default User Locale<a name="configure-default-user-locale"></a>

To specify a default user locale for your users’ streaming sessions, perform the following steps\.

**Note**  
If you plan to configure the display language and you want the user locale and display language to match, you do not need to change the user locale\. Changing the display language automatically changes the user locale to match\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder that you want to use, choose **Connect**, and log in as **Administrator**\. 

1. On the image builder desktop, choose the Windows **Start** button, and choose **Control Panel**\.

1. Choose **Clock, Language, and Region**, then **Region**\.

1. In the **Region** dialog box, choose the **Formats** tab\.

1. In the **Format** list, choose a language and region\.
**Note**  
Currently, AppStream 2\.0 supports only **English \(United States\) **and **Japanese \(Japan\)**\.

1. Choose **OK **to close the **Region** dialog box\.

1. If required, configure additional default regional or language settings\. Otherwise, on the image builder desktop, open Image Assistant and install and configure applications for streaming\. 

1. In Step 2 of the Image Assistant process, choose **Save settings**\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

1. Do one of the following:
   + Create a new fleet and choose your new image for the fleet\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
   + Update an existing fleet to use the new image\.

1. Associate your fleet with the stack that is assigned to the users for whom you are configuring the default settings\. 

   The default user locale setting that you configured is applied to the fleet instances and user streaming sessions that are launched from those instances\.

**Note**  
Your users can change their user locale from the default setting that you configured to any one of 11 different supported locales\. To do so, they can configure their regional settings during application streaming sessions, as described in [Enable Your AppStream 2\.0 Users to Configure Their Regional Settings](regional-settings.md)\. Also, if a user previously selected a user locale when streaming from any fleet instance in the same Region, that user\-specified setting automatically overrides any default user locale setting that you specify through your image builder\.

## Specify a Default Input Method<a name="configure-default-display-language"></a>

To specify a default input method to be used in your users’ streaming sessions, perform the following steps\.

**Note**  
If you plan to configure the display language, and you want the input method and display language to match, you do not need to change the input method\. Changing the display language in Windows also automatically changes the user locale and input method to match the language and region of the display language\. If you want all three settings to match, you do not need to separately change the user locale or input method\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder that you want to use, choose **Connect**, and log in as **Administrator**\. 

1. On the image builder desktop, choose the Windows **Start** button, and choose **Control Panel**\.

1. Choose **Clock, Language, and Region**, then **Language**, **Add a language**\.

1. Choose a language, and choose **Add**\.
**Note**  
Currently, AppStream 2\.0 supports only **English \(United States\)** and **Japanese**\.

1. The language that you chose appears in the list of languages you added to Windows\.

1. Choose **Advanced Settings**\. Under **Override for default input method**, choose the input method for the language you added\.

1. Choose **Save**\.

1. Log off and log in again\. To do so, choose the Windows **Start** button on the image builder desktop\. Choose **ImageBuilderAdmin**, **Sign out**\. When prompted, log in as Administrator\.

1. If required, configure additional default regional or language settings\. Otherwise, on the image builder desktop, open Image Assistant and install and configure applications for streaming\. 

1. In Step 2 of the Image Assistant process, choose **Save settings**\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

1. Do one of the following:
   + Create a new fleet and choose your new image for the fleet\. For information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
   + Update an existing fleet to use the new image\.

1. Associate your fleet with the stack that is assigned to the users for whom you are configuring the default settings\. 

   The default input method that you configured is applied to the fleet instances and user streaming sessions that are launched from those instances\.

**Note**  
Your users can change their input method from the default setting that you configured to any one of nine different supported input methods\. They can configure this setting by configuring their regional settings during application streaming sessions, as described in [Enable Your AppStream 2\.0 Users to Configure Their Regional Settings](regional-settings.md)\. Also, if a user previously selected an input method when streaming from any fleet instance in the same Region, that user\-specified setting automatically overrides any default input method that you specify through your image builder\.

## Special Considerations for Application Settings Persistence<a name="special-considerations-app-settings-persistence"></a>

When you create a stack in the AppStream 2\.0 console, in **Step 3: User Settings**, if you use the same settings group under **Application settings persistence** as another stack that uses different regional settings, only one set of regional settings is used for both stacks\. For each user, the default regional settings for the stack that the user logs into first automatically override the default regional settings of any other stacks in the same application settings group\. To avoid this problem, do not use the same application settings group for two different stacks that have different regional settings\.

## Special Considerations for Japanese Language Settings<a name="special-considerations-japanese-language-settings"></a>

This section describes key points to keep in mind when configuring Japanese language settings for your AppStream 2\.0 users\.

### <a name="special-considerations-as2-cient"></a>

### AWS CLI<a name="special-considerations-japanese-language-AWS-CLI"></a>

Changing the Windows system locale to Japanese requires that your image builder have AWS Command Line Interface \(AWS CLI\) version 1\.16\.30 or later installed\. To update the version of AWS CLI on your image builder, follow the steps in [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html)\.

### Japanese Keyboards<a name="special-considerations-japanese-language-keyboards"></a>

If your image builder input method is set to Japanese when you create an image, AppStream 2\.0 automatically configures your image to use a Japanese keyboard\. Any fleets that use the image are also automatically configured to use Japanese keyboards\. However, if you want to use a Japanese keyboard within your image builder session, update the following registry settings for the HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\i8042prt\\Parameters registry key:


| Name | Type | Data | 
| --- | --- | --- | 
| LayerDriver JPN | REG\_SZ  |  kbd106\.dll  | 
| OverrideKeyboardIdentifier | REG\_SZ | PCAT\_106KEY | 
| OverrideKeyboardSubtype | DWORD | 2 | 
| OverrideKeyboardType | DWORD | 7 | 

After changing these settings, restart your image builder\. To do so, choose the Windows **Start** button, and choose **Windows PowerShell**\. In PowerShell, use the restart\-computer cmdlet\.