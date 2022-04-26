# Update an AppStream 2\.0 Fleet<a name="update-fleets-new-image"></a>

You can make updates to an existing AppStream 2\.0 fleet\. 

When you create a new AppStream 2\.0 image, you must update your Always\-On and On\-Demand fleets to make the applications and data on the new image available to users\. If your update is minor \(for example, patching applications or the operating system\), you can update your running fleet\. When new streaming instances are created, they are created from the updated image\. Changing the image on a running fleet does not disrupt users who have active streaming sessions\. Unused streaming instances are replaced periodically, while streaming instances that users are connected to are terminated after the streaming sessions are finished\. 

You can update a fleet with a new image that runs the same operating system when the fleet is in a **Running** or **Stopped** state\. However, you can update a fleet with a new image that runs a different operating system only when the fleet is in a **Stopped** state\.

**Note**  
The application catalog that AppStream 2\.0 displays to users is based on the current image that is associated with the fleet\. If the updated image contains applications that are not specified in the older image, the applications may not launch if the user streams from an instance that is based on the older image\.

## Update a fleet with a new image<a name="update-fleets"></a>

**To update an AppStream 2\.0 fleet with a new image**

To apply operating system updates or make new applications available to users, create a new image that has these changes\. Then, update the fleet with the new image\. 

1. Connect to the image builder that you want to use and sign in with a user account that has local administrator permissions on the image builder\. To do so, do either of the following: 
   + [Use the AppStream 2\.0 console](managing-image-builders-connect.md#managing-image-builders-connect-console) \(for web connections only\)
   + [Create a streaming URL](managing-image-builders-connect.md#managing-image-builders-connect-streaming-URL) \(for web or AppStream 2\.0 client connections\)
**Note**  
If your organization requires smart card sign in, you must create a streaming URL and use the AppStream 2\.0 client for the connection\. For information about smart card sign in, see [Smart Cards](client-system-requirements-feature-support.md#feature-support-USB-devices-qualified-smart-cards)\.

1. Do either or both of the following as required: 
   + Install updates to the operating system\.
   + Install applications\.

     If an application requires the Windows operating system to restart, let it do so\. Before the operating system restarts, you are disconnected from your image builder\. After the restart is complete, connect to the image builder again, then finish installing the application\.

1. On the image builder desktop, open Image Assistant\. 

1. Follow the necessary steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   After the image status changes to **Available**, you can update the fleet with your new image\.

1. In the left navigation pane, choose **Fleets**\.

1. Select the fleet that you want to update with the new image\. 

1. On the **Fleet Details** tab, choose **Edit**\.

1. In the **Edit Fleet** dialog box, the list of available images displays in the **Name** list\. Select the new image from the list\. 

1. Choose **Update**\.

## Manage applications associated to an Elastic fleet<a name="manage-apps"></a>

**To manage applications associated to an Elastic fleet**

You can associate and disassociate applications from an Elastic fleet at any time\. Changes to the applications associated to an Elastic fleet are visible to users currently streaming from the fleet, but may not take effect\. For example, if you disassociate an application from a fleet, it will be removed from the application catalog, but the virtual hard disk will remain mounted to existing streaming sessions\.

1. Open the [AppStream 2\.0 console](managing-image-builders-connect.md#managing-image-builders-connect-console)\.

1. In the left navigation pane, choose **Fleets**, then either select the name of the fleet, or select the fleet radio button, then choose **View details**\.

1. To associate a new application to the fleet, choose **Associate** in **Assigned applications**, select the application to be associated, and choose **Associate**\.

1. To disassociate an existing application from the fleet, select the application to disassociate, choose **Disassociate**, and confirm that you want to disassociate the selected application by choosing **Disassociate**\.