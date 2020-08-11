# Enable Your AppStream 2\.0 Users to Configure Their Regional Settings<a name="regional-settings"></a>

Users can configure their Amazon AppStream 2\.0 streaming sessions to use settings that are specific to their location or language\. In particular, users can configure the following settings:
+ **Time zone** — Determines the system time used by Windows and any applications that rely on the operating system time\. AppStream 2\.0 makes available the same options for this setting as the Windows Server version used in your fleet\.
+ **Locale** \(also known as culture\) — Determines the conventions used by Windows and any applications that query the Windows culture when formatting dates, numbers, or currencies or when sorting strings\. For a list of locales that AppStream 2\.0 supports, see [Supported Locales](#supported-locales)\.
+ **Input method** — Determines the keystroke combinations that can be used to input characters in another language\.

If users change regional settings during their streaming sessions, the changes are applied to any future streaming sessions in the same AWS Region\.

**Note**  
For guidance that you can provide your users to help them get started with configuring their regional settings, see [Configure Regional Settings](regional-settings-end-user.md)\.

**Topics**
+ [Supported Locales](#supported-locales)
+ [Enable Regional Settings for Your AppStream 2\.0 Users](#regional-settings-enable)

## Supported Locales<a name="supported-locales"></a>

AppStream 2\.0 supports the following locales:


| Locale | Language culture name | 
| --- | --- | 
| Chinese \(Simplified, China\) | zh\-CN | 
| Chinese \(Simplified, Singapore\) | zh\-SG | 
| Chinese \(Traditional, Taiwan\) | zh\-TW | 
| Dutch \(The Netherlands\) | nl\-NL | 
| English \(Australia\) | en\-AU | 
| English \(Canada\) | en\-CA | 
| English \(United Kingdom\) | en\-GB | 
| English \(United States\) | en\-US | 
| French \(France\) | fr\-FR | 
| German \(Germany\) | de\-DE | 
| Italian \(Italy\) | it\-IT | 
| Japanese \(Japan\) | ja\-JP | 
| Korean \(Korea\) | ko\-KR | 
| Portuguese \(Brazil\) | pt\-BR | 
| Spanish \(Spain, International Sort\)  | es\-ES | 
| Thai \(Thailand\) | th\-TH | 

## Enable Regional Settings for Your AppStream 2\.0 Users<a name="regional-settings-enable"></a>

To enable users to configure regional settings for a given stack during their AppStream 2\.0 streaming sessions, your stack must be associated with a fleet based on an image that uses a version of the AppStream 2\.0 agent released on or after June 6, 2018\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\. Additionally, your image must have Windows PowerShell 5\.1 or later installed\. Images created from AppStream 2\.0 base images published on or after June 12, 2018 meet both criteria\. Images created from AppStream 2\.0 base images published before June 12, 2018 do not have Windows PowerShell 5\.1 by default\.

**To update an existing image to include Windows PowerShell 5\.1**

1. Launch a new image builder using your existing image as the base image by doing the following: 

   1.  In the left navigation pane in the AppStream 2\.0 console, choose **Images**\.

   1. Choose the **Image Builder** tab, **Launch Image Builder**, and then select your existing image\.

   1. If you are prompted to update the AppStream 2\.0 agent when you launch the image builder, select the check box, and then choose **Start**\.

1. Once your new image builder is running, connect to it and log in with a user account that has local administrator permissions\. 

1. From the image builder desktop, open Windows PowerShell\. Choose the Windows **Start** button, and then choose **Windows PowerShell**\. 

1. At the PowerShell command prompt, type the command `$PSVersionTable` to determine the version of Windows PowerShell that is installed on your image builder\. If your image builder does not include Windows PowerShell 5\.1 or later, use the following steps to install it\.

1. Open a web browser and follow the steps in [Install and Configure WMF 5\.1](https://docs.microsoft.com/en-us/powershell/scripting/windows-powershell/wmf/setup/install-configure?view=powershell-7) in the Microsoft documentation, making sure that you download the Windows Management Framework \(WMF\) 5\.1 package for Windows Server 2012 R2\. WMF 5\.1 includes Windows PowerShell 5\.1\.

1. At the end of the WMF 5\.1 installation process, the installer prompts you to restart your computer\. Choose** Restart Now** to restart the image builder\.

1. Wait about 10 minutes before logging in to your image builder, even though AppStream 2\.0 prompts you to do so immediately\. Otherwise, you might encounter an error\.

1. After logging in to your image builder again, open Windows PowerShell and type the command `$PSVersionTable` to confirm that Windows PowerShell 5\.1 is installed on your image builder\.

1. Use the image builder to create a new image\. This new image now includes the latest versions of the AppStream 2\.0 agent and Windows PowerShell\.

1. Update your fleet to use the new image by doing the following: 

   1. In the left navigation pane in the AppStream 2\.0 console, choose **Fleets**, and then choose the fleet associated with the stack for which you want to enable regional settings\.

   1. On the **Fleet Details** tab, choose **Edit**\.

   1. In **Image name,** choose the new image to use for the fleet\.

For more information about using image builders to create images, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.