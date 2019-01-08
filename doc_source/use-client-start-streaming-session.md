# Use the AppStream 2\.0 Client to Start a Streaming Session<a name="use-client-start-streaming-session"></a>

After you install the AppStream 2\.0 client on your local computer, you can use the client to connect to a streaming session\. Use either of the following access methods, as required for your organization:
+ The AppStream 2\.0 API
+ SAML 2\.0 \[single sign\-on \(SSO\)\]

**AppStream 2\.0 API**

In the AppStream 2\.0 client sign\-in page, enter the streaming URL that you created as the web address, and then choose **Connect**\.

**SAML 2\.0**

If you use SAML 2\.0 to federate your users to an AppStream 2\.0 stack, you must create a registry value to configure the AppStream 2\.0 client to automatically connect to a start URL whenever the client is launched\. For more information, see [Run a PowerShell Script to Install the AppStream 2\.0 Client](install-configure-client.md#configure-start-url-remotely-use-powershell) 