# AppStream 2\.0 Base Image and Managed Image Update Release Notes<a name="base-image-version-history"></a>

Amazon AppStream 2\.0 provides base images to help you create images that include your own applications\. Base images are Amazon Machine Images \(AMIs\) that contain software configurations specific to the operating system\. For AppStream 2\.0, each base image includes the AppStream 2\.0 agent and the latest version of one of the following operating systems:
+ Windows Server 2012 R2 — Available on the following image types: Base, Graphics Design, Graphics G4dn, Graphics Pro, and Sample apps
+ Windows Server 2016 Base — Available on the following image types: Base, Graphics Design, Graphics G4dn, and Graphics Pro
+ Windows Server 2019 Base — Available on the following image types: Base, Graphics G4dn, and Graphics Pro
+ Amazon Linux 2 – Available on the following image types: Base, Graphics G4dn, and Graphics Pro

After you create your own image that includes your own applications, you are responsible for installing and maintaining the updates for the operating system, your applications, and their dependencies\. AppStream 2\.0 provides an automated way to update your image using managed AppStream 2\.0 image updates\. With managed image updates, you select the image that you want to update\. AppStream 2\.0 creates an image builder in the same AWS account and Region to install the updates and create the new image\. After the new image is created, you can test it on a pre\-production fleet before updating your production fleets or sharing the image with other AWS accounts\. For more information, see "Keep Your AppStream 2\.0 Image Up\-to\-Date" in [Administer Your Amazon AppStream 2\.0 Images](administer-images.md)\.

For information about the latest AppStream 2\.0 agent, see [AppStream 2\.0 Agent Release Notes](agent-software-versions.md)\.

The following table lists the latest released images\.


| Image type | Image name | 
| --- | --- | 
| Base |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| Graphics Design |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| Graphics G4dn |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| Graphics Pro |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| Sample apps |  Amazon\-AppStream2\-Sample\-Image\-10\-08\-2021 For information about how to access this base image, see [Get Started with Amazon AppStream 2\.0: Set Up With Sample Applications](getting-started.md)\.  | 

The latest Windows base images were released on March 3, 2022, and the latest managed AppStream 2\.0 image updates for the Windows platform were released on February 18, 2022\. The following table lists the software components for the latest released base images and the components that are available if you update your image using managed image updates\. If the version is marked “latest”, the current stable software component available from the vendor will be installed\. If the version is marked “not included”, managed image updates is not managing the component and the version will not be changed when you update your image\.

The following table lists the software components for the latest released Windows images\.


| Software component | Latest base images \(March 3, 2022\) | Managed AppStream 2\.0 image updates \(February 18, 2022\) | 
| --- | --- | --- | 
| Amazon AWS \(AvsCamera\) Driver | 19\.42\.32\.749 | 19\.42\.32\.749 | 
| Amazon CloudWatch Agent | 1\.3\.50741 | 1\.3\.50740 | 
| SSM Agent | 3\.0\.1295\.0  | Not included | 
| Amazon WDDM Hook Driver/NICE DCV Virtual Display | NICE DCV Virtual Display 1\.0\.34\.0 \(Windows Server 2016/2019\)Amazon WDDM Hook Driver 1\.0\.0\.56 \(Windows Server 2012 R2\) | NICE DCV Virtual Display 1\.0\.34\.0 \(Windows Server 2016/2019\)Amazon WDDM Hook Driver 1\.0\.0\.56 \(Windows Server 2012 R2\) | 
| AMD Driver for Graphics Design instances | 24\.20\.13028\.3002 \(Windows Server 2012 R2\)24\.20\.13028\.5012 \(Windows Server 2016/2019\) | 24\.20\.13028\.3002 \(Windows Server 2012 R2\)24\.20\.13028\.5012 \(Windows Server 2016/2019\) | 
| AppStream 2\.0 Agent | 02\-21\-2021 | 03\-14\-2022 | 
| AWS Command Line Interface \(AWS CLI\) | 1\.18\.138 | Not included | 
| Amazon EC2 Config service | 4\.9\.4508 \(Windows Server 2012 R2 only\)  | Not included | 
| Firefox | 96\.0\.3 | 97\.0 | 
| Microsoft Message Queuing \(MSMQ\) | Installed with Windows Server | Installed with Windows Server | 
| NVIDIA Graphics Driver for Graphics Pro and G4dn instances | 451\.48 | Not included | 
| Process monitor | 3\.70  | [Latest](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) | 
| Quality Windows Audio/Video Experience \(qWAVE\) | Installed with Windows Server | Installed with Windows Server | 
| Visual C\+\+ redistributable packages | 12\.0\.30501\.0 | 12\.0\.30501\.0 | 
| Windows Server updates | Base image updates as of January 11, 2022 | [Latest](https://www.catalog.update.microsoft.com/home.aspx) | 
| WinSCard Filter Driver | 1\.0\.15\.0 | 1\.0\.15\.0 | 

The latest Linux base images were released on February 18, 2022\. The following table lists the software components for the latest released Linux base images\.


| Software component | Latest base images \(February 18, 2022\) | 
| --- | --- | 
| AWS Command Line Interface \(AWS CLI\) | 1\.18\.147\-1 | 
| Amazon CloudWatch Agent | 1\.247347\.4\-1 | 
| SSM Agent | 3\.1\.501\.0\-1  | 
| NICE DCV Server AppStream | 2021\.2\.11373\-1 | 
| Cloud\-init | 19\.3\-44 | 
| AL2 Kernel | 4\.14\.252\-195\.483 | 
| NVIDIA Graphics Driver for Graphics Pro and G4dn instances | 470\.63\.01 | 
| Cuda Version | 470\.63\.01 | 

**Important**  
The following public images are deprecated and therefore no longer available from AWS:  
Windows images released before September 2021
Linux images dated 11\-15\-2021
Images for the Graphics Desktop instance family

The following table describes all released base images\.


| Release | Platform | Image  | Changes | 
| --- | --- | --- | --- | 
| 03\-03\-2022 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 02\-18\-2022 |  Amazon Linux 2  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 11\-19\-2021  |  Amazon Linux 2  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 11\-15\-2021  |  Amazon Linux 2  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 10\-08\-2021 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 07\-19\-2021 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 06\-01\-2021 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 12\-28\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 07\-16\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 04\-22\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 03\-18\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 03\-16\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 03\-05\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 01\-13\-2020 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 12\-12\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 09\-18\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 09\-05\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 06\-24\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 05\-28\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 04\-29\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 01\-22\-2019 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 06\-12\-2018 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 05\-02\-2018 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 03\-19\-2018 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 01\-24\-2018 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 01\-01\-2018 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 12\-07\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 11\-13\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 09\-05\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 07\-25\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 07\-24\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 06\-20\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 
| 05\-18\-2017 | Windows |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/base-image-version-history.html)  | 