# Web Browser Access<a name="web-browser-user"></a>

The following information helps you use a web browser to connect to AppStream 2\.0 and stream applications\.

**Topics**
+ [Requirements](#web-browser-requirements-user)
+ [Setup](#web-browser-setup-user)
+ [Connect to AppStream 2\.0](#web-browser-start-streaming-session-user)
+ [Monitors and Display Resolution](#web-browser-monitors-display-resolution-user)
+ [USB Devices](#web-browser-usb-devices-user)
+ [Touchscreen Devices](#web-browser-using-touchscreen-devices-user)
+ [Function Keys](#web-browser-using-function-keys-user)
+ [Remap the Mac Option and Command Keys](#web-browser-remap-mac-keys-user)
+ [Video and Audio Conferencing](#web-browser-video-audio)
+ [Drawing Tablets](#web-browser-drawing-tablets-user)
+ [Relative Mouse Offset](#web-browser-relative-mouse-offset-web-access-user)
+ [Troubleshooting](#web-browser-troubleshooting-user)

## Requirements<a name="web-browser-requirements-user"></a>

You can connect to AppStream 2\.0 from any location by using an HTML5\-capable web browser\. Supported browsers include the following:
+ Google Chrome
+ Mozilla Firefox
+ Safari
+ Microsoft Edge
+ Microsoft Internet Explorer version 11 or later

**Note**  
Only the Google Chrome or Mozilla Firefox browsers are supported for use with drawing tablets during AppStream 2\.0 streaming sessions\. Webcam redirection for video and audio conferencing is supported on Chromium\-based web browsers, including Google Chrome and Microsoft Edge\.

## Setup<a name="web-browser-setup-user"></a>

No browser extensions or plugins are required to use AppStream 2\.0 in a web browser\. 

## Connect to AppStream 2\.0<a name="web-browser-start-streaming-session-user"></a>

Follow these steps to connect to AppStream 2\.0 and start an application streaming session\.

1. If your administrator requires you to sign in first through your organization's sign\-in page, complete the tasks in this step\.

   If your administrator doesn't require you to sign in through your organization's sign\-in page, skip the tasks in this step and proceed to step 2\.

   1. Navigate to your organizational sign\-in page and enter your domain credentials when prompted\.

   1. After you sign in, you are redirected to a page that displays one or more applications that are available for your AppStream 2\.0 streaming session\. **Desktop View** is also available, if enabled by your administrator\.

   1. Choose an application or, if available, **Desktop View**\.

1. If your administrator doesn't require you to sign in first through your organization's sign\-in page, do either of the following:
   + If this is the first time that you've used AppStream 2\.0 and you receive a welcome email that notifies you to start accessing your applications using AppStream 2\.0:

     1. Open the email, and then select the **Login page** link\.

     1. Enter your email address and the temporary password that was provided in the email, and then choose **Log in**\.

     1. When prompted, enter a new password, confirm it, and then choose **Set Password**\.

     1. After a few moments, the AppStream 2\.0 portal opens, displaying one or more applications that are available for your AppStream 2\.0 streaming session\. **Desktop View** is also available, if enabled by your administrator\.

     1. Choose an application or, if available, **Desktop View**\.
   + If this isn't the first time that you've used AppStream 2\.0 and your administrator has provided you with the web address \(URL\) for the AppStream 2\.0 portal:

     1. Enter the URL provided by your administrator to navigate to the AppStream 2\.0 portal\.

     1. Enter your password when prompted, and choose **Connect**\.

     1. After a few moments, the AppStream 2\.0 portal opens, displaying one or more applications that are available for your AppStream 2\.0 streaming session\. **Desktop View** is also available, if enabled by your administrator\.

## Monitors and Display Resolution<a name="web-browser-monitors-display-resolution-user"></a>

AppStream 2\.0 supports the use of multiple monitors during streaming sessions, including monitors that have different resolutions\. To help ensure an optimal streaming experience, we recommend that you set the display scale for your monitors to 100 percent if you use multiple monitors\.

You can use dual monitors for application streaming sessions that are started on the following web browsers:
+ Google Chrome
+ Mozilla Firefox
+ Safari
+ Microsoft Edge

For browser\-based streaming sessions on dual monitors, a maximum display resolution of 2560x1600 pixels is supported per monitor\. If you require more than two monitors, or a display resolution that is greater than 2560x1600 pixels per monitor, you must use the AppStream 2\.0 client\.

## USB Devices<a name="web-browser-usb-devices-user"></a>

USB devices are not supported for browser\-based AppStream 2\.0 streaming sessions\. To use your USB devices with applications streamed through AppStream 2\.0, you must use the AppStream 2\.0 client\. For more information, see [AppStream 2\.0 Client Application for Windows](client-application-windows-user.md)\.

## Touchscreen Devices<a name="web-browser-using-touchscreen-devices-user"></a>

AppStream 2\.0 supports gestures on touch\-enabled iPads, Android tablets, and Windows devices\. Examples of supported touch gestures include long\-tap to right\-click, swipe to scroll, pinch to zoom, and two\-finger rotation for supporting applications\.

To display the on\-screen keyboard on an iPad or Android tablet, tap the keyboard icon on the AppStream 2\.0 toolbar\. The keyboard icon turns blue, and you can use the on\-screen keyboard to input text in the streaming application\. Tap the keyboard icon again to hide the on\-screen keyboard\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/CircleKeyboardIconBorder.PNG)

Tap the Fn icon to display a row of Windows\-specific keys and keyboard shortcuts\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/CircleFnIconBorder.PNG)

For touch\-enabled devices, the *remote keyboard*, which is displayed when you tap the keyboard icon on the AppStream 2\.0 toolbar, is different than the *local keyboard*, the on\-screen keyboard that a touch\-enabled device automatically displays when you tap inside an input control in a locally running application\. During AppStream 2\.0 streaming sessions, you can use the remote keyboard to input text into streaming applications only\. You can display or hide the remote keyboard only by tapping the keyboard icon on the AppStream 2\.0 toolbar\. A blue keyboard icon on the AppStream 2\.0 toolbar indicates that the remote keyboard is active\.

You can use the local keyboard to input text into elements of the AppStream 2\.0 web portal, including the **My Files** dialog box\. However, you can't use this keyboard to input text into streaming applications\. Also, you can't display or hide it by using the keyboard icon on the AppStream 2\.0 toolbar\.

**Note**  
To display the on\-screen keyboard on a Windows computer, tap the keyboard icon in the Windows system tray\. If the keyboard icon doesn't appear in the Windows system tray, switch to Windows tablet mode\. Tap the keyboard icon in the Windows system tray again to hide the on\-screen keyboard\.

For more information about function keys, see the next section\.

## Function Keys<a name="web-browser-using-function-keys-user"></a>

You can use keyboard shortcuts during AppStream 2\.0 streaming sessions to enter special keystrokes or key combinations\. To display a row of Windows\-specific keys and keyboard shortcuts during your streaming session, choose the Fn icon\. The Fn icon is displayed in the AppStream 2\.0 toolbar in the top right of your session window\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream-Fn-Key-1.png)

Following is an example of how Windows\-specific keys and keyboard shortcuts are displayed when you choose the Fn icon\. If not all keys are displayed, you can scroll to the right or left on the shortcut toolbar to display more keys\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream-Fn-Key-2a-Keys-No-Scrollbar.png)

To use a key combination that includes the Windows Control key, choose the Ctrl key on the shortcut toolbar, and then type any key on the shortcut toolbar \(or, if you are using a touch\-enabled device, the on\-screen keyboard\)\. Choosing the Ctrl key changes the color to blue\. In this case, any other key that you select is interpreted as a key combination that includes the Control key\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream-Fn-Key-3-Choose-Ctrl-Key.png)

Choose the Ctrl key again to release it\. For example, to use the keyboard shortcut Ctrl \+ F, choose the Ctrl key on the shortcut toolbar, and then type the f key\. Choose the Ctrl key on the shortcut toolbar again to release the Control key\. To use shortcuts that include the Alt or Shift keys, choose the Alt key or the Shift key on the shortcut toolbar in the same way\. You can use the Shift key on the shortcut toolbar only for keyboard shortcuts\. If you are using a touch\-enabled device, this key doesn't affect the capitalization of keys that you type on the on\-screen keyboard\.

## Remap the Mac Option and Command Keys<a name="web-browser-remap-mac-keys-user"></a>

When you use a device that runs macOS or Mac OS X to connect to AppStream 2\.0, you can remap the Mac Option and Command keys on your keyboard\. 

A *modifier key* modifies the action of another key when you use both keys together\. You can use a modifier key with another key to perform a task such as printing\. A *Meta key* is a special type of modifier key\. You can use a Meta key to temporarily change the function of another key when you use both keys together\.


| You can remap this Mac key | To this key during a streaming session | 
| --- | --- | 
| Option key ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/mac-option-key.png)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/web-browser-user.html)  | 
| Command key ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/mac-command-key.png)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/web-browser-user.html)  | 

Follow these steps to remap the Mac Option and Command keys during an AppStream 2\.0 streaming session\.

**To remap the Mac Option and Command keys**

1. Use a web browser to connect to AppStream 2\.0\.

1. In the top left of the AppStream 2\.0 toolbar, choose the **Settings** icon, and choose **Keyboard Settings**\.

1. Choose the options that correspond to the keys that you want to remap\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/AppStream-Mac-Key-Remapping-for-Windows.png)

## Video and Audio Conferencing<a name="web-browser-video-audio"></a>

AppStream 2\.0 real\-time audio\-video \(AV\) redirects your local webcam video and microphone audio input to AppStream 2\.0 streaming sessions\. That way, you can use your local devices for video and audio conferencing within your AppStream 2\.0 streaming session\. 

**To use a local webcam and microphone within an AppStream 2\.0 streaming session**

1. Connect to AppStream 2\.0 from a Chromium\-based web browser, including Google Chrome and Microsoft Edge\. 
**Note**  
Most popular HTML5 compatible browsers support audio input in an AppStream 2\.0 session, including Chrome, Edge, and Firefox\.
**Note**  
If your web browser doesn't support video or audio input, the options won't appear on the AppStream 2\.0 toolbar\.

1. Configure your web browser’s camera and microphone permissions to set default devices and allow access to AppStream 2\.0\.
**Note**  
For information about how to configure Google Chrome, see [Use your camera & microphone](https://support.google.com/chrome/answer/2693767)\.

1. In the top\-left of the AppStream 2\.0 toolbar, choose the Settings icon, and then choose **Enable webcam**\.
**Note**  
If the microphone or webcam icons don't appear in the **Settings** menu, contact your AppStream 2\.0 administrator\. Your web browser might not support video or audio input, or your administrator might need to perform additional configuration tasks\. For more information, see [Real\-Time Audio\-Video \(Client for Windows\)](client-system-requirements-feature-support.md#feature-support-real-time-av)\.

1. Depending on your web browser settings, you might be prompted to allow the camera to be used by your web browser\. Choose **Allow** to enable your camera\.

1. In the top\-left of the AppStream 2\.0 toolbar, choose the Settings icon, and then choose **Enable microphone**\.

1. Depending on your web browser settings, you might be prompted to the microphone to be used by your web browser\. Choose **Allow** to enable your microphone\.
**Note**  
If you have more than one webcam or microphone and want to change the devices that you use for streaming within an AppStream 2\.0 session, you must clear your web browser settings for the AppStream 2\.0 website URL and configure default devices\. Then, refresh your browser or start a new session for the changes to take effect, and repeat the above steps to enable your webcam and microphone\.

## Drawing Tablets<a name="web-browser-drawing-tablets-user"></a>

Drawing tablets, also known as pen tablets, are computer input devices that let you draw with a stylus \(pen\)\. With AppStream 2\.0, you can connect a drawing tablet, such as a Wacom drawing tablet, to your local computer and use the tablet with your streaming applications\. 

Following are requirements and considerations for using drawing tablets with your streaming applications\.
+ To use this feature, you must connect to AppStream 2\.0 through the Google Chrome or Mozilla Firefox browsers only, or by using the [AppStream 2\.0 client](client-application-windows-user.md)\.
+ The applications that you stream must support Windows Ink technology\. For more information, see [Pen interactions and Windows Ink in Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/input/pen-and-stylus-interactions)\.
+ Depending on the streaming applications that you use, your drawing tablet might require USB redirection to function as expected\. This is because some applications, such as GIMP, require USB redirection to support pressure sensitivity\. If this is the case for your streaming applications, you must connect to AppStream 2\.0 by using the AppStream 2\.0 client, and share the drawing tablet with your streaming session\. For information about how to share USB devices with your streaming session, see [USB Devices](client-application-windows-user.md#client-application-windows-how-to-share-usb-devices-user)\.
+ This feature is not supported on Chromebooks\.

To get started with using a drawing tablet during your application streaming sessions, connect your drawing tablet to your local computer with USB, share the device with AppStream 2\.0 if required for pressure sensitivity detection, and then start an AppStream 2\.0 streaming session\. You can use a supported web browser or the AppStream 2\.0 client, if it is installed, to start a streaming session\.

## Relative Mouse Offset<a name="web-browser-relative-mouse-offset-web-access-user"></a>

By default, during a streaming session, AppStream 2\.0 transmits information about mouse movements by using absolute coordinates and rendering the mouse movements locally\. For graphics\-intensive applications, such as computer\-aided design \(CAD\)/computer\-aided manufacturing \(CAM\) software or video games, mouse performance improves when relative mouse mode is enabled\. Relative mouse mode uses relative coordinates, which represent how far the mouse moved since the last frame, rather than the absolute x\-y coordinate values within a window or screen\. When you enable relative mouse mode, AppStream 2\.0 renders the mouse movements remotely\.

You can enable this feature during an AppStream 2\.0 streaming session by doing either of the following:
+ Windows: Pressing Ctrl\+Shift\+F8
+ Mac: Pressing Control\+Fn\+Shift\+F8

## Troubleshooting<a name="web-browser-troubleshooting-user"></a>

If issues occur when you use AppStream 2\.0, your AppStream 2\.0 session ID can help your administrator with troubleshooting\. This section describes how to find the session ID\. 

The session ID is created when you request a streaming session\. The session ID, and other information used by AppStream 2\.0, is stored in the session storage location for your browser\. You can use the developer tools that are available for your browser interface to find this location\.

For information about the developer tools that are available for common web browsers, see the following resources:
+ [Apple Safari Developer Help: Storage tab](https://support.apple.com/guide/safari-developer/storage-tab-dev43453fff5/mac)
+ [View And Edit Session Storage With Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/storage/sessionstorage)
+ [Firefox Developer Tools: Local Storage / Session Storage](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Local_Storage_Session_Storage)
+ [Microsoft Edge \(Chromium\) Developer Tools](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium)
+ [Microsoft Edge \(EdgeHTML\) Developer Tools](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide)

After you locate the developer tools for your browser, search for the session storage for the AppStream 2\.0 website\. The domain for the website is **https://appstream2\.<*aws\-region*>\.aws\.amazon\.com**\. Expand the domain, and choose **sessionStorage\.as2SessionData**\. The session ID is stored in the key **sessionId**\.