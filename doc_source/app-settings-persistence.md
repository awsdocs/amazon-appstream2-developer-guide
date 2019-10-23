# Enable Application Settings Persistence for Your AppStream 2\.0 Users<a name="app-settings-persistence"></a>

AppStream 2\.0 supports persistent application settings\. This means that your users' application customizations and Windows settings are automatically saved after each streaming session and applied during the next session\. Examples of persistent application settings that your users can configure include, but are not limited to, browser favorites, settings, webpage sessions, application connection profiles, plugins, and UI customizations\. These settings are saved to an Amazon Simple Storage Service \(Amazon S3\) bucket in your account, within the AWS Region in which application settings persistence is enabled\. They are available in each AppStream 2\.0 streaming session\. 

**Note**  
Standard Amazon S3 charges may apply to data that is stored in your S3 bucket\. For more information, see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)\.

**Topics**
+ [How Application Settings Persistence Works](how-it-works-app-settings-persistence.md)
+ [Enabling Application Settings Persistence](enabling-app-settings-persistence.md)
+ [Administer the VHDs for Your Users' Application Settings](administer-app-settings-vhds.md)