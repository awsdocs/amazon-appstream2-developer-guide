# Provide Access Through a Web Browser<a name="access-through-web-browser-admin"></a>

Users can access AppStream 2\.0 through an HTML5\-capable web browser on a desktop computer such as a Windows, Mac, Chromebook, or Linux computer\. HTML5\-capable web browsers that can be used include the following:
+ Google Chrome
+ Mozilla Firefox
+ Safari
+ Microsoft Edge
+ Microsoft Internet Explorer version 11 or later

No browser extensions or plugins are required to use AppStream 2\.0 in a web browser\. 

Users can also access AppStream 2\.0 fleet streaming sessions on the following browsers and devices:
+ Chrome or Safari on an iPad \(iOS 11 or later\)
+ Android \(Android 8 or later\)
+ Microsoft Surface Pro \(Windows 10\) tablet

AppStream 2\.0 is not supported on devices that have screen resolutions smaller than 1024x768 pixels\.

## Dual\-Monitor Support<a name="dual-monitor-support-web-access-admin"></a>

AppStream 2\.0 provides dual\-monitor support for streaming sessions that are started on the following web browsers:
+ Google Chrome
+ Mozilla Firefox
+ Safari

For browser\-based streaming sessions on dual monitors, a maximum display resolution of 2560x1440 pixels is supported per monitor\. If your users require more than two monitors, or a display resolution that is greater than 2560x1440 pixels per monitor, the AppStream 2\.0 client is available\.

**Note**  
Dual monitors are not supported on mobile devices or for embedded AppStream 2\.0 streaming sessions\. 

In addition to user connections for streaming sessions, AppStream 2\.0 also supports the use of dual monitors for administrative connections to image builders\.

## Touchscreen Device Support<a name="touchscreen-device-web-access-admin"></a>

AppStream 2\.0 supports gestures on touch\-enabled iPads, Android tablets, and Windows devices\. All touch events are passed through to the streaming session and handled according to Windows conventions\. Examples of supported touch gestures include long\-tap to right\-click, swipe to scroll, pinch to zoom, and two\-finger rotation for supporting applications\.

**Note**  
To enable support for gestures on touch\-enabled devices, your AppStream 2\.0 image must use a version of the AppStream 2\.0 agent released on or after March 7, 2019\. For more information, see [AppStream 2\.0 Agent Version History](agent-software-versions.md)\. 

For guidance that you can provide your users to help them get started with touch\-enabled devices during their AppStream 2\.0 streaming sessions, see [Touchscreen Devices](web-browser-user.md#web-browser-using-touchscreen-devices-user)\.

## Drawing Tablet Support<a name="drawing-tablet-support-web-access-admin"></a>

Drawing tablets, also known as pen tablets, are computer input devices that let users draw with a stylus \(pen\)\. With AppStream 2\.0, your users can connect a drawing tablet, such as a Wacom drawing tablet, to their local computer and use the tablet with their streaming applications\.

Following are requirements and considerations for enabling your users to use drawing tablets with their streaming applications\.
+ To enable your users to use this feature, you must configure your AppStream 2\.0 fleet to use an image that runs Windows Server 2019\.
+ To use this feature, users must access AppStream 2\.0 through the Google Chrome or Mozilla Firefox browsers only, or the AppStream 2\.0 client\.
+ Streaming applications must support Windows Ink technology\. For more information, see [Pen interactions and Windows Ink in Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/input/pen-and-stylus-interactions)\.
+ Some applications, such GIMP, must detect drawing tablets on the streaming instance to support pressure sensitivity\. If this is the case, your users must use the AppStream 2\.0 client to access AppStream 2\.0 and stream these applications\. In addition, you must qualify your users' drawing tablets, and users must share their drawing tablets with AppStream 2\.0 every time they start a new streaming session\. For step\-by\-step guidance, see [Qualify USB Devices for Use with Streaming Applications](qualify-usb-devices.md)\.
+ This feature is not supported on Chromebooks\.

To get started with using drawing tablets during application streaming sessions, users connect their drawing tablet to their local computer with USB and use a supported web browser or the AppStream 2\.0 client, if it is installed, to start a streaming session\. No USB redirection is required to use this feature\.