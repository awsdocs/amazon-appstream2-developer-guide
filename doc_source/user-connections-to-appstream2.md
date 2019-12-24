# User Connections to Amazon AppStream 2\.0<a name="user-connections-to-appstream2"></a>

Users can connect to AppStream 2\.0 streaming instances through the default public internet endpoint, or by using an interface VPC endpoint \(interface endpoint\) that you create in your virtual private cloud \(VPC\)\. For more information, see [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)\.

By default, AppStream 2\.0 is configured to route streaming connections over the public internet\. Internet connectivity is required to authenticate users and deliver the web assets that AppStream 2\.0 requires to function\. To allow this traffic, you must allow the domains listed in [Allowed Domains](allowed-domains.md)\.

**Note**  
For user authentication, AppStream 2\.0 supports user pools, Security Assertion Markup Language 2\.0 \(SAML 2\.0\), and the [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action\. For more information, see [Authentication of Corporate Users](authentication-authorization.md)\.

The following topics provide information about how to enable user connections to AppStream 2\.0\.

**Topics**
+ [Bandwidth Recommendations](bandwidth-recommendations-user-connections.md)
+ [IP Address and Port Requirements for AppStream 2\.0 User Devices](client-application-ports.md)
+ [Allowed Domains](allowed-domains.md)