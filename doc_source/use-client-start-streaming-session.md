# Configure a Connection Method for Your AppStream 2\.0 Client Users<a name="use-client-start-streaming-session"></a>

After you install the AppStream 2\.0 client on your users' local computers, they can use the AppStream 2\.0 client to connect to a streaming session\. Depending on your organizational requirements, you can provide client users with access to AppStream 2\.0 by doing one of the following: Setting up identity federation using SAML 2\.0, using an AppStream 2\.0 user pool, or creating a streaming URL\.

**Topics**
+ [SAML 2\.0](#use-client-start-streaming-session-SAML)
+ [AppStream 2\.0 User Pool](#use-client-start-streaming-session-user-pool)
+ [Streaming URL](#use-client-start-streaming-session-streaming-URL)
+ [Next Steps](#use-client-start-streaming-session-next-steps)

## SAML 2\.0<a name="use-client-start-streaming-session-SAML"></a>

If you use external identity providers to federate your users to an AppStream 2\.0 stack, you must create a registry value to configure the AppStream 2\.0 client with a prepopulated URL whenever the client is launched\. The URL must use a certificate that is trusted by the device\. The certificate must contain a Subject Alternative Name \(SAN\) that includes the URL's domain name\.

For more information, see:
+ [Setting Up SAML](external-identity-providers-setting-up-saml.md)
+ [Set the StartURL Registry Value for AppStream 2\.0 Client Users](install-client-configure-settings.md#set-start-url-registry-value)

## AppStream 2\.0 User Pool<a name="use-client-start-streaming-session-user-pool"></a>

When you create a new user in the AppStream 2\.0 user pool, or assign a user pool user to an AppStream 2\.0 stack, AppStream 2\.0 sends email to users on your behalf\. Users enter the URL that was provided to them in the welcome email, enter their credentials, and then choose **Connect**\.

For more information, see [AppStream 2\.0 User Pools](user-pool.md)\.

## Streaming URL<a name="use-client-start-streaming-session-streaming-URL"></a>

To create a streaming URL, use one of the following methods:
+ AppStream 2\.0 console
+ The [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action 
+ The [create\-streaming\-url](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-streaming-url.html) AWS CLI command

To create a streaming URL by using the AppStream 2\.0 console, complete the steps in the following procedure\.

**To create a streaming URL by using the AppStream 2\.0 console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Fleets**\.

1. In the list of fleets, choose the fleet that is associated with the stack for which you want to create a streaming URL\. Verify that the status of the fleet is **Running**\.

1. In the navigation pane, choose **Stacks**\. Choose the stack, and then choose **Actions**, **Create streaming URL**\.

1. In **User id**, enter the user ID\.

1. For **URL Expiration**, choose an expiration time, which determines how long the generated URL is valid\. This URL is valid for a maximum of seven days\.

1. Choose **Get URL**\.

1. Copy the URL, save it to an accessible location, and then provide it to your users\.

   In the AppStream 2\.0 client sign\-in page, users enter the streaming URL that you created as the web address, and then choose **Connect**\. 

## Next Steps<a name="use-client-start-streaming-session-next-steps"></a>

After you configure a client connection method, you can provide your users with the following step\-by\-step guidance to help them connect to AppStream 2\.0 and start a streaming session: [Connect to AppStream 2\.0](client-application-windows-user.md#client-application-windows-start-streaming-session-user)\.