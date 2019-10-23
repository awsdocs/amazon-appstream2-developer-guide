# Use the AppStream 2\.0 Client to Start a Streaming Session<a name="use-client-start-streaming-session"></a>

After you install the AppStream 2\.0 client on your local computer, you can use the client to connect to a streaming session\. Use either of the following access methods, as required for your organization:
+ The AppStream 2\.0 API
+ SAML 2\.0 \[single sign\-on \(SSO\)\]
+ User pool 

**AppStream 2\.0 API**

In the AppStream 2\.0 client sign\-in page, enter the streaming URL that you created as the web address, and then choose **Connect**\.

**SAML 2\.0**

If you use SAML 2\.0 to federate your users to an AppStream 2\.0 stack, you must create a registry value to configure the AppStream 2\.0 client with a pre\-populated URL whenever the client is launched\. The URL must use a certificate that is trusted by the device\. The certificate must contain a Subject Alternative Name \(SAN\) that includes the URL's domain name\. For more information, see [Set the Start URL for AppStream 2\.0 Client Users](install-configure-client.md#set-start-url) 

**User pool**

In the AppStream 2\.0 client sign\-in page, enter the URL that was provided in your welcome email, and then choose **Connect**\. 