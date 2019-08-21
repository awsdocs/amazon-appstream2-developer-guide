# Enable and Test Dynamic App Providers<a name="enable-test-dynamic-app-providers"></a>

Dynamic app providers must first be enabled within an AppStream 2\.0 image\. After you enable these providers, they can manage applications for users on the streaming instance\.

## Enable Dynamic App Providers<a name="enable-dynamic-app-providers"></a>

 To enable this capability, you must add your dynamic app provider details to a configuration file on the image builder\. The image builder must be joined to a Microsoft Active Directory domain\. Perform the following steps on an image builder, then you can test your dynamic apps to verify that they function as expected\. Finally, finish creating your image\.

**Note**  
Third\-party dynamic app providers may modify the configuration file during install\. For installation instructions, see the documentation for the applicable provider\.

**To enable dynamic app providers**

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose an image builder that is joined to a Microsoft Active Directory domain\. Verify that the image builder is in the **Running** state, and choose **Connect**\.

1. When prompted, choose **Administrator**\.

1. Navigate to C:\\ProgramData\\Amazon\\AppStream\\AppCatalogHelper\\DynamicAppCatalog\\, and open the **Agents\.json** configuration file\.

1. In the **Agents\.json** file, add the following entries:

   "DisplayName": "<Uninstall hive display name value>",

   "Path": "<C:\\path\\to\\client\\application>"

   *DisplayName* must match the **DisplayName** registry value for the **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall** key created for your application\.

1. Install your dynamic app provider\.

1. On the image builder desktop, open Image Assistant\.

1. Optionally, install any other applications that you want to include in the image\. 

1. In Image Assistant, on the **1\. Add Apps** page, select the **Enable dynamic app providers** check box\.

1. On the same page, if you installed other applications as described in step 8, choose **\+Add App**, and specify the applications to add\.
**Note**  
When you use a dynamic app provider, you don't need to specify any applications in the image\. If you specify applications in the image, they can't be removed by dynamic app providers\.

1. Proceed to the steps in the next section to test your dynamic app provider\.

## Test Dynamic App Providers \(Optional\)<a name="test-dynamic-app-providers"></a>

After you enable your dynamic app provider on an image builder, you can test the provider to verify that it functions as expected\. To do so, perform the following steps before you finish creating the image\.

**To test dynamic app providers**

1. Do one of the following: 
   + If you are already logged on as an Administrator to the image builder on which you enabled dynamic app providers, you must switch to an account that does not have local administrator permissions on the image builder\. To do so, in the upper right corner of the image builder session toolbar, choose **Admin Commands**, **Switch User**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/admin-commands-switch-user.png)
   + If you are not already logged on to the image builder, in the left navigation pane, choose **Images**, **Image Builder**\. Choose the image builder on which you enabled your dynamic app providers\. Verify that the image builder is in the **Running** state, and choose **Connect**\.

1. When prompted, choose **Directory User**, and log on with a domain user account that does not have local administrator permissions on the image builder\. 

1. On the image builder desktop, open Image Assistant, if it is not already open\. 

1. On the **Test Apps** page, if you specified any applications in the image that are not from the dynamic app provider, they display first in the list\. It may take a few moments for applications from dynamic app providers to appear in the list\.

1. Choose an application from the list and open it to verify that it functions as expected\.

1. After you finish testing, in the lower right corner of the **Test Apps** page, choose **Switch user**\. 

1. Choose **Administrator**, and log back into the image builder\.

1. Follow the necessary steps in Image Assistant to finish creating your image\. For information about how to create an image, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   AppStream 2\.0 automatically optimizes the agents that are specified in the **Agents\.json** configuration file\.