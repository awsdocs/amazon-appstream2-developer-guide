# Provide Your Users with Access to AppStream 2\.0<a name="accessing-as-user"></a>

Users can access AppStream 2\.0 streaming sessions by using either a web browser or the AppStream 2\.0 client on a supported device\.

Depending on your organizational requirements, you can enable user access to AppStream 2\.0 streaming sessions by: Setting up identity federation using SAML 2\.0, using an AppStream 2\.0 user pool, or creating a streaming URL\. Following are recommendations for choosing a connection method\.
+ [SAML 2\.0](external-identity-providers-setting-up-saml.md): Use this connection method when you have an identity provider that manages your user accounts and supports SAML 2\.0 federation\.
**Note**  
This connection method is required when your AppStream 2\.0 fleet is joined to a Microsoft Active Directory domain\.
+ [AppStream 2\.0 user pools](user-pool.md): Use this connection method when:
  + You want to set up a Proof\-of\-Concept \(POC\) quickly before you configure your SAML 2\.0\-compliant identity provider\.
  + You don't have a SAML 2\.0\-compliant identity provider\.
  + You want to manage users directly within the AppStream 2\.0 console\.
+ [Streaming URL](use-client-start-streaming-session.md#use-client-start-streaming-session-streaming-URL): Use this connection method when you want to programmatically provide access to AppStream 2\.0 by using temporary URLs\. We recommend this connection method when you want to use your existing identity provider to provide programmatic access to AppStream 2\.0

The following topics provide information about how to configure user access to AppStream 2\.0 for application streaming\.

**Topics**
+ [Provide Access Through a Web Browser](access-through-web-browser-admin.md)
+ [Provide Access Through the AppStream 2\.0 Client for Windows](client-application.md)

For guidance that you can provide your users to help them get started with application streaming, see [Guidance for AppStream 2\.0 Users](user-guidance.md)\.