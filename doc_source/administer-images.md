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