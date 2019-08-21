# Update an AppStream 2\.0 Fleet with a New Image<a name="update-fleets-new-image"></a>

When you update an Amazon AppStream image, you must update your fleets to make the applications and data on the new image available to users\. If your update is minor \(for example, patching applications or the operating system\), you can update your running fleet\. When new streaming instances are created, they are created from the updated image\. Changing the image on a running fleet does not disrupt users who have active streaming sessions\. Unused streaming instances are replaced periodically, while streaming instances that users are connected to are terminated after the streaming sessions are finished\. 

You can update a fleet with a new image that runs the same operating system when the fleet is in a **Running** or **Stopped** state\. However, you can update a fleet with a new image that runs a different operating system only when the fleet is in a **Stopped** state\.

**Note**  
The application catalog that AppStream 2\.0 displays to users is based on the current image that is associated with the fleet\. If the updated image contains applications that are not specified in the older image, the applications may not launch if the user streams from an instance that is based on the older image\.