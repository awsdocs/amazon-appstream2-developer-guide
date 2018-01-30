# AppStream 2\.0 Image Builders<a name="managing-image-builders"></a>

AppStream 2\.0 provides virtual machines, or instances, that are used to install and add applications into and create your image\. These instances are called *image builders*\. You can launch an image builder from a base image provided by AWS, or from an image that you create\. After your image builder instance is available \(running\), you can connect to the image builder to start a desktop session, install your applications, add your applications to an image, and create an image\. 

While launching a new image builder, you can choose from different instance types with various compute, memory, and graphics configurations\. Note that the instance type must align with the instance family you need\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.

You also provide a VPC subnet so that AppStream 2\.0 can establish a network interface to the image builder\. This connection provides your image builder with access to resources that might be needed while you install and add applications; for example, file servers, licensing servers, database servers, and so on\. For more information, see [Tutorial: Create a Custom Image](tutorial-image-builder.md)\. 

## Actions<a name="managing-image-builders-actions"></a>

The following actions can be performed on an image builder, depending on the current state \(status\) of the image builder instance\.

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