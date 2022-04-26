# Fleets and Stacks<a name="managing-stacks-fleets"></a>

With Amazon AppStream 2\.0, you create fleet instances and stacks as part of the process of streaming applications\. A fleet consists of streaming instances that run the image that you specify\. A stack consists of an associated fleet, user access policies, and storage configurations\.

**Topics**
+ [Fleet Type](#fleet-types)
+ [Session Context](#managing-stacks-fleets-session-context)
+ [Fleet Types](fleet-type.md)
+ [Instance Families](instance-types.md)
+ [Create a Fleet and Stack](set-up-stacks-fleets.md)
+ [Customize a Fleet](customize-fleets.md)
+ [Update a Fleet](update-fleets-new-image.md)
+ [Fleet Auto Scaling](autoscaling.md)
+ [Create and Manage App Blocks and Applications](apps-and-app-blocks.md)

## Fleet Type<a name="fleet-types"></a>

The fleet type allows you to decide when your instances run and how you pay for them\. When your instances runs determines how quickly your users application will launch when it is selected\. You specify the fleet type when you create a fleet, and can't change the fleet type after it is created\.

The available fleet types are:

**Always\-On**  
Streaming instances run continuously, even when no users are streaming applications and desktops\.

**On\-Demand**  
Streaming instances run only when users are streaming applications and desktops\. Streaming instances not yet assigned to users are in a stopped state\.

**Elastic**  
The pool of streaming instances is managed by AppStream 2\.0\. When your users select their application or desktop to launch, they will start streaming after the app block has been downloaded and mounted to a streaming instance\. For more information about creating app blocks for your Elastic fleets, see [Create and Manage App Blocks and Applications for Elastic Fleets](apps-and-app-blocks.md)\.

Use an Always\-On fleet to provide your users with instant access to their applications\. Use an On\-Demand fleet to optimize your streaming charges and provide your users with access to their applications after a 1\-2 minute wait\. For more information, see [Amazon AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

## Session Context<a name="managing-stacks-fleets-session-context"></a>

You can pass parameters to your streaming application by using either of the following methods:
+ Specify session content in the CreateStreamingURL AppStream 2\.0 API operation\. For more information, see [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html)\.
+ Specify the session context as a SAML assertion in your SAML 2\.0 identity provider's authentication response\. For more information, see [Step 5: Create Assertions for the SAML Authentication Response](external-identity-providers-setting-up-saml.md#external-identity-providers-create-assertions)\.

If your image uses a version of the AppStream 2\.0 agent that was released on or after October 30, 2018, the session context is stored within the image as a Windows or Linux environment variable\. For information about specific environment variables, see "User and Instance Metadata for AppStream 2\.0 Fleets" in [Customize an AppStream 2\.0 Fleet to Optimize Your Users' Application Streaming Experience ](customize-fleets.md)\. 

**Note**  
The session context parameter is visible to the user in the AppStream 2\.0 streaming URL\. We strongly recommend that you never put confidential or sensitive information in the session context parameter\. Because it is possible for users to modify the streaming URL, we recommend performing additional validation to determine that the session context is valid for the end user\. For example, you can compare the session context with other session information, such as user and instance metadata for AppStream 2\.0 fleets\.   
AppStream 2\.0 does not perform validation on the session context parameter\. 

### Using Session Context to Pass Parameters to a Streaming Application<a name="managing-stacks-fleets-parameters"></a>

In the following steps, you'll use session context to start a web browser and automatically open a specific website\. For instances running Windows, you'll use Firefox\. For instances running Linux, you'll use Chromium\.

**To use session context to launch a website**

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder to use, verify that it is in the **Running** state, and choose **Connect**\. 

1. Log in to the image builder by choosing **Administrator** on the **Local User** tab\.

1. Create a child folder of `C:\`\. For this example, use `C:\Scripts`\.

1. Create a Windows batch file in the new folder\. For this example, create `C:\Scripts\session-context-test.bat` and add a script that launches Firefox with the URL from the session context\.

   Use the following script:

   ```
   CD "C:\Program Files (x86)\Mozilla Firefox"
   Start firefox.exe %APPSTREAM_SESSION_CONTEXT%
   ```

1. In Image Assistant, add `session-context-test.bat` and change the name to **Firefox**\.

   You do not need to add Firefox\. This step requires that you add only the batch file\.

1. Create an image, fleet, and stack\. For this example, use a fleet name of **session\-context\-test\-fleet** and a stack name of **session\-context\-test\-stack**\.

1. After the fleet is running, you can call [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) with the `session-context` parameter, as shown in this example\.

   ```
   aws appstream create-streaming-url --stack-name session-context-test-stack \ 
   --fleet-name session-context-test-fleet \
   --user-id username –-validity 10000 \
   --application-id firefox --session-context "www.amazon.com"
   ```

1. Open the streaming URL in a browser\. The script file launches Firefox and loads `http://www.amazon.com`\.

Similarly, you can perform the following steps to pass parameters to your Linux streaming application\.

**To pass parameters to your Linux streaming application**

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder to use, verify that it is in the **Running** state, and choose **Connect**\. 

1. Log in to the image builder by default as **ImageBuilderAdmin**\.

1. Create a script file \(for example, launch\-chromium\.sh\) by running the following command:

   sudo vim /usr/bin/launch\-chromium\.sh

1. Write the script and set executable permissions, such as the following:
**Note**  
\#\!/bin/bash and source /etc/profile are always required in the script\.

   ```
   #!/bin/bash
   source /etc/profile
   /usr/bin/chromium-browser $APPSTREAM_SESSION_CONTEXT
   ```

1. Use the Image Assistant CLI to add launch\-chromium\.sh:

   ```
   sudo AppStreamImageAssistant add-application \ 
   --name chromium \
   --absolute-app-path /usr/bin/launch-chromium.sh
   ```

1. Create an image, fleet, and stack\. For this example, use a fleet name of **session\-context\-test\-fleet** and a stack name of **session\-context\-test\-stack**\.

1. After the fleet is running, you can call [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) with the `session-context` parameter, as shown in this example\.

   ```
   aws appstream create-streaming-url --stack-name session-context-test-stack \ 
   --fleet-name session-context-test-fleet \
   --user-id username \
   --application-id chromium --session-context "www.amazon.com"
   ```

1. Open the streaming URL in a browser\. The batch file launches Chromium and loads `http://www.amazon.com`\.