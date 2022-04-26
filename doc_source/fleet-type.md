# AppStream 2\.0 Fleet Types<a name="fleet-type"></a>

The fleet type determines when your instances run and how you pay for them\. You can specify a fleet type when you create a fleet\. You cannot change the fleet type after you create the fleet\.

The following are the possible fleet types:

Always\-On  
Streaming instances run all the time, even when no users are streaming applications and desktops\. Streaming instances must be provisioned before a user is able to stream\. The number of streaming instances provisioned is managed through auto scaling rules\.  
When your users choose their application or desktop, they will start streaming instantly\. You are charged the running instance fee for all streaming instances, even when no users are streaming\.

On\-Demand  
Streaming instances run only when users are streaming applications and desktops\. Streaming instances not yet assigned to users are in a stopped state\. Streaming instances must be provisioned before a user is able to stream\. The number of streaming instances provisioned is managed through auto scaling rules\.  
When your users choose their application or desktop, they will start streaming after a 1\-2 minute wait\. You are charged a lower stopped instance fee for streaming instances that are not yet assigned to users, and the running instance fee for streaming instances that are assigned to users\.

Elastic  
The pool of streaming instances is managed by AppStream 2\.0\. When your users select their application or desktop to launch, they will start streaming after the app block has been downloaded and mounted to a streaming instance\. For more information about creating app blocks for your Elastic fleets, see [Create and Manage App Blocks and Applications for Elastic Fleets](apps-and-app-blocks.md)\.  
You are charged the running instance fee for Elastic fleet streaming instances only for the duration of the streaming session, in seconds, with a minimum of 15 minutes\.

For more information about how fleet types are charged, see [Amazon AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

## Always\-On and On\-Demand Fleets<a name="always-demand-fleet"></a>

Always\-On and On\-Demand fleets represent a pool of streaming instances that you manage the capacity of using auto scaling policies\. Your users use the streaming instances to stream their applications and desktops\. With an Always\-On fleet, your user’s application launches nearly instantly, and you pay the running instance rate per instance even when a user isn’t streaming\. With an On\-Demand fleet, your user’s application launches after a 1\-2 minute wait as the streaming instance is started, and you pay a lower cost stopped instance fee for instances not in use, and the running instance fee for instances that are in use\.

Applications for Always\-On and On\-Demand fleet instances are delivered through AppStream 2\.0 images that are created by image builders\. You can learn more about how to create an image builder, install your applications, and create an image by reading [Images](managing-images.md)\.

Always\-On and On\-Demand fleet streaming instances must be provisioned and unassigned to an existing user before a user can stream\. You can use fixed or dynamic fleet autoscaling policies to manage the number of instances in your fleet, ensuring that you have sufficient available capacity to meet your user needs while controlling costs\. You can learn more about scaling your fleets by reading [Fleet Auto Scaling for Amazon AppStream 2\.0](autoscaling.md)\.

## Elastic Fleets<a name="elastic-fleet"></a>

Elastic fleets represent a pool of streaming instances that AppStream 2\.0 manages\. You do not need to predict concurrency, or create and manage any auto scaling policies for your users to stream their applications and desktops\. When your user requests a streaming instance, a streaming instance is assigned from the pool, and made available to them after configuration completes\. 

Elastic fleets rely on applications that are stored on app blocks\. When a user chooses an application from the catalog, the app block is downloaded to the instance, mounted, and then the application launches\.

AWS manages the streaming instance provisioning and availability with an Elastic fleet\. You need to configure the maximum concurrency you expect when creating and updating the fleet, and ensure that you have sufficient streaming instance limits to meet your user demand\.

For more information about creating app blocks for your Elastic fleets, see [Create and Manage App Blocks and Applications for Elastic Fleets](apps-and-app-blocks.md)\.