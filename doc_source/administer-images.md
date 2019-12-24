# Administer Your Amazon AppStream 2\.0 Images<a name="administer-images"></a>

Available images are listed in the **Image Registry** in the AppStream 2\.0 console, and categorized by visibility as follows: 
+ **Public** — Base images that are owned and made available by AWS\. Base images include the latest Windows operating system and the AppStream 2\.0 agent software\. You can use these base images to create new images that include your own applications\. For information about the base images released by AWS, see [AppStream 2\.0 Base Image Version History](base-image-version-history.md)\. 
+ **Private** — Images that you create and own, and that you have not shared with other AWS accounts\. 
+ **Shared with others** — Images that you create and own, and that you have shared with one or more AWS accounts in the same AWS Region\. When you share an image with another AWS account, you can specify whether the image can be used for an image builder \(to create a new image\), for a fleet, or both\.
+ **Shared with me** — Images that are created and owned by another AWS account in the same AWS Region, and that are shared with your AWS account\. Depending on the permissions that the owner provided when sharing the image with your account, you can use this image for image builders, for fleets, or both\.

**Topics**
+ [Delete a Private Image](#delete-private-image)
+ [Copy an Image That You Own to Another AWS Region](#copy-image-different-region)
+ [Share an Image That You Own With Another AWS Account](#share-image-with-another-account)
+ [Stop Sharing an Image That You Own](#stop-sharing-image-with-all-accounts)
+ [Keep Your AppStream 2\.0 Image Up\-to\-Date](#keep-image-updated)
+ [Windows Update and Antivirus Software on AppStream 2\.0](#windows-update-antivirus-software)
+ [Programmatically Create a New Image](#create-image-programmatically)

## Delete a Private Image<a name="delete-private-image"></a>

You can delete your private images when you no longer need them\. You can't delete an image that is used by fleets or shared with other AWS accounts\. To delete an image that is used by fleets or shared, you must first remove the image from any fleets and remove all image sharing permissions\. After you delete an image, you can't recover it\.

**To delete a private image**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Registry**\.

1. In the image list, select the private image you want to delete\.

1. Choose **Actions**, **Delete**, then choose **Delete** again\.

   The image is removed from the image registry and deleted\.

## Copy an Image That You Own to Another AWS Region<a name="copy-image-different-region"></a>

You can copy images that you own to another AWS Region\. Using the same image across different AWS Regions can help simplify global deployments of your applications on AppStream 2\.0\. By deploying your applications in the AWS Regions that are geographically closest to your users, you can help provide your users with a more responsive experience\.

**To copy an image that you own to another AWS Region**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Registry**\.

1. In the image list, select the image that you want to copy to another AWS Region\.

1. Choose **Actions**, **Copy**\. 

1. In the **Copy image** dialog box, in **Destination region**, select the AWS Region that you want to copy the image to\.

1. Type a unique name and optionally, a description for the image in **Destination region**\. 

1. Choose **Copy Image**\.

## Share an Image That You Own With Another AWS Account<a name="share-image-with-another-account"></a>

AppStream 2\.0 images are a regional resource, so you can share an image that you own with other AWS accounts within the same AWS Region\. Doing so can be helpful in several different scenarios\. For example, if you separate your development and production resources by using different AWS accounts, you can create an image by using your development account\. Then you can share the image with your production account\. If your organization is an independent software vendor \(ISV\), you can share optimized images with your customers\. Optimized images that have the required applications already installed and configured let your customers get started with your applications quickly, so that they won't need to install and configure those applications themselves\.

When you share an image with another AWS account, you specify whether the destination account can use the image in a fleet or create new images by creating an image builder\. You continue to own images that you share\. This way, you can add, change, or remove permissions as needed for your shared images\.

If you share an image with an account and grant the account fleet permissions, the shared image can be used to create or update fleets in that account\. If you remove these permissions later, the account can no longer use the image\. For fleets in the account that use the shared image, the desired capacity is set to 0, which prevents new fleet instances from being created\. Existing sessions continue until the streaming session ends\. For new fleet instances to be created, the fleet in that account must be updated with a valid image\.

If you share an image with an account and grant the account image builder permissions, the shared image can be used to create image builders and images in that account\. If you remove these permissions later, image builders and images that were created from your image are not affected\. 

**Important**  
After you share an image with an account, you can't control image builders or images in the account that are created from your image\. For this reason, grant image builder permissions to an account only if you want to enable the account to make a copy of your image, and retain access to the copy after you stop sharing your image\.

**To share an image that you own with another AWS account**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Registry**\.

1. In the image list, select the image that you want to share\.

1. Choose **Actions**, **Share**\.

1. In the **Share image** dialog box, choose **Add account**\.

1. Type the 12\-digit AWS account ID of the account that you want to share the image with, and then select whether the account can do one or both of the following:
   + Use the image to launch an image builder, if you want to create a new image\.
   + Use the image with a fleet\.

   To remove an account from the list of accounts that the image is shared with, in the row for the account you want to remove, choose the X icon to the right of the **Use for fleet **option\.

1. To share the image with more AWS accounts, repeat step 6 for each account that you want to share the image with\. 

1. Choose **Share Image**\.

**To add or update image sharing permissions for an image that you own**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Registry**\.

1. In the image list, select the image that you want to change the permissions for\.

1. Below the image list, choose the **Permissions** tab for the image you selected, then choose **Edit**\.

1. In the **Edit image permissions** dialog box, select or clear one or both of the following image sharing options as needed for one or more AWS accounts\. If you clear both options for an account, the image is no longer shared with that account\. 
   + Use the image to launch an image builder, if you want to create a new image\.
   + Use the image with a fleet\.

   To remove an account from the list of accounts that the image is shared with, in the row for the account you want to remove, choose the X icon to the right of the **Use for fleet **option\.

1. To edit image sharing permissions for more AWS accounts, repeat step 5 for each account you want to update permissions for\. 

1. Choose **Update image sharing permissions**\.

## Stop Sharing an Image That You Own<a name="stop-sharing-image-with-all-accounts"></a>

Follow these steps to stop sharing an image that you own with any other AWS account\.

**To stop sharing an image that you own with any other AWS account**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Images**, **Image Registry**\.

1. In the image list, select the image that you want to change the permissions for\.

1. Below the image list, choose the **Permissions** tab for the image you selected, then choose **Edit**\.

1. In the **Edit image permissions** dialog box, in the row for all AWS accounts that the image is shared with, choose the X icon to the right of the **Use for fleet **option\.

1. Choose **Update image sharing permissions**\.

## Keep Your AppStream 2\.0 Image Up\-to\-Date<a name="keep-image-updated"></a>

AppStream 2\.0 provides an automated way to update your image builder with newer AppStream 2\.0 agent software\. Doing so enables you to create a new image whenever a new version of the agent is released\. You can then test the image before updating your production fleets\. For more information about how to manage the AppStream 2\.0 agent software, see [Manage AppStream 2\.0 Agent Versions](base-images-agent.md)\. 

You are responsible for installing and maintaining the updates for the Windows operating system, your applications, and their dependencies\. To keep your AppStream 2\.0 image updated with the latest Windows operating system updates, do one of the following:
+ Install your applications on the latest base image each time a new image is released\.
+ Install the updates for the Windows operating system, your applications, and their dependencies on an existing image builder\.
+ Install the updates for the Windows operating system, your applications, and their dependencies on a new image builder from an existing image\.

After you create a new image with the latest Windows operating system, applications and their dependencies, and the AppStream 2\.0 agent software, test the image on a development fleet\. After you verify that your applications work as expected, update your production fleet with the new image\.

## Windows Update and Antivirus Software on AppStream 2\.0<a name="windows-update-antivirus-software"></a>

AppStream 2\.0 streaming instances are non\-persistent\. When a user streaming session ends, AppStream 2\.0 terminates the instance used by the session and, depending on your scaling policies, provisions a new instance to replace it in your fleet\. All fleet instances are provisioned from the same image\. Because images cannot be changed once created, all fleet instances used in user streaming sessions have only the Windows and application updates that were installed on the underlying image when the image was created\. In addition, because a fleet instance used for a streaming session terminates at the end of the session, any updates made to Windows or to applications on the instance during the streaming session will not persist to future sessions by the same user or other users\.

**Note**  
If you enabled application settings persistence for your stack, AppStream 2\.0 persists Windows and application configuration changes made by a user to future sessions for the same user if those configuration changes are stored in the user’s Windows profile\. However, the application settings persistence feature persists only Windows and application configuration settings\. It does not persist software updates to Windows or applications on the streaming instance\.

For these reasons, AppStream 2\.0 takes the following approach to Windows Update and antivirus software on AppStream 2\.0 instances\.

### Windows Update<a name="windows-update-antivirus-software-wu"></a>

Windows Update is not enabled by default on AppStream 2\.0 base images\. If you enable Windows Update on an image builder and then try to create an image, Image Assistant displays a warning and disables Windows Update during the image creation process\. To ensure that your fleet instances have the latest Windows updates installed, we recommend that you install Windows updates on your image builder, create a new image, and update your fleet with the new image on a regular basis\.

### Antivirus Software<a name="windows-update-antivirus-software-av"></a>

If you choose to install antivirus software on your image, we recommend that you do not enable automatic updates for the antivirus software\. Otherwise, the antivirus software may attempt to update itself with the latest definition files or other updates during user sessions\. This may affect performance\. In addition, any updates made to the antivirus software will not persist beyond the current user session\. To ensure that your fleet instances always have the latest antivirus updates, we recommend that you do either of the following:
+ Update your image builder and create a new image on a regular basis \(for example, by using the [Image Assistant CLI operations](https://docs.aws.amazon.com/appstream2/latest/developerguide/programmatically-create-image.html)\)\.
+ Use an antivirus application that delegates scanning or other operations to an always\-up\-to\-date external server\.

**Note**  
Even if you do not enable automatic updates for your antivirus software, the antivirus software may perform hard drive scans or other operations that may impact the performance of your fleet instances during user sessions\.

AppStream 2\.0 Windows Server 2012 R2 base images do not include any antivirus software\. On AppStream 2\.0 Windows Server 2016 and Windows Server 2019 base images published on or after September 10, 2019, Windows Defender is not enabled by default\. On AppStream 2\.0 Windows Server 2016 and Windows Server 2019 base images published on June 24, 2019, Windows Defender is enabled by default\.

**To enable Windows Defender manually**

If Windows Defender is not enabled on your base image, you can enable it manually\. To do so, complete the following steps\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\. 

1. Choose the image builder on which to enable Windows Defender, verify that it is in the **Running** state, and choose **Connect**\. 

1. Log in to the image builder with the local **Administrator** account or with a domain user account that has local administrator permissions\.

1. Open Registry Editor\.

1. Navigate to the following location in the registry: **HKLM\\SOFTWARE\\Policies\\Microsoft\\Windows Defender\\DisableAntiSpyware**\. 

1. To edit this registry key, double\-click it, or right\-click the registry key, and choose **Modify**\.

1. In the **Edit DWORD \(32\-bit\) Value** dialog box, in **Value data**, change **1** to **0**\.

1. Choose **OK**\.

1. Close Registry Editor\.

1. Open the Microsoft Management Console \(MMC\) **Services** snap\-in \(`services.msc`\)\.

1. In the list of services, do either of the following:
   + Right\-click **Windows Defender Antivirus Service**, and choose **Start**\.
   + Double\-click **Windows Defender Antivirus Service**, choose **Start** in the properties dialog box, and then choose **OK**\.

1. Close the **Services** snap\-in\.

## Programmatically Create a New Image<a name="create-image-programmatically"></a>

You can create AppStream 2\.0 images programmatically by connecting to an image builder and using the Image Assistant command line interface \(CLI\) operations\. For more information, see [Create Your AppStream 2\.0 Image Programmatically by Using the Image Assistant CLI Operations](programmatically-create-image.md)\. 