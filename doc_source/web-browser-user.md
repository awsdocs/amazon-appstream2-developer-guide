# Web Browser Access<a name="web-browser-user"></a>

The following information helps you use a web browser to connect to AppStream 2\.0 and stream applications\.

**Topics**
+ [Requirements](#web-browser-requirements-user)
+ [Setup](#web-browser-setup-user)
+ [Connect to AppStream 2\.0](#web-browser-start-streaming-session-user)
+ [Monitors and Display Resolution](#web-browser-monitors-display-resolution-user)
+ [Touchscreen Devices](#web-browser-using-touchscreen-devices-user)
+ [Drawing Tablets](#web-browser-drawing-tablets-user)
+ [Troubleshooting](#web-browser-troubleshooting-user)

## Requirements<a name="web-browser-requirements-user"></a>

You can connect to AppStream 2\.0 from any location by using an HTML5\-capable web browser\. Supported browsers include the following:
+ Google Chrome
+ Mozilla Firefox
+ Safari
+ Microsoft Edge
+ Microsoft Internet Explorer version 11 or later

**Note**  
Only the Google Chrome or Mozilla Firefox browsers are supported for use with drawing tablets during AppStream 2\.0 streaming sessions\.

## Setup<a name="web-browser-setup-user"></a>

No browser extensions or plugins are required to use AppStream 2\.0 in a web browser\. 

## Connect to AppStream 2\.0<a name="web-browser-start-streaming-session-user"></a>

Follow these steps to connect to AppStream 2\.0 and start an application streaming session\.

1. If you received a welcome email that notifies you to start accessing your apps using AppStream 2\.0, open the email, and then click the **Login page** link\.

1. In the AppStream 2\.0 sign\-in page, enter your email address and the temporary password that was provided in the email, and then choose **Log in**\.

1. When prompted, enter a new password, confirm it, and then choose **Set Password**\.

1. When the AppStream 2\.0 application portal opens, displaying applications that your administrator has made available to you for streaming, click an application to start it\.

## Monitors and Display Resolution<a name="web-browser-monitors-display-resolution-user"></a>

You can use dual monitors for application streaming sessions that are started on the following web browsers:
+ Google Chrome
+ Mozilla Firefox
+ Safari

For browser\-based streaming sessions on dual monitors, a maximum display resolution of 2560x1440 pixels is supported per monitor\. If you require more than two monitors, or a display resolution that is greater than 2560x1440 pixels per monitor, you must use the AppStream 2\.0 client\.

## Touchscreen Devices<a name="web-browser-using-touchscreen-devices-user"></a>

AppStream 2\.0 supports gestures on touch\-enabled iPads, Android tablets, and Windows devices\. Examples of supported touch gestures include long\-tap to right\-click, swipe to scroll, pinch to zoom, and two\-finger rotation for supporting applications\.

To display the on\-screen keyboard on an iPad or Android tablet, tap the keyboard icon on the AppStream 2\.0 toolbar\. The keyboard icon turns blue, and you can use the on\-screen keyboard to input text in the streaming application\. Tap the keyboard icon again to hide the on\-screen keyboard\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/CircleKeyboardIconBorder.PNG)

Tap the Fn icon to display a row of Windows\-specific keys and keyboard shortcuts\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/CircleFnIconBorder.PNG)

Here is an example of how Windows\-specific keys and keyboard shortcuts are displayed when the Fn icon is tapped\. Swipe to the left on the shortcut toolbar to display more keys\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/ShortcutRowBorder.PNG)

To use a key combination that includes the Windows Control key, tap the Ctrl key on the shortcut toolbar, and then type any key on either the on\-screen keyboard or the shortcut toolbar\. Tapping the Ctrl key changes the color to blue\. In this case, any other key that you select is interpreted as a key combination that includes the Control key\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/ShortcutRowControlKeyHighlightedBorder.PNG)

Tap the Ctrl key again to release it\. For example, to use the keyboard shortcut Ctrl \+ F, tap the Ctrl key on the shortcut toolbar, and then type the f key on the on\-screen keyboard\. Tap the Ctrl key on the shortcut toolbar again to release the Control key\. To use shortcuts that include the Alt or Shift keys, tap the Alt key or the Shift key on the shortcut toolbar in the same way\. You can use the Shift key on the shortcut toolbar only for keyboard shortcuts\. This key doesn't affect the capitalization of keys that you type on the on\-screen keyboard\.

**Note**  
The *remote keyboard*, the on\-screen keyboard that is displayed when a user taps the keyboard icon on the AppStream 2\.0 toolbar, is different than the *local keyboard*, the on\-screen keyboard that a touch\-enabled device automatically displays when a user taps inside an input control in a locally running application\. During AppStream 2\.0 streaming sessions, the remote keyboard can be used to input text into streaming applications only\. Users can display or hide the remote keyboard only by tapping the keyboard icon on the AppStream 2\.0 toolbar\. A blue keyboard icon on the AppStream 2\.0 toolbar indicates that the remote keyboard is active\.  
The local keyboard can be used to input text into elements of the AppStream 2\.0 web portal, including the **My Files** dialog box\. However, this keyboard can't be used to input text into streaming applications\. Also, users can't display or hide it by using the keyboard icon on the AppStream 2\.0 toolbar\.  
AppStream 2\.0 doesn't display the keyboard icon or the Fn icon when streaming to a Windows device because Windows already provides a way to display an on\-screen keyboard that includes common Windows keys\. To display the on\-screen keyboard on a Windows computer, tap the keyboard icon in the Windows system tray\. If the keyboard icon doesn't appear in the Windows system tray, switch to Windows tablet mode\. Tap the keyboard icon in the Windows system tray again to hide the on\-screen keyboard\.

## Drawing Tablets<a name="web-browser-drawing-tablets-user"></a>

Drawing tablets, also known as pen tablets, are computer input devices that let you draw with a stylus \(pen\)\. With AppStream 2\.0, you can connect a drawing tablet, such as a Wacom drawing tablet, to your local computer and use the tablet with your streaming applications\. 

Following are requirements and considerations for using drawing tablets with your streaming applications\.
+ To use this feature, you must connect to AppStream 2\.0 through the Google Chrome or Mozilla Firefox browsers only, or by using the [AppStream 2\.0 client](client-application-windows-user.md)\.
+ The applications that you stream must support Windows Ink technology\. For more information, see [Pen interactions and Windows Ink in Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/input/pen-and-stylus-interactions)\.
+ Depending on the streaming applications that you use, your drawing tablet might require USB redirection to function as expected\. This is because some applications, such as GIMP, require USB redirection to support pressure sensitivity\. If this is the case for your streaming applications, you must connect to AppStream 2\.0 by using the AppStream 2\.0 client, and share the drawing tablet with your streaming session\. For information about how to share USB devices with your streaming session, see [USB Devices](client-application-windows-user.md#client-application-share-usb-devices-with-session-user)\.
+ This feature is not supported on Chromebooks\.

To get started with using a drawing tablet during your application streaming sessions, connect your drawing tablet to your local computer with USB, share the device with AppStream 2\.0 if required for pressure sensitivity detection, and then start an AppStream 2\.0 streaming session\. You can use a supported web browser or the AppStream 2\.0 client, if it is installed, to start a streaming session\.

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