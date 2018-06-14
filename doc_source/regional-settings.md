# Enable Regional Settings for Your AppStream 2\.0 Users<a name="regional-settings"></a>

Amazon AppStream 2\.0 regional settings enable your users to configure their AppStream 2\.0 streaming sessions to use settings that are specific to their location or language\. In particular, users can configure the following settings:
+ **Time zone** — Determines the system time used by Windows and any applications that rely on the operating system time\. AppStream 2\.0 makes available the same options for this setting as Windows Server 2012 R2\.
+ **Locale** \(also known as culture\) — Determines the conventions used by Windows and any applications that query the Windows culture when formatting dates, numbers, or currencies or when sorting strings\. AppStream 2\.0 supports the following locales: Chinese \(Simplified and Traditional\), Dutch, English, French, German, Italian, Japanese, Korean, Portuguese, Spanish, and Thai\.
+ **Input method** — Determines the keystroke combinations that can be used to input characters in another language\.

If users change regional settings during their streaming sessions, the changes are applied to any future streaming sessions in the same AWS Region\. 

**Topics**
+ [Enable Regional Settings for Your AppStream 2\.0 Users](#regional-settings-enable)
+ [Provide Your AppStream 2\.0 Users with Guidance for Working with Regional Settings](#regional-settings-end-user)

## Enable Regional Settings for Your AppStream 2\.0 Users<a name="regional-settings-enable"></a>

To enable users to configure regional settings for a given stack during their AppStream 2\.0 streaming sessions, your stack must be associated with a fleet based on an image that uses a version of the AppStream 2\.0 agent released on or after June 6, 2018\. For more information, see [Amazon AppStream 2\.0 Agent Version History](agent-software-versions.md)\. Additionally, your image must have Windows PowerShell 5\.1 or later installed\. Images created from AppStream 2\.0 base images published on or after June 12, 2018 meet both criteria\. Images created from AppStream 2\.0 base images published before June 12, 2018 do not have Windows PowerShell 5\.1 by default\.

**To update an existing image to include Windows PowerShell 5\.1**

1. Launch a new image builder using your existing image as the base image by doing the following: 

   1.  In the left navigation pane in the AppStream 2\.0 console, choose **Images**\.

   1. Choose the **Image Builder** tab, **Launch Image Builder**, and then select your existing image\.

   1. If you are prompted to update the AppStream 2\.0 agent when you launch the image builder, select the check box, and then choose **Start**\.

1. Once your new image builder is running, connect to it and log in with a user account that has local administrator permissions\. 

1. From the image builder desktop, open Windows PowerShell\. Choose the Windows **Start** button, and then choose **Windows PowerShell**\. 

1. At the PowerShell command prompt, type the command `$PSVersionTable` to determine the version of Windows PowerShell that is installed on your image builder\. If your image builder does not include Windows PowerShell 5\.1 or later, use the following steps to install it\.

1. Open a web browser and follow the steps in [Install and Configure WMF 5\.1](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) in the Microsoft documentation, making sure that you download the Windows Management Framework \(WMF\) 5\.1 package for Windows Server 2012 R2\. WMF 5\.1 includes Windows PowerShell 5\.1\.

1. At the end of the WMF 5\.1 installation process, the installer prompts you to restart your computer\. Choose** Restart Now** to restart the image builder\.

1. Wait about 10 minutes before logging in to your image builder, even though AppStream 2\.0 prompts you to do so immediately\. Otherwise, you might encounter an error\.

1. After logging in to your image builder again, open Windows PowerShell and type the command `$PSVersionTable` to confirm that Windows PowerShell 5\.1 is installed on your image builder\.

1. Use the image builder to create a new image\. This new image now includes the latest versions of the AppStream 2\.0 agent and Windows PowerShell\.

1. Update your fleet to use the new image by doing the following: 

   1. In the left navigation pane in the AppStream 2\.0 console, choose **Fleets**, and then choose the fleet associated with the stack for which you want to enable regional settings\.

   1. On the **Fleet Details** tab, choose **Edit**\.

   1. In **Image name,** choose the new image to use for the fleet\.

For more information about using image builders to create images, see [Tutorial: Create a Custom Image](tutorial-image-builder.md)\.

## Provide Your AppStream 2\.0 Users with Guidance for Working with Regional Settings<a name="regional-settings-end-user"></a>

To help your users understand how to work with regional settings during their streaming sessions, you can provide them with the following information\. 

**Guidance for Users**

You can configure regional settings so that your AppStream 2\.0 streaming sessions use settings that are specific to your location or language\. Changes that you make during your streaming session are applied to future streaming sessions\. 

**To configure regional settings for your AppStream 2\.0 streaming sessions**

1. In your AppStream 2\.0 session, in the top left area, choose the **Settings** icon, and then choose **Regional settings**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/regional-settings-menu-item.png)

1. In the **Regional settings** dialog box, set the following options as needed\. When you're done, choose **Save**\.
   + **Time zone** — Determines the system time used by Windows and any applications that rely on the operating system time\. 
   + **Locale** \(also known as culture\) — Determines how Windows displays numbers, currency, time, and dates\. AppStream 2\.0 supports the following locales: Chinese \(Simplified and Traditional\), Dutch, English, French, German, Italian, Japanese, Korean, Portuguese, Spanish, and Thai\.
   + **Input method** — Determines the keystroke combinations that can be used to input characters in another language\. 