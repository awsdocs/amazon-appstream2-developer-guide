# Use the AppStream 2\.0 Client to Start a Streaming Session<a name="use-client-start-streaming-session"></a>

After you install the AppStream 2\.0 client on your users' local computers, they can use the client to connect to a streaming session\. You can configure one or more of the following connection methods, as required for your organization:
+ [The AppStream 2\.0 API](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL)
+ [SAML 2\.0](external-identity-providers-setting-up-saml.md)
+ [The AppStream 2\.0 user pool \(console\)](user-pool.md)

For each of these connection methods, the user experience is as follows:

**AppStream 2\.0 API**

In the AppStream 2\.0 client sign\-in page, users enter the streaming URL that you created as the web address, and then choose **Connect**\.

**SAML 2\.0**

If you use SAML 2\.0 to federate your users to an AppStream 2\.0 stack, you must create a registry value to configure the AppStream 2\.0 client with a prepopulated URL whenever the client is launched\. The URL must use a certificate that is trusted by the device\. The certificate must contain a Subject Alternative Name \(SAN\) that includes the URL's domain name\. For more information, see [Set the StartURL Registry Value for AppStream 2\.0 Client Users](install-client-configure-settings.md#set-start-url-registry-value)\.

**User pool**

In the AppStream 2\.0 client sign\-in page, users enter the URL that was provided in your welcome email, and then choose **Connect**\. 

For step\-by\-step guidance that you can provide your users to help them with connecting to AppStream 2\.0 and starting a streaming session, see the following topics:
+  [Connect by Using a Web Browser](web-browser-user.md#web-browser-start-streaming-session-user)
+ [Connect by Using the AppStream 2\.0 Client for Windows](client-application-windows-user.md#client-application-windows-start-streaming-session-user)