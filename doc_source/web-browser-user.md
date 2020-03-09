# Web Browser Access<a name="web-browser-user"></a>

The following information will help you get started with using a web browser to connect to AppStream 2\.0 and stream applications\.

**Topics**
+ [Requirements](#web-browser-requirements-user)
+ [Setup](#web-browser-setup-user)
+ [Connect to AppStream 2\.0](#web-browser-start-streaming-session-user)
+ [Monitors and Display Resolution](#web-browser-monitors-display-resolution-user)
+ [Touchscreen Devices](#using-touchscreen-devices-user)

## Requirements<a name="web-browser-requirements-user"></a>

You can connect to AppStream 2\.0 from any location by using an HTML5\-capable web browser\. Supported browsers include the following:
+ Google Chrome
+ Mozilla Firefox
+ Safari
+ Microsoft Edge
+ Microsoft Internet Explorer version 11 or later

## Setup<a name="web-browser-setup-user"></a>

No browser extensions or plugins are required to use AppStream 2\.0 in a web browser\. 

## Connect to AppStream 2\.0<a name="web-browser-start-streaming-session-user"></a>

To connect to AppStream 2\.0 and start an application streaming session, perform these steps\.

1. If you received a welcome email that notifies you to start accessing your apps using AppStream 2\.0, open the email and click the **Login page** link\.

1. The AppStream 2\.0 sign\-in page opens in your browser\.

1. Type your email address and the temporary password that was provided in the email, and choose **Log in**\.

1. When prompted, type a new password, confirm it, and then choose **Set Password**\.

1. The AppStream 2\.0 application portal opens, displaying applications that your administrator has made available to you for streaming\.

1. Click an application to start it\.

## Monitors and Display Resolution<a name="web-browser-monitors-display-resolution-user"></a>

You can use dual monitors for application streaming sessions that are started on the following web browsers:
+ Google Chrome
+ Mozilla Firefox
+ Safari

For browser\-based streaming sessions on dual monitors, a maximum display resolution of 2560x1440 pixels is supported per monitor\. If you require more than two monitors, or a display resolution that is greater than 2560x1440 pixels per monitor, you must use the AppStream 2\.0 client\.

## Touchscreen Devices<a name="using-touchscreen-devices-user"></a>

AppStream 2\.0 supports gestures on touch\-enabled iPads, Android tablets, and Windows devices\. Examples of supported touch gestures include long\-tap to right\-click, swipe to scroll, pinch to zoom, and two\-finger rotation for supporting applications\.

To display the on\-screen keyboard on an iPad or Android tablet, tap the keyboard icon on the AppStream 2\.0 toolbar\. The keyboard icon turns blue, and you can use the on\-screen keyboard to input text within the streaming application\. Tap the keyboard icon again to hide the on\-screen keyboard\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/CircleKeyboardIconBorder.PNG)

Tap the Fn icon to display a row of Windows\-specific keys and keyboard shortcuts\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/CircleFnIconBorder.PNG)

Following is an example of how Windows\-specific keys and keyboard shortcuts are displayed when the Fn icon is tapped\. Swipe to the left on the shortcut toolbar to display more keys\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/ShortcutRowBorder.PNG)

To use a key combination that includes the Windows Control key, tap the Ctrl key on the shortcut toolbar and then type any key on either the on\-screen keyboard or the shortcut toolbar\. Tapping the Ctrl key changes the color to blue\. In this case, any other key that you select is interpreted as a key combination that includes the Control key\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/ShortcutRowControlKeyHighlightedBorder.PNG)

Tap the Ctrl key again to release it\. For example, to use the keyboard shortcut Ctrl \+ F, tap the Ctrl key on the shortcut toolbar, and then type the f key on the on\-screen keyboard\. Tap the Ctrl key on the shortcut toolbar again to release the Control key\. To use shortcuts that include the Alt or Shift keys, tap the Alt key and/or the Shift key on the shortcut toolbar in the same way\. You can use the Shift key on the shortcut toolbar only for keyboard shortcuts\. This key doesn't affect the capitalization of keys that you type on the on\-screen keyboard\.

**Note**  
The *remote keyboard*, the on\-screen keyboard that is displayed when a user taps the keyboard icon on the AppStream 2\.0 toolbar, is different than the *local keyboard*, the on\-screen keyboard that a touch\-enabled device automatically displays when a user taps inside an input control in a locally running application\. During AppStream 2\.0 streaming sessions, the remote keyboard can be used to input text into streaming applications only\. Users can display or hide the remote keyboard only by tapping the keyboard icon on the AppStream 2\.0 toolbar\. A blue keyboard icon on the AppStream 2\.0 toolbar indicates that the remote keyboard is active\.  
The local keyboard can be used to input text into elements of the AppStream 2\.0 web portal, including the **My Files** dialog box\. This keyboard can't be used, however, to input text into streaming applications\. Also, users can't display or hide it by using the keyboard icon on the AppStream 2\.0 toolbar\.  
AppStream 2\.0 doesn't display the keyboard icon or the Fn icon when streaming to a Windows device because Windows already provides a way to display an on\-screen keyboard that includes common Windows keys\. To display the on\-screen keyboard on a Windows computer, tap the keyboard icon in the Windows system tray\. If the keyboard icon doesn't appear in the Windows system tray, switch to Windows tablet mode\. Tap the keyboard icon in the Windows system tray again to hide the on\-screen keyboard\.