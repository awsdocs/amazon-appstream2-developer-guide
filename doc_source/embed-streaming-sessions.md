# Embed AppStream 2\.0 Streaming Sessions<a name="embed-streaming-sessions"></a>

You can create a dynamic, interactive, and customized experience for your users by embedding an AppStream 2\.0 streaming session within your website\. Embedded AppStream 2\.0 streaming sessions let your users interact with 3D models, maps, and datasets directly from your website\. For example, users can view training instructions or educational materials alongside their AppStream 2\.0 streaming session\. 

**Topics**
+ [Prerequisites](#embed-streaming-sessions-prerequisites)
+ [Recommendations and Usage Considerations](#embed-streaming-sessions-recommendations-considerations)
+ [Step 1: Specify a Host Domain for Embedded AppStream 2\.0 Streaming Sessions](#specify-host-domain-embedded-streaming-sessions)
+ [Step 2: Create a Streaming URL for User Authentication](#create-streaming-url-user-authentication)
+ [Step 3: Download the Embedded AppStream 2\.0 Files](#download-embed-files)
+ [Step 4\. Configure Your Website for Integration with AppStream 2\.0](#configure-website-for-integration)
+ [Constants, Functions, and Events for Embedded AppStream 2\.0 Streaming Sessions](#constants-functions-events-embedded-sessions)

## Prerequisites<a name="embed-streaming-sessions-prerequisites"></a>

To embed an AppStream 2\.0 streaming session in a website, you must have the following:
+ A configured AppStream 2\.0 environment that includes an AppStream 2\.0 image, fleet, and stack\. For information about how to create these resources, see the following topics in the *AppStream 2\.0 Administration Guide*: 
  +  [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md) or [Create Your AppStream 2\.0 Image Programmatically by Using the Image Assistant CLI Operations](programmatically-create-image.md)
  + [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)
  + [Create a Stack](set-up-stacks-fleets.md#set-up-stacks-fleets-install)
+ A streaming URL for user authentication\. SAML 2\.0 and AppStream 2\.0 user pools are currently not supported as authentication methods for embedded AppStream 2\.0 streaming sessions\.
+ Optionally, you can use custom domains for embedded AppStream 2\.0 streaming sessions\. You can use custom domains so that your own company URL displays for users rather than an AppStream 2\.0 URL\. Custom domains are required if your users have web browsers that block third\-party cookies\.
**Note**  
You can configure custom domains by using Amazon CloudFront\. For information, see [Using Custom Domains with AppStream 2\.0](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-custom-domains-with-amazon-appstream-2-0/)\.

  When you use a custom domain, you must:
  + Create a streaming URL that uses the same domain\. 
  + Add **appstream\-custom\-url\-domain** to the header of the webpage that will host the embedded AppStream 2\.0 streaming sessions\. For the header value, use the domain that your reverse proxy displays to users\. For more information, see [Configuration Requirements for Using Custom Domains](#configuration-requirements-custom-domains)\.

## Recommendations and Usage Considerations<a name="embed-streaming-sessions-recommendations-considerations"></a>

Consider the following recommendations and usage notes for embedded AppStream 2\.0 streaming sessions\.
+ To maintain maximum control over the embedded AppStream 2\.0 streaming experience for your users, we recommend that you configure short\-lived streaming URLs that last approximately 5 seconds\. Any user can inspect the contents of a webpage and view its source\. This includes the document object model \(DOM\) and the src \(source\) URL of the iframe\. If the URL is still valid when a user copies it, that user can paste the URL in a separate browser tab and stream the session with the standard AppStream 2\.0 portal user interface, without the embed options\.
+ Concurrent sessions are not supported when custom domains are used for embedded AppStream 2\.0 streaming sessions\. Concurrent sessions occur when users start two embedded AppStream 2\.0 streaming sessions either on the same webpage or across two different browser tabs\. 

## Step 1: Specify a Host Domain for Embedded AppStream 2\.0 Streaming Sessions<a name="specify-host-domain-embedded-streaming-sessions"></a>

To embed an AppStream 2\.0 streaming session in a webpage, first update your stack to specify the domain to host the embedded streaming session\. This a security measure to ensure that only authorized website domains can embed AppStream 2\.0 streaming sessions\. AppStream 2\.0 adds the domain or domains that you specify to the **Content\-Security\-Policy** \(CSP\) header\. For more information, see [Content Security Policy \(CSP\)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) in the Mozilla [MDN Web Docs](https://developer.mozilla.org/en-US/) documentation\.

To update your stack to specify the domain to host the embedded streaming session, use any of the following methods:
+ The AppStream 2\.0 console
+ The `EmbedHostDomains` API action 
+ The `embed-host-domains` AWS command line interface \(AWS CLI\) command

To specify a host domain by using the AppStream 2\.0 console, perform the following steps\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Stacks**, and select the stack that you want\.

1. Choose **Edit**\.

1. Expand **Embed AppStream 2\.0 \(Optional\)**\.

1. In **Host Domains**, specify a valid domain\. For example: **training\.example\.com**\.
**Note**  
Embedded streaming sessions are only supported over HTTPS \[TCP port 443\]\.

1. Choose **Update**\.

## Step 2: Create a Streaming URL for User Authentication<a name="create-streaming-url-user-authentication"></a>

You must create a streaming URL to authenticate users for embedded AppStream 2\.0 streaming sessions\. SAML 2\.0 and user pools are currently not supported for embedded streaming sessions\. To create a streaming URL, use one of the following methods:
+ AppStream 2\.0 console
+ The [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action 
+ The [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream;create-streaming-url.html) AWS CLI command

### Configuration Requirements for Using Custom Domains<a name="configuration-requirements-custom-domains"></a>

Whether you use custom domains to apply your company branding or to ensure that embedded AppStream 2\.0 streaming sessions work with browsers that block third\-party cookies, the configuration requirements are the same\.

For web browsers that block third\-party cookies, custom domains are required\. AppStream 2\.0 uses browser cookies to authenticate streaming sessions and lets users reconnect to an active session without being prompted to provide their user name and password every time\. By default, AppStream 2\.0 streaming URLs include **appstream\.com** as the domain\. When you embed a streaming session within your website, **appstream\.com** is treated as a third\-party domain\. As a result, streaming sessions may be blocked when modern browsers are used that block third\-party cookies by default\.

To avoid embedded AppStream 2\.0 streaming sessions from being blocked in this scenario, follow these steps:

1. Specify a custom domain to host your embedded AppStream 2\.0 streaming sessions\.

   When you configure your custom domain, make sure that the domain is a subdomain of the webpage in which you plan to embed AppStream 2\.0\. For example, if you update your stack to specify **training\.example\.com** as the host domain, you can create a subdomain called **content\.training\.example\.com** for your embedded streaming sessions\.

1. Create a streaming URL for embedded AppStream 2\.0 streaming sessions that uses the same custom subdomain\. To create the streaming URL, use the [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action or the [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream;create-streaming-url.html) AWS CLI command\. You cannot use the AppStream 2\.0 console to create a streaming URL in this scenario\.

   To create a streaming URL for embedded AppStream 2\.0 streaming sessions, in the URL, replace **appstream2\.***region***\.aws\.amazon\.com** with your own domain\. 

   By default, AppStream 2\.0 streaming URLs are formatted as follows:

   ```
   https://appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode
   ```

   If your subdomain is **content\.training\.example\.com**, your new streaming URL follows this format:

   ```
   https://content.training.example.com/authenticate?parameters=authenticationcode
   ```
**Note**  
When you create a custom domain, you can use the domain for embedded AppStream 2\.0 streaming sessions only in the AWS Region for which it was configured\. If you plan to support custom domains in multiple Regions, create a custom domain for each applicable Region\. Also, embedded streaming sessions are only supported over HTTPS \[TCP port 443\]\.

1. Add **appstream\-custom\-url\-domain** to the header of the webpage that will host the embedded streaming sessions\. For the header value, use the domain that your reverse proxy displays to users\. For example:

   ```
   Header name: appstream-custom-url-domain
   Header value: training.example.com
   ```

   Setting a custom domain and creating a streaming URL that specifies the same domain lets the cookies be saved as first\-party cookies\. For information about how to configure custom domains by using Amazon CloudFront, see [Using Custom Domains with AppStream 2\.0](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-custom-domains-with-amazon-appstream-2-0/)\.

## Step 3: Download the Embedded AppStream 2\.0 Files<a name="download-embed-files"></a>

To host embedded AppStream 2\.0 streaming sessions, you must download and configure the provided AppStream 2\.0 API JavaScript file\.

1. On the [Embedding AppStream 2\.0 in Your Website](https://clients.amazonappstream.com/embed.html) webpage, choose the link in step 1 to download the AppStream 2\.0 Embed Kit \.zip file, **appstream\_embed\_<version>\.zip**\.

1. Navigate to the location where you downloaded the \.zip file, and extract the contents of the file\.

1. The extracted contents of the file comprise one folder, **appstream\-embed**\. In addition to the **COPYRIGHT\.txt** and **THIRD\_PARTY\_NOTICES\.txt **file, this folder contains the following two files:
   + **appstream\-embed\.js** — Provides the embedded AppStream 2\.0 API\. This JavaScript file includes the functions and API actions for configuring and controlling your embedded AppStream 2\.0 streaming session\.
   + **embed\-sample\.html** — Describes how to use the embedded AppStream 2\.0 API to initialize a streaming session, call functions, and listen for events\. This sample file expands on the information in this topic, to provide an example use case for developers\.

## Step 4\. Configure Your Website for Integration with AppStream 2\.0<a name="configure-website-for-integration"></a>

The following sections provide information about how to configure your webpage to host embedded AppStream 2\.0 streaming sessions\.

**Topics**
+ [Import the appstream\-embed JavaScript File](#import-embed-javascript-file)
+ [Initialize and Configure the `AppStream.Embed` Interface Object](#initialize-configure-embed-interface-object)
+ [Examples for Hiding Items in the AppStream 2\.0 User Interface](#examples-hiding-user-interface-items)

### Import the appstream\-embed JavaScript File<a name="import-embed-javascript-file"></a>

1. On the webpage where you plan to embed the AppStream 2\.0 streaming session, import the **appstream\-embed\.js** file into the webpage by adding the following code:

   ```
   <script type="text/javascript" src="./appstream_embed.js"> </script>
   ```

1. Next, create an empty container div\. The ID of the div that you set is passed into the AppStream 2\.0 embed constructor\. It's then used to inject an iframe for the streaming session\. To create the div, add the following code:

   ```
   <div id="appstream-container"> </div>
   ```

### Initialize and Configure the `AppStream.Embed` Interface Object<a name="initialize-configure-embed-interface-object"></a>

To initialize the `AppStream.Embed` interface object in JavaScript, you must add code that creates an `AppStream.Embed` object with options for the streaming URL and user interface configuration\. These options, and the div ID that you created, are stored in an object called `appstreamOptions`\.

The following example code shows how to initialize the `AppStream.Embed` interface object\.

```
var appstreamOptions = {
     sessionURL: 'https://appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode...',
     userInterfaceConfig:{[AppStream.Embed.Options.HIDDEN_ELEMENTS]:[AppStream.Embed.Elements.TOOLBAR]}
 };
 appstreamEmbed = new AppStream.Embed("appstream-container", appstreamOptions);
```

In the code, replace *sessionURL* and *userInterfaceConfig* with your own values\. 

**Note**  
The value specified for *userInterfaceConfig* hides the entire AppStream 2\.0 toolbar\. This value, which is included as an example, is optional\.

***sessionUrl***  
The streaming URL that you created by using the AppStream 2\.0 console, the [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action, or the [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream;create-streaming-url.html) AWS CLI command\. This parameter is case\-sensitive\.  
**Type**: String  
**Required**: Yes

***userInterfaceConfig***  
The configuration that generates the initial state of the user interface elements\. The configuration is a key\-value pair\.   
The key, `AppStream.Embed.Options.HIDDEN_ELEMENTS`, specifies the user interface objects that are initially hidden when the embedded AppStream 2\.0 streaming session is initialized\. Later, you can return both hidden and visible objects by using the `getInterfaceState` parameter\.  
The value is an array of constants \(toolbar buttons\)\. For a list of constants that you can use, see [Working with `HIDDEN_ELEMENTS`](#constants-hidden-elements)\.  
**Type**: Map \(*key*:*value*\)  
**Required**: No

### Examples for Hiding Items in the AppStream 2\.0 User Interface<a name="examples-hiding-user-interface-items"></a>

The examples in this section show how to hide items in the AppStream 2\.0 user interface from users during their embedded AppStream 2\.0 streaming sessions\.

**Topics**
+ [Example 1: Hide the entire AppStream 2\.0 toolbar](#example-hide-the-entire-tooolbar)
+ [Example 2: Hide a specific button on the AppStream 2\.0 toolbar](#example-hide-a-specific-toolbar-button)
+ [Example 3: Hide multiple buttons on the AppStream 2\.0 toolbar](#example-hide-multiple-toolbar-buttons)

#### Example 1: Hide the entire AppStream 2\.0 toolbar<a name="example-hide-the-entire-tooolbar"></a>

To prevent users from accessing any button on the AppStream 2\.0 toolbar during embedded streaming sessions, use the `AppStream.Embed.Elements.TOOLBAR` constant\. This constant lets you hide all AppStream 2\.0 toolbar buttons\.

```
var appstreamOptions = {
     sessionURL: 'https://appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode...',
     userInterfaceConfig:{[AppStream.Embed.Options.HIDDEN_ELEMENTS]:[AppStream.Embed.Elements.TOOLBAR]}
 };
```

#### Example 2: Hide a specific button on the AppStream 2\.0 toolbar<a name="example-hide-a-specific-toolbar-button"></a>

You can display the AppStream 2\.0 toolbar, while preventing users from accessing a specific toolbar button during embedded streaming sessions\. To do so, specify the constant for the button that you want to hide\. The following code uses the `AppStream.Embed.Elements.FILES_BUTTON` constant to hide the **My Files** button\. This prevents users from accessing persistent storage options during embedded streaming sessions\.

```
var appstreamOptions = {
     sessionURL: 'https://appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode...',
     userInterfaceConfig:{[AppStream.Embed.Options.HIDDEN_ELEMENTS]:[AppStream.Embed.Elements.FILES_BUTTON]}
 };
```

#### Example 3: Hide multiple buttons on the AppStream 2\.0 toolbar<a name="example-hide-multiple-toolbar-buttons"></a>

You can display the AppStream 2\.0 toolbar, while preventing users from accessing more than one toolbar button during embedded streaming sessions\. To do so, specify the constants for the buttons that you want to hide\. The following code uses the `AppStream.Embed.Elements.END_SESSION_BUTTON` and `AppStream.Embed.Elements.FULLSCREEN_BUTTON` constants to hide the **End Session** and **Fullscreen** buttons\. 

**Note**  
Separate each constant with a comma, with no preceding or following space\.

```
var appstreamOptions = {
     sessionURL: 'https://appstream2.region.aws.amazon.com/authenticate?parameters=authenticationcode... (https://appstream2.region.aws.amazon.com/#/)',
     userInterfaceConfig:{[AppStream.Embed.Options.HIDDEN_ELEMENTS]:[AppStream.Embed.Elements.END_SESSION_BUTTON,AppStream.Embed.Elements.FULLSCREEN_BUTTON]}
 };
```

## Constants, Functions, and Events for Embedded AppStream 2\.0 Streaming Sessions<a name="constants-functions-events-embedded-sessions"></a>

The following topics provide reference information for constants, functions, and events that you can use to configure embedded AppStream 2\.0 streaming sessions\.

**Topics**
+ [Working with `HIDDEN_ELEMENTS`](#constants-hidden-elements)
+ [Functions for the `AppStream.Embed` Object](#functions-embed-object)
+ [Events for Embedded AppStream 2\.0 Streaming Sessions](#events-embedded-streaming-sessions)
+ [Examples for Adding Event Listeners and Ending an Embedded AppStream 2\.0 Streaming Session](#examples-add-event-listeners-end-embedded-streaming-session)

The following AppStream 2\.0 user interface elements can be passed into the `HIDDEN_ELEMENTS` configuration option when an embedded AppStream 2\.0 streaming session is initialized\.

### Working with `HIDDEN_ELEMENTS`<a name="constants-hidden-elements"></a>

The following AppStream 2\.0 user interface elements can be passed as constants into the `HIDDEN_ELEMENTS` configuration option when an embedded AppStream 2\.0 streaming session is initialized\. 

```
AppStream.Embed.Elements.TOOLBAR
AppStream.Embed.Elements.FULLSCREEN_BUTTON
AppStream.Embed.Elements.END_SESSION_BUTTON
AppStream.Embed.Elements.TOOLBAR
AppStream.Embed.Elements.CATALOG_BUTTON
AppStream.Embed.Elements.WINDOW_SWITCHER_BUTTON
AppStream.Embed.Elements.FILES_BUTTON
AppStream.Embed.Elements.CLIPBOARD_BUTTON
AppStream.Embed.Elements.COPY_LOCAL_BUTTON
AppStream.Embed.Elements.PASTE_REMOTE_BUTTON
AppStream.Embed.Elements.SETTINGS_BUTTON
AppStream.Embed.Elements.STREAMING_MODE_BUTTON
AppStream.Embed.Elements.SCREEN_RESOLUTION_BUTTON
AppStream.Embed.Elements.REGIONAL_SETTINGS_BUTTON
AppStream.Embed.Elements.FULLSCREEN_BUTTON
AppStream.Embed.Elements.END_SESSION_BUTTON
```

The following three elements can be passed as strings into HIDDEN\_ELEMENTS, rather than as constants\.


| String | Description | 
| --- | --- | 
| 'adminCommandsButton' | When you are connected to an AppStream 2\.0 image builder, the Admin Commands button displays on the top right corner of the session toolbar\. Passing this string into HIDDEN\_ELEMENTS hides the Admin Commands button\. | 
| 'softKeyboardButton' | During AppStream 2\.0 streaming sessions on touch\-enabled devices, users can tap the keyboard icon on the AppStream 2\.0 toolbar to display the on\-screen keyboard\. Passing this string into HIDDEN\_ELEMENTS hides the keyboard icon\. | 
| 'keyboardShortcutsButton' | During AppStream 2\.0 streaming sessions on touch\-enabled devices, users can tap the Fn icon to display keyboard shortcuts\. Passing this string into HIDDEN\_ELEMENTS hides the Fn icon\. | 

### Functions for the `AppStream.Embed` Object<a name="functions-embed-object"></a>

The following table lists the functions that can be performed on the `AppStream.Embed` object\. 


| Function | Description | 
| --- | --- | 
| AppStream\.Embed\(containerId:string, options:object\) | The AppStream\.Embed object constructor\. This constructor initializes and communicates with the AppStream\.Embed object, and it uses a div container ID\. The ID is used to inject the iframe\. It also injects an object that includes the configuration options for appstreamOptions \(sessionURL and HIDDEN\_ELEMENTS\)\.  | 
| endSession\(\) | This function ends the streaming session, but does not destroy the iframe\. If you specify a redirect URL, the iframe attempts to load the URL\. Depending on the CORS headers of the page, the URL may not load\.  | 
| launchApp\(appId:string\) | This function programmatically launches an application with the application ID that was specified during image creation\.  | 
| launchAppSwitcher\(\) | This function sends the AppSwitcher command to the AppStream 2\.0 portal\. This triggers the AppSwitcher command on the instance\.  | 
| getSessionState\(\) | This function returns an object for sessionStatus\. For more information, see [Events for Embedded AppStream 2\.0 Streaming Sessions](#events-embedded-streaming-sessions)\.  | 
| getUserInterfaceState\(\) | This function returns an object for `UserInterfaceState`\. The object contains the key\-value pairs for the following:  `sessionStatus`: State enumeration `sessionTerminationReason`: String `sessionDisconnectionReason`: String  For more information, see [Events for Embedded AppStream 2\.0 Streaming Sessions](#events-embedded-streaming-sessions)\.  | 
| addEventListener\(name, callback\) | This function adds a callback function to call when the specified event is triggered\. For a list of the events that can be triggered, see [Events for Embedded AppStream 2\.0 Streaming Sessions](#events-embedded-streaming-sessions)\.  | 
| removeEventListener\(name, callback\) | This function removes the callback for the specified events\.  | 
| destroy\(\) | This function deletes the iframe and cleans up resources\. This function does not affect streaming sessions that are in progress\.  | 

### Events for Embedded AppStream 2\.0 Streaming Sessions<a name="events-embedded-streaming-sessions"></a>

The following table lists the events that can be triggered during embedded AppStream 2\.0 streaming sessions\.


| Event | Data | Description | 
| --- | --- | --- | 
| AppStream\.Embed\.Events\.SESSION\_STATE\_CHANGE |  `sessionStatus`: `State enumeration` `sessionTerminationReason`: String `sessionDisconnectionReason`: String  | This event is triggered when any session state change occurs\. The event includes a map of the states that changed\. To retrieve the full session state, use the `getSessionState()` function\. Following are the session states: `AppStream.Embed.SessionStatus.Unknown` — The session has not started and is not reserved `AppStream.Embed.SessionStatus.Reserved` — The session is reserved but has not started\.  `AppStream.Embed.SessionStatus.Started` — The user connected to the session and started streaming\. `AppStream.Embed.SessionStatus Disconnected `— The user disconnected from the session\. `AppStream.Embed.SessionStatus.Ended` — The session was marked as ended or expired\.  | 
| AppStream\.Embed\.Events\.SESSION\_INTERFACE\_STATE\_CHANGE | `hiddenElements`: Array of strings  `isFullscreen`: Boolean `isSoftKeyboardVisible`: Boolean  | This event is triggered when any session state change occurs\. The event includes a map of the states that changed\. To retrieve the full session state, use the getSessionState\(\) function\. | 
| AppStream\.Embed\.Events\.SESSION\_ERROR | `errorCode`: Number `errorMessage`: String  | This event is triggered when any errors occur during a session\. | 

### Examples for Adding Event Listeners and Ending an Embedded AppStream 2\.0 Streaming Session<a name="examples-add-event-listeners-end-embedded-streaming-session"></a>

The examples in this section show how to do the following:
+ Add event listeners for embedded AppStream 2\.0 streaming sessions\.
+ Programmatically end an embedded AppStream 2\.0 streaming session\.

#### Example 1: Add event listeners for embedded AppStream 2\.0 streaming sessions<a name="example-add-event-listeners"></a>

To add event listeners for session state changes, session interface state changes, and session errors during embedded streaming sessions, use the following code:

```
appstreamEmbed.addEventListener(AppStream.Embed.Events.SESSION_STATE_CHANGE, updateSessionStateCallback);

appstreamEmbed.addEventListener(AppStream.Embed.Events.SESSION_INTERFACE_STATE_CHANGE, updateUserInterfaceStateCallback);

appstreamEmbed.addEventListener(AppStream.Embed.Events.SESSION_ERROR, errorCallback);
```

In this example, `AppStream.Embed.Events.SESSION_STATE_CHANGE`, `AppStream.Embed.Events.SESSION_INTERFACE_STATE_CHANGE`, and `AppStream.Embed.Events.SESSION_ERROR` are event names\.

The `updateSessionStateCallback`, `updateUserInterfaceStateCallback`, and `errorCallback` functions are ones that you implement\. These functions are passed into the `addEventListener` function and called when an event is triggered\.

#### Example 2: Programmatically end an embedded AppStream 2\.0 streaming session<a name="programmatically-end-embedded-streaming-session"></a>

To end an embedded AppStream 2\.0 streaming sessions, use the following function:

```
appstreamEmbed.endSession();
```