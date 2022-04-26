# Install AMD Driver on Graphics Design Instances<a name="AMD-driver"></a>

If you need to update the AMD driver on your Windows Image Builder that is using a Graphics Design instance, you can either use the latest AppStream 2\.0 Graphics Design base images, or download the AMD driver and install it on your Image Builder\. If you need to update the AMD driver for an existing image of the Graphics Design instance family, you can use managed AppStream 2\.0 image updates\. For more information, see [Update an Image by Using Managed AppStream 2\.0 Image Updates](administer-images.md#keep-image-updated-managed-image-updates)\.

The AMD driver download is available to AWS customers only\. By downloading, you agree to use the downloaded software only to build images for use with AppStream 2\.0 Graphics Design instances using AMD FirePro S7150x2 Server GPU hardware\. Upon installation of the software, you are bound by the terms of the [AMD Software End User License Agreements](https://www.amd.com/en/support/eula)\.

The latest AMD driver version for Graphics Design instances is version 24\.20\.13028\.5012\.

Before you begin, make sure that you meet the following prerequisites:
+ Configure default credentials for the AWS Tools for Windows PowerShell on your Windows instance\. For more information, see [Getting Started with the AWS Tools for Windows PowerShell](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-getting-started.html)\.
+ IAM users must have the permissions granted by the **AmazonS3ReadOnlyAccess** policy\.

**To install the AMD driver on your Image Builder**

1. Connect to your Windows Image Builder instance and open a PowerShell window as an Administrator\.

1. Download the drivers from Amazon S3 to your desktop using the following PowerShell commands: 

   ```
   $Bucket = "appstream2-driver-patches"
   $LocalPath = "$home\Desktop\AMD"
   $Objects = Get-S3Object -BucketName $Bucket -Region us-east-1  
   foreach ($Object in $Objects) {
      $LocalFileName = $Object.Key
      if ($LocalFileName -ne '' -and $Object.Size -ne 0) {
        $LocalFilePath = Join-Path $LocalPath $LocalFileName
        Copy-S3Object -BucketName $Bucket -Key $Object.Key -LocalFile $LocalFilePath -Region us-east-1 
      }
    }
   ```

1. Unzip the downloaded driver file and run the installer using the following PowerShell commands:

   ```
   Expand-Archive $LocalFilePath -DestinationPath $home\Desktop -Verbose
   $Driverdir = Get-ChildItem $home\Desktop\ -Directory -Filter "*210426a-366782C*"
   Write-Host $Driverdir
   pnputil /add-driver $home\Desktop\$Driverdir\Packages\Drivers\Display\WT6A_INF\*inf /install
   ```

1. Follow the instructions to install the driver and reboot your instance as required\.

1. To verify that the GPU is working properly, check **Device Manager**\. You should see **AMD MxGPU** listed as a display adapter, with the latest driver version\.