# Fleets and Stacks<a name="managing-stacks-fleets"></a>

With Amazon AppStream 2\.0, you create fleet instances and stacks as part of the process of streaming applications\. A fleet consists of streaming instances that run the image that you specify\. A stack consists of an associated fleet, user access policies, and storage configurations\.

**Topics**
+ [Fleet Type](#fleet-types)
+ [Session Context](#managing-stacks-fleets-session-context)
+ [Instance Families](instance-types.md)
+ [Create a Fleet and Stack](set-up-stacks-fleets.md)
+ [Customize a Fleet](customize-fleets.md)
+ [Update a Fleet with a New Image](update-fleets-new-image.md)
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

## Session Context<a name="managing-stacks-fleets-session-context"></a>

You can pass parameters to your streaming application by using the [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) AppStream 2\.0 API operation\. If your image uses a version of the AppStream 2\.0 agent that was released on or after October 30, 2018, the session context can be accessed within the image as a Windows environment variable\. For information about specific environment variables, see "User and Instance Metadata for AppStream 2\.0 Fleets" in [Customize an AppStream 2\.0 Fleet to Optimize Your Users' Application Streaming Experience ](customize-fleets.md)\. 

### Using Session Context to Pass Parameters to a Streaming Application<a name="managing-stacks-fleets-parameters"></a>

Perform the following steps to pass parameters to your streaming application\. The example uses session context to launch a specific website using Firefox\.

**To use session context to launch a website**

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder to use, verify that it is in the **Running** state, and choose **Connect**\. 

1. Log in to the image builder by choosing **Administrator** on the **Local User** tab\.

1. Create a child folder of `C:\`\. For this example, use `C:\Scripts`\.

1. Create a Windows batch file in the new folder\. For this example, create `C:\Scripts\session-context-test.bat` and add a script that launches Firefox with the URL from the session context\.

   Do one of the following, based on the version of the AppStream 2\.0 agent that your image uses \(when the AppStream 2\.0 agent was released\): 
   + On or after October 30, 2018 — Use the following script, then proceed to step 6\.

     ```
     CD "C:\Program Files (x86)\Mozilla Firefox"
     Start firefox.exe %APPSTREAM_SESSION_CONTEXT%
     ```
   + On or after September 5, 2017 and before October 30, 2018 — Follow the instructions in [Using Session Context with AppStream 2\.0 Agent Versions Released On or After September 5, 2017 and Before October 30, 2018](#managing-stacks-fleets-parameters-older-agent-versions), then proceed to step 6\.
   + Before September 5, 2017 — Follow the instructions in [Using Session Context with AppStream 2\.0 Agent Versions Released Before September 5, 2017](#managing-stacks-fleets-parameters-agent-versions-before-09-05-2017), then proceed to step 6\.

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

1. Open the streaming URL in a browser\. The batch file launches Firefox and loads `http://www.amazon.com`\.

### Using Session Context with AppStream 2\.0 Agent Versions Released On or After September 5, 2017 and Before October 30, 2018<a name="managing-stacks-fleets-parameters-older-agent-versions"></a>

If your image uses a version of the AppStream 2\.0 agent version that was released on or after September 5, 2017 and before October 30, 2018, the APPSTREAM\_SESSION\_CONTEXT variable is accessible only through \.NET\. To access the environment variable, download the `SessionContextRetriever.exe` file from [https://dsfpe42xwhi2e.cloudfront.net/SessionContextRetriever.exe](https://dsfpe42xwhi2e.cloudfront.net/SessionContextRetriever.exe) and copy this \.exe file to C:\\Scripts\. Then, create the following script as part of completing step 5 in [Using Session Context to Pass Parameters to a Streaming Application](#managing-stacks-fleets-parameters)\.

```
for /f "tokens=*"
%%f in ('C:\Scripts\SessionContextRetriever.exe')
do (set var=%%f)
CD "C:\Program Files (x86)\Mozilla Firefox"
start firefox.exe %var%
```

When you're done, proceed to step 6\.

### Using Session Context with AppStream 2\.0 Agent Versions Released Before September 5, 2017<a name="managing-stacks-fleets-parameters-agent-versions-before-09-05-2017"></a>

If your image uses a version of the AppStream 2\.0 agent that was released before September 5, 2017, use the following script for step 5 in [Using Session Context to Pass Parameters to a Streaming Application](#managing-stacks-fleets-parameters), then proceed to step 6\.

```
CD "C:\Program Files (x86)\Mozilla Firefox"
start firefox.exe %1
```

Parameters are passed to the streaming application\. 