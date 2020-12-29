# Configure a Connection Method for Your AppStream 2\.0 Client Users<a name="use-client-start-streaming-session"></a>

After you install the AppStream 2\.0 client on your users' local computers, they can use the AppStream 2\.0 client to connect to a streaming session\. You can configure one or more of the following connection methods, as required for your organization\.

**Streaming URL**

In the AppStream 2\.0 client sign\-in page, users enter the streaming URL that you created as the web address, and then choose **Connect**\. To create a streaming URL, use one of the following methods:
+ AppStream 2\.0 console
+ The [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action 
+ The [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) AWS CLI command

**SAML 2\.0**

If you use [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md) to federate your users to an AppStream 2\.0 stack, you must create a registry value to configure the AppStream 2\.0 client with a prepopulated URL whenever the client is launched\. The URL must use a certificate that is trusted by the device\. The certificate must contain a Subject Alternative Name \(SAN\) that includes the URL's domain name\. For more information, see [Set the StartURL Registry Value for AppStream 2\.0 Client Users](install-client-configure-settings.md#set-start-url-registry-value)\.

**AppStream 2\.0 user pool**

When you create a new user in the AppStream 2\.0 user pool, or asssign a user pool user to an AppStream 2\.0 stack, AppStream 2\.0 sends email to users on your behalf\. In the AppStream 2\.0 client sign\-in page, users enter the URL that was provided in the welcome email, enter their credentials, and then choose **Connect**\. For more information, see [AppStream 2\.0 User Pools](user-pool.md)\.

For step\-by\-step guidance that you can provide your users to help them with connecting to AppStream 2\.0 and starting a streaming session, see [Connect to AppStream 2\.0](client-application-windows-user.md#client-application-windows-start-streaming-session-user)\.