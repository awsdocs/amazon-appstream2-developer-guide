# Add Your Custom Branding to Amazon AppStream 2\.0<a name="branding"></a>

To create a familiar experience for your users when they stream applications, you can customize the appearance of AppStream 2\.0 with your own branding images, text, and website links, and you can choose from one of several color palettes\. When you customize AppStream 2\.0, your branding is displayed to users during application streaming sessions rather than the default AppStream 2\.0 branding\.

## Custom Branding Options<a name="branding-options"></a>

You can customize the appearance of the streaming application catalog page by using the following branding options\.

**Note**  
Custom branding is not available for the user pool sign\-in portal or for the email notifications that AppStream 2\.0 sends to user pool users\.


| Branding element | Description | Requirements and recommendations | 
| --- | --- | --- | 
| Organization logo | Enables you to display an image that is familiar to your users\. The image appears in the header of the streaming application catalog page, which is displayed to users after they sign in to AppStream 2\.0\.   | File type: \.png, jpg, \.jpeg, or \.gif Maximum dimensions: 1000 px x 500 px Maximum file size: 300 KB  | 
| Organization website links |  Enables you to display links to helpful resources for your users, such as your organization's IT support and product marketing sites\. The links are displayed in the footer of the streaming application catalog page\.  | Maximum number of links: 3 Format \(URL\): https://example\.com or http://example\.com  Maximum length \(display name\): 100 letters, spaces, and numbers Special characters allowed \(display name\): @ \. / \# & \+ $  | 
| Color theme | Applied to website links, text, and buttons\. These colors are also applied as accents in the background for the streaming application catalog page\.  | Predefined themes from which to choose: 4 For information about each color theme, see [Color Theme Palettes](#branding-color-themes) later in this topic\.   | 
| Page title |  Displayed at the top of the browser tab during users' application streaming sessions\.  | Maximum length: 200 letters, spaces, and numbers\. Special characters allowed: @ \. / \# & \+ $  | 
| Favicon | Enables your users to recognize their application streaming site in a browser full of tabs or bookmarks\. The favicon icon is displayed at the top of the browser tab for the application streaming site during users' streaming sessions\.   | File type: \.png, \.jpg, \.jpeg, \.gif, or \.ico Maximum dimensions: 128 px x 128 px Maximum file size: 50 KB  | 
| Redirect URL | Enables you to specify a URL to which users are redirected when they end a streaming session\. |  Format: https://example\.com or http://example\.com  This URL is configured in the **Details** page for a stack when you create or edit a stack, not in the **Branding** page\.  | 
| Feedback URL | Enables you to specify a URL for a Send Feedback link, so that your users can submit feedback\. If you do not specify a URL, the Send Feedback link is not displayed\. |  Format: https://example\.com or http://example\.com  This URL is configured in the **Details** page for a stack when you create or edit a stack, not in the **Branding** page\.  | 

## Adding Your Custom Branding to AppStream 2\.0<a name="branding-add-custom-branding"></a>

To customize AppStream 2\.0 with your organizational branding, use the AppStream 2\.0 console to select the stack to customize, and then add your branding\.

**To add your custom branding to AppStream 2\.0**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left pane, choose **Stacks**\.

1. In the stack list, select the stack to customize with your branding\.

1. Choose **Branding**, **Custom**\.

1. For **Application catalog page**, customize how the streaming application catalog page appears to users after they sign in to AppStream 2\.0\.

   1. For **Organization logo**, do either of the following:
      + If you are uploading a logo for the first time, choose **Upload**, and then select the image to display in the header of the streaming application catalog page\.
      + If you have already uploaded a logo and need to change it, choose **Change Logo**, and then select the image to display\. 

   1. For **Organization website links**, specify up to three website links to display in the page footer\. For each link, choose the **Add Link **button, and then enter a display name and URL\. To add more links, repeat these steps for each link to add\. To remove a link, choose the **Remove **button under the link URL\.

   1. For **Color theme**, choose the colors to use for your website links, body text, and buttons, and as an accent for the page background\. For information about each color theme, see [Color Theme Palettes](#branding-color-themes) later in this topic\. 

1. For **Browser tab**, customize the page title and icon to display to users at the top of their browser tab during streaming sessions\.

   1. For **Page title**, enter the title to display at the top of the browser tab\.

   1. For **Favicon**, do either of the following:
      + If you are uploading a favicon for the first time, choose **Upload**, and then select the image to display at the top of the browser tab\.
      + If you have already uploaded a favicon and want to change it, choose **Change Logo**, and then select the image to display\. 

1. Do either of the following:
   + To apply your branding changes, choose **Save**\. When users connect to new streaming sessions that are launched for the stack, your branding changes are displayed\.
**Note**  
AppStream 2\.0 retains the custom branding changes that you save\. If you save your custom branding changes, but then choose to restore the AppStream 2\.0 default branding, your custom branding changes are saved for later use\. If you restore the AppStream 2\.0 default branding and decide later to reapply your custom branding, choose **Custom**, **Save**\. In this case, the most recently saved custom branding is displayed to your users\.
   + To discard your branding changes, choose **Cancel**\. When prompted to confirm your choice, choose **Confirm**\. If you cancel your changes, the most recently saved branding is displayed to your users\.

## Specifying a Custom Redirect URL and Feedback URL<a name="branding-specifying-feedback-URL"></a>

You can specify a URL to which your users are redirected when they end their streaming session, as well as a URL where your users can submit feedback\. By default, AppStream 2\.0 displays a **Send Feedback** link that enables users to submit feedback to AWS about the quality of their application streaming session\. To enable your users to submit feedback to a site that you specify, you can provide a custom feedback URL\. You can specify the redirect URL and feedback URL when you create a new stack or edit the details for an existing stack\. For more information, see [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install)\. 

## Previewing Your Custom Branding Changes<a name="branding-previewing-changes"></a>

You can preview how your branding changes will appear to your users by applying your branding changes to a test stack before you apply them to a production stack, and then creating a streaming URL for the test stack\. After you validate your branding changes, you can them deploy them to your production stack\. For information, see [Step 2: Provide Access to Users](getting-started.md#getting-started-access) in *Getting Started with Amazon AppStream 2\.0*\. 

## Color Theme Palettes<a name="branding-color-themes"></a>

When you choose a color theme, the colors for that theme are applied to the website links, text, and buttons in your streaming application catalog page\. A color is also applied as an accent in the background for your streaming application catalog page\. For each color in a color theme palette, the hex value is also noted\.

**Topics**
+ [Red](#color-theme-red)
+ [Light Blue](#color-theme-lightblue)
+ [Blue](#color-theme-blue)
+ [Pink](#color-theme-pink)

### Red<a name="color-theme-red"></a>

The following colors are applied when you select the red color theme\. 

![\[red icon (#d51900)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-d51900.png)    **Red \(\#d51900\)** – Used for buttons and website links\.

![\[white icon (#faf9f7)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-faf9f7.png)    **White \(\#faf9f7\)** – Used as a background accent\.

![\[dark grey icon (#404040)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-404040.png)    **Dark grey \(\#404040\)** – Used for the body text and in the progress spinner\.

When you choose the red color theme, the website links, body text, and background accent appear in your streaming application catalog page as follows\.

![\[Red color theme applied to application catalog page\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/Red-AppCatalogPage2.png)

### Light Blue<a name="color-theme-lightblue"></a>

The following colors are applied when you select the light blue color theme:

![\[light blue icon (#1d83c2)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-1D83C2.png)    **Light blue \(\#1d83c2\)** – Used for buttons and website links\.

![\[white icon (#f6f6f6)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/colore-theme-f6f6f6.png)    **White \(\#f6f6f6\)** – Used as a background accent\.

![\[dark grey icon (#333333)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-333333.png)    **Dark grey \(\#333333\)** – Used for the body text and in the progress spinner\.

When you choose the light blue color theme, the website links, body text, and background accent appear in your streaming application catalog page as follows\.

![\[Light blue color theme applied to application catalog page\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/LightBlue-AppCatalogPage2.png)

### Blue<a name="color-theme-blue"></a>

The following colors are applied when you select the blue color theme:

![\[blue icon (#0070ba)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-0070ba.png)    **Blue \(\#0070ba\)** – Used for website links\.

![\[white icon (#ffffff)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-ffffff.png)    **White \(\#ffffff\)** – Used as a background accent\.

![\[light green icon (#8ac53e)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-8ac53e.png)    **Light green \(\#8ac53e\)** – Used for buttons\.

![\[grey icon (#666666)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-666666.png)    **Grey \(\#666666\)** – Used for the body text and in the progress spinner\.

When you choose the blue color theme, the website links, body text, and background accent appear in your streaming application catalog page as follows\.

![\[Blue color theme applied to application catalog page\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/Blue-AppCatalogPage2.png)

### Pink<a name="color-theme-pink"></a>

The following colors are applied when you select the pink color theme:

![\[pink icon (#ec0069)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-ec0069.png)    **Pink \(\#ec0069\)** – Used for website links\.

![\[white icon (#ffffff)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-ffffff.png)    **White \(\#ffffff\)** – Used as a background accent\.

![\[blue icon (#3159a2)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-3159A2.png)    **Blue \(\#3159a2\)** – Used for buttons\.

![\[dark grey icon (#333333)\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/color-theme-333333.png)    **Dark grey \(\#333333\)** – Used for the body text and in the progress spinner\.

When you choose the pink color theme, the website links, body text, and background accent appear in your streaming application catalog page as follows\.

![\[Pink color theme applied to application catalog page\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/Pink-AppCatalogPage.png)