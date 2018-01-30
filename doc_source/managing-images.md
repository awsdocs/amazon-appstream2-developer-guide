# AppStream 2\.0 Images<a name="managing-images"></a>

An Amazon AppStream 2\.0 image contains applications that can be streamed to users\. The image is used to launch streaming instances that are part of an AppStream 2\.0 fleet\. All images available to you are listed under the **Image Registry** section in the AWS Management Console\. Note that the image's instance family must align with the instance type you need\. For more information, see [AppStream 2\.0 Instance Families](instance-types.md)\.

The images in your image registry are differentiated by these visibility attributes:

+ **Public Images** — Base images that are made available by AWS to help you create images with your own applications\.

+ **Private Images** — Images that are created and owned by you\.

You can use either public or private images to launch an image builder and set up your AppStream 2\.0 fleet\. For more information, see [Tutorial: Create a Custom Image](tutorial-image-builder.md)\.

You can also delete your private images\. Note that a private image cannot be deleted if there are active fleets using it\. You must stop all associated fleets before deleting the image\.