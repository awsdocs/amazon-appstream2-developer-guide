# Enable Local Printer Redirection<a name="enable-local-printer-redirection"></a>

With local printer redirection, your AppStream 2\.0 users can redirect print jobs from their streaming application to a printer that is connected to their local computer\. You don't need a printer driver installed on the AppStream 2\.0 streaming instance to enable users to print documents during their streaming sessions\. 

## Prerequisites for Local Printer Redirection<a name="local-printer-redirection-prerequisites"></a>

To ensure that your users can use local printer redirection, you must:
+ Use an image that uses a version of the AppStream 2\.0 agent released on or after July 30, 2020\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\.
+ Ensure that your users have AppStream 2\.0 client version 1\.1\.179 or later installed\. For more information, see [AppStream 2\.0 Client Version History](client-release-versions.md)\.
+ Ensure printer redirection is enabled on the stack that your users access for streaming sessions\.

## How to Enable or Disable Local Printer Redirection<a name="how-to-enable-disable-local-printer-redirection"></a>

By default, local printer redirection is enabled when the AppStream 2\.0 client is installed\. However, if local printer redirection is not enabled on the stack that your users access for streaming sessions, perform the following steps to enable it\. 

**To enable local printer redirection**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**\.

1. Choose the stack for which you want to enable local printer redirection\.

1. Choose the **User Settings** tab, and then expand the **Clipboard, file transfer, and local print permissions** section\.

1. For **Print to local device**, verify that **Enabled** is selected\. If not, choose **Edit**, and then choose **Enabled**\.

1. Choose **Update**\.

**To disable local printer redirection**

You can disable local printer redirection in either of the following ways:
+ During client installation on managed devices\.
+ By using the AppStream 2\.0 console or an AWS SDK to disable this option on an AppStream 2\.0 stack\.