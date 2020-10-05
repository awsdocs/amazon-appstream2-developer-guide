# Configure a Connection Method for Your AppStream 2\.0 Users \(Web Browser\)<a name="configure-connection-method-web-access-admin"></a>

You can configure one or more of the following connection methods for users who access AppStream 2\.0 through a web browser\.

**Streaming URL**

Users enter the streaming URL that you create as the web address to sign in to AppStream 2\.0\. To create a streaming URL, use one of the following methods:
+ AppStream 2\.0 console
+ The [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action 
+ The [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream;create-streaming-url.html) AWS CLI command

**SAML 2\.0**

Users enter the URL that you provide for them to access your internal organizational portal\. After they enter their organizational credentials, they are redirected to AppStream 2\.0\. For more information, see [Set the StartURL Registry Value for AppStream 2\.0 Client Users](install-client-configure-settings.md#set-start-url-registry-value)\.

**AppStream 2\.0 user pool**

When you create a new user in the AppStream 2\.0 user pool, or asssign a user pool user to an AppStream 2\.0 stack, AppStream 2\.0 sends email to users on your behalf\. Users enter the URL that was provided to them in the welcome email, enter their credentials, and then choose **Connect**\. For information about how to add a user to the AppStream 2\.0 user pool, see [AppStream 2\.0 User Pools](user-pool.md)\.

For step\-by\-step guidance that you can provide your users to help them with connecting to AppStream 2\.0 and starting a streaming session, see [Connect to AppStream 2\.0](web-browser-user.md#web-browser-start-streaming-session-user)\.