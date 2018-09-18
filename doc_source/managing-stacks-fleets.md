# Amazon AppStream 2\.0 Fleets and Stacks<a name="managing-stacks-fleets"></a>

With Amazon AppStream 2\.0, you create stacks and fleets as part of the process of streaming applications\. A fleet consists of streaming instances that run the image that you specify\. A stack consists of an associated fleet, user access policies, and storage configurations\.

**Topics**
+ [Fleet Type](#fleet-types)
+ [Session Context](#managing-stacks-fleets-parameters)
+ [Instance Families](instance-types.md)
+ [Create Fleets and Stacks](set-up-stacks-fleets.md)
+ [Customize Fleets](customize-fleets.md)
+ [Fleet Auto Scaling](autoscaling.md)

## Fleet Type<a name="fleet-types"></a>

The fleet type determines when your instances run and how you pay for them\. You can specify a fleet type when you create a fleet\. You cannot change the fleet type after you create the fleet\.

The following are the possible fleet types:

Always\-On  
Instances run all the time, even when no users are streaming applications\.

On\-Demand  
Instances run only when users are streaming applications\. Idle instances that are available for streaming are in a stopped state\.

Use an Always\-On fleet to provide your users with instant access to their applications\. Use an On\-Demand fleet to optimize your streaming charges and provide your users with access to their applications after a 1\-2 minute wait\. For more information, see [Amazon AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

To create an On\-Demand fleet, you must use a base image starting with 09\-05\-2017\.

## Session Context<a name="managing-stacks-fleets-parameters"></a>

You can pass parameters to your streaming application using *session context*\. The format is a string with parameters separated by commas\. Session context is supported using the AWS CLI and the AWS SDKs, but is not supported using the AWS Management Console\.

Starting with the images released on 09\-05\-2017, the parameters are passed using the `AppStream_Session_Context` environment variable\. This environment variable is accessible only through \.NET, and we provide an executable file, `SessionContextRetriever.exe`, that you can use to access it\. With images released prior to 09\-05\-2017, parameters are passed to the application\.

The following example uses session context to launch a specific website using Google Chrome\.

**To use session context to launch a website**

1. Connect to your image builder in Administrator mode\. For this example, install Google Chrome on the image builder\.

1. Create a child folder of `C:\`\. For this example, use `C:\Scripts`\.

1. For images released on or after 09\-05\-2017, [download SessionContextRetriever\.exe](https://dsfpe42xwhi2e.cloudfront.net/SessionContextRetriever.exe)\.

1. Create a Windows batch file in the new folder\. For this example, create `C:\Scripts\session-context-test.bat` and add a script that launches Chrome with the URL from session context, and then waits for keyboard input\.

   For images released on or after 09\-05\-2017, use the following script:

   ```
   for /f "tokens=* USEBACKQ" %%f in (`SessionContextRetriever.exe`) do (
   set var=%%f
   )
   chrome.exe %var%
   pause
   ```

   For images released prior to 09\-05\-2017, use the following scripts:

   ```
   chrome.exe %1
   pause
   ```

1. In Image Assistant, add `session-context-test.bat` and change the working directory to `C:\Program Files (x86)\Google\Chrome\Application`\.

1. Create an image, fleet, and stack\. For this example, use a fleet name of **session\-context\-test\-fleet** and a stack name of **session\-context\-test\-stack**\.

1. After the fleet is running, you can call [create\-streaming\-url](http://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) with the `session-context` parameter, as shown in this example\.

   ```
   aws appstream create-streaming-url --stack-name session-context-test-stack \ 
   --fleet-name session-context-test-fleet \
   --user-id username --validity 10000 \
   --application-id chrome --session-context "www.google.com"
   ```

1. Open the streaming URL in a browser\. The batch file launches Chrome and loads `http://www.google.com`\.
