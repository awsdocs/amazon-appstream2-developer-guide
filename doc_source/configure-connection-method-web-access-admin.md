# Configure a Connection Method for Your AppStream 2\.0 Users \(Web Browser\)<a name="configure-connection-method-web-access-admin"></a>

Depending on your organizational requirements, you can provide users with access to AppStream 2\.0 through a web browser by doing one of the following: Setting up identity federation using SAML 2\.0, using an AppStream 2\.0 user pool, or creating a streaming URL\.

**Topics**
+ [SAML 2\.0](#use-web-browser-start-streaming-session-SAML)
+ [AppStream 2\.0 User Pool](#use-web-browser-start-streaming-session-user-pool)
+ [Streaming URL](#use-web-browser-start-streaming-session-streaming-URL)
+ [Next Steps](#use-web-browser-start-streaming-session-next-steps)

## SAML 2\.0<a name="use-web-browser-start-streaming-session-SAML"></a>

 Users enter the URL that you provide for them to access your internal organizational portal\. After they enter their organizational credentials, they're redirected to AppStream 2\.0\.

For more information, see [Setting Up SAML](external-identity-providers-setting-up-saml.md)\.

**Note**  
If your organization requires a smart card for Windows sign in to Active Directory\-joined streaming instances and in\-session authentication for streaming applications, your users must install and use the AppStream 2\.0 client\. For more information, see [Smart Cards](client-system-requirements-feature-support.md#feature-support-USB-devices-qualified-smart-cards)\.

## AppStream 2\.0 User Pool<a name="use-web-browser-start-streaming-session-user-pool"></a>

When you create a new user in the AppStream 2\.0 user pool, or assign a user pool user to an AppStream 2\.0 stack, AppStream 2\.0 sends email to users on your behalf\. Users enter the URL that was provided to them in the welcome email, enter their credentials, and then choose **Connect**\.

For more information, see [AppStream 2\.0 User Pools](user-pool.md)\.

## Streaming URL<a name="use-web-browser-start-streaming-session-streaming-URL"></a>

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

## Next Steps<a name="use-web-browser-start-streaming-session-next-steps"></a>

After you configure a web browser connection method, you can provide your users with the following step\-by\-step guidance to help them connect to AppStream 2\.0 and start a streaming session: [Connect to AppStream 2\.0](web-browser-user.md#web-browser-start-streaming-session-user)\.