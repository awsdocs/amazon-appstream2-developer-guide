# Instance Metadata for AppStream 2\.0 Image Builders<a name="user-instance-metadata-image-builders"></a>

AppStream 2\.0 image builder instances have instance metadata available through Windows environment variables\. You can use the following environment variables in your applications and scripts to modify your environment based on the image builder instance details\.


| Environment Variable | Context | Description | 
| --- | --- | --- | 
| AppStream\_Image\_Arn | Machine | The ARN of the image that was used to create the streaming instance\. | 
| AppStream\_Instance\_Type | Machine | The instance type of the streaming instance\. For example, stream\.standard\.medium\. | 
| AppStream\_Resource\_Type | Machine | The type of AppStream 2\.0 resource\. The value is either fleet or imagebuilder\. | 
| AppStream\_Resource\_Name | Machine | The name of the image builder\. | 