# Image Builder Actions<a name="managing-image-builders-actions"></a>

You can perform the following actions on an image builder, depending on the current state \(status\) of the image builder instance\.

**Delete**  
Permanently delete an image builder\.   
The instance must be in a **Stopped** state\.

**Connect**  
Connect to a running image builder\. This action starts a desktop streaming session with the image builder to install and add applications to the image, and create an image\.   
The instance must be in a **Running** state\.

**Start**  
Start a stopped image builder\. A running instance is billed to your account\.  
The instance must be in a **Stopped** state\.

**Stop**  
Stop a running image builder\. A stopped instance is not billed to your account\.   
The instance must be in a **Running** state\.

None of these actions can be performed on an instance in any of the following intermediate states:
+ **Pending**
+ **Snapshotting**
+ **Stopping**
+ **Starting**
+ **Deleting**