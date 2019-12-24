# Infrastructure Security in Amazon AppStream 2\.0<a name="infrastructure-security"></a>

As a managed service, Amazon AppStream 2\.0 is protected by the AWS global network security procedures that are described in the [Amazon Web Services: Overview of Security Processes](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Whitepaper.pdf) whitepaper\.

use published AWS API calls to access AppStream 2\.0 through the network\. Clients must support Transport Layer Security \(TLS\) 1\.0 or later\. We recommend TLS 1\.2 or later\. Clients must also support cipher suites with perfect forward secrecy \(PFS\) such as Ephemeral Diffie\-Hellman \(DHE\) or Elliptic Curve Ephemeral Diffie\-Hellman \(ECDHE\)\. Most modern systems such as Java 7 and later support these modes\.

Additionally, requests must be signed using an access key ID and a secret access key that is associated with an IAM principal\. Or you can use the [AWS Security Token Service](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html) \(AWS STS\) to generate temporary security credentials to sign requests\.

The following topics provide additional information about AppStream 2\.0 infrastructure security\.

**Topics**
+ [Network Isolation](network-isolation.md)
+ [Isolation on Physical Hosts](physical-isolation.md)
+ [Controlling Network Traffic](control-network-traffic.md)
+ [Authentication of Corporate Users](authentication-authorization.md)
+ [AppStream 2\.0 Interface VPC Endpoints](interface-vpc-endpoints.md)
+ [Protecting Data in Transit with FIPS Endpoints](protecting-data-in-transit-FIPS-endpoints.md)