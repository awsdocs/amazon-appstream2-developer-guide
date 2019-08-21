# Image Builders<a name="managing-image-builders"></a>

Amazon AppStream 2\.0 uses EC2 instances to stream applications\. You launch instances from base images, called *image builders*, which AppStream 2\.0 provides\. To create your own custom image, you connect to an image builder instance, install and configure your applications for streaming, and then create your image by creating a snapshot of the image builder instance\.

When you launch an image builder, you choose:
+ An instance type — AppStream 2\.0 provides different instance types with various compute, memory, and graphics configurations\. The instance type must align with the instance family you need\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.
+ An operating system — AppStream 2\.0 provides the following Microsoft Windows operating systems:
  + Windows Server 2012 R2
  + Windows Server 2016 Base
  + Windows Server 2019 Base
+ The subnet and security groups to use — Make sure that the subnet and security groups provide access to the network resources that your applications require\. Typical network resources required by applications may include licensing servers, database servers, file servers, and application servers\.

**Topics**
+ [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)
+ [Image Builder Actions](managing-image-builders-actions.md)
+ [Instance Metadata for AppStream 2\.0 Image Builders](user-instance-metadata-image-builders.md)
+ [AppStream 2\.0 Base Image Version History](base-image-version-history.md)