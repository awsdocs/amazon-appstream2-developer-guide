# Manage AppStream 2\.0 Agent Versions<a name="base-images-agent"></a>

The AppStream 2\.0 agent is software that runs on your streaming instances and enables users to stream applications\. When you create a new image, the **Always use latest agent version** option is selected by default\. When this option is selected, new image builders or fleet instances that are launched from your image always use the latest AppStream 2\.0 agent version\. We recommend that you leave this option selected\. In some cases, however, you may want to control agent updates to ensure compatibility\.

The following procedures describe how to manage AppStream 2\.0 agent versions\.

**Topics**
+ [Create an Image That Always Uses the Latest Version of the AppStream 2\.0 Agent](#create-image-that-always-uses-latest-agent)
+ [Create an Image That Uses a Specific Version of the AppStream 2\.0 Agent](#create-image-that-uses-specific-agent)
+ [Create an Image That Uses a Newer Version of the AppStream 2\.0 Agent](#create-image-that-uses-newer-agent)

## Create an Image That Always Uses the Latest Version of the AppStream 2\.0 Agent<a name="create-image-that-always-uses-latest-agent"></a>

When your images are configured to always use the latest AppStream 2\.0 agent version, your streaming instances are automatically updated with the latest features, performance improvements, and security updates that are available from AWS\.

**To create an image that always uses the latest version of the AppStream 2\.0 agent**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Do either of the following: 
   + If you have an image builder that you want to use to create the image, start the image builder and then connect to it\. If the image builder is not running the latest version of the AppStream 2\.0 agent, you are prompted to choose whether to start the image builder with the latest agent\. Make sure that this option is selected, choose **Start**, and then connect to the image builder\.
   + If you do not have an image builder that you want to use to create the image, launch a new image builder\. In **Step 1: Choose Image**, choose an AWS base image or a custom image\. In **Step 2: Configure Image Builder**, if the image that you choose is not running the latest version of the AppStream 2\.0 agent, the **AppStream 2\.0** section displays\. In the **Agent version** list, select the latest agent version\. Complete the remaining steps to create the image builder, and then connect to it\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

1. On the image builder desktop, open Image Assistant and follow the steps to create your new image\. For the **Configure Image** step, make sure that **Always use the latest agent version** is selected\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\. 

   If you decide later to not always use the latest version of the AppStream 2\.0 agent, you must create a new image and clear that option\.

1. Create a new fleet or modify an existing one\. When you configure the fleet, select the new image that you created\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.

1. Create a new stack or modify an existing one and associate it with your fleet\.

## Create an Image That Uses a Specific Version of the AppStream 2\.0 Agent<a name="create-image-that-uses-specific-agent"></a>

You may want to control AppStream 2\.0 agent updates rather than always using the latest version so that you can test for compatibility first\. To ensure that the version of the AppStream 2\.0 agent you use is compatible with your streaming applications, you can create an image that uses a specific version of the agent software\. Then perform your qualification tests in a separate fleet before deploying to your production fleet\. 

When you create the image, make sure that the **Always use latest agent version** option is not selected\. Doing so pins your image to the version of the AppStream 2\.0 agent that you selected when you launched the image builder, rather than always using the latest version\. After you finish your qualification tests, you can update your production fleet with the image\.

**To create an image that uses a specific version of the AppStream 2\.0 agent**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Do either of the following: 
   + If you have an image builder that you want to use to create the image, start the image builder and then connect to it\.
   + If you do not have an image builder that you want to use to create the image, launch a new image builder\. In **Step 1: Choose Image**, choose an AWS base image or a custom image\. In **Step 2: Configure Image Builder**, if the image that you choose is not running the latest version of the AppStream 2\.0 agent, the **AppStream 2\.0** section displays\. In the **Agent version** list, do not select the latest agent version\. Complete the remaining steps to create the image builder, and then connect to it\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

1. On the image builder desktop, open Image Assistant and follow the steps to create your new image\. For the **Configure Image** step in Image Assistant, make sure that **Always use the latest agent version** is not selected\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   If you decide later to always use the latest version of the AppStream 2\.0 agent, you must create a new image and select that option\.

1. Create a new fleet or modify an existing one\. When you configure the fleet, select the new image that you created\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.

1. Create a new stack or modify an existing one and associate it with your fleet\.

1. Connect to your fleet and test your applications for compatibility\.

## Create an Image That Uses a Newer Version of the AppStream 2\.0 Agent<a name="create-image-that-uses-newer-agent"></a>

If you pin your image to a specific AppStream 2\.0 agent version, you must update to a newer version by creating a new image\. This approach lets you test each agent update for compatibility first, and then update your fleet incrementally\. 

When you create the image, make sure that the **Always use latest agent version** option is not selected\. After you create your image, perform your qualification tests in a separate fleet before deploying to your production fleet\. After you finish your qualification tests, you can update your production fleet with the image\.

**To create an image that uses a newer version of the AppStream 2\.0 agent**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Do either of the following: 
   + If you have an image builder that you want to use to create the image, start the image builder and then connect to it\. If the image builder is not running the latest version of the AppStream 2\.0 agent, you are prompted to choose whether to start the image builder with the latest agent\. Make sure that this option is selected, choose **Start**, and then connect to the image builder\.
   + If you do not have an image builder that you want to use to create the image, launch a new image builder\. In **Step 1: Choose Image**, choose an AWS base image or a custom image\. In **Step 2: Configure Image Builder**, if the image that you choose is not running the latest version of the AppStream 2\.0 agent, the **AppStream 2\.0** section displays\. In the **Agent version** list, select the latest agent version\. Complete the remaining steps to create the image builder, and then connect to it\. For more information, see [Launch an Image Builder to Install and Configure Streaming Applications](tutorial-image-builder-create.md)\.

1. On the image builder desktop, open Image Assistant and follow the steps to create your new image\. For the **Configure Image** step in Image Assistant, make sure that **Always use the latest agent version** is not selected\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

   If you decide later to always use the latest version of the AppStream 2\.0 agent, you must create a new image and select that option\.

1. Create a new fleet or modify an existing one\. When you configure the fleet, select the new image that you created\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.

1. Create a new stack or modify an existing one and associate it with your fleet\.

1. Connect to your fleet and test your applications for compatibility\.