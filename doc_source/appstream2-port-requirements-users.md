# Port Requirements for User Connections to Amazon AppStream 2\.0<a name="appstream2-port-requirements-users"></a>

For AppStream 2\.0 users to connect to streaming instances and stream applications, the network that the users' devices are connected to must allow access to certain IP addresses and ports\. 

## Ports for AppStream 2\.0 User Devices<a name="client-application-ports"></a>

AppStream 2\.0 users' devices require outbound access on port 443 \(TCP\), and if you are using DNS servers for domain name resolution, port 53 \(UDP\)\.
+ Port 443 is used for HTTPS communication between AppStream 2\.0 users' devices and streaming instances\. Typically, when end users browse the web during streaming sessions, the web browser randomly selects a source port in the high range for streaming traffic\. You must ensure that return traffic to this port is allowed\.
+ Port 53 is used for communication between AppStream 2\.0 users' devices and your DNS servers\. The port must be open to the IP addresses for your DNS servers so that public domain names can be resolved\. This port is optional if you are not using DNS servers for domain name resolution\. 

## Whitelisted Domains<a name="whitelisted_ports"></a>

For AppStream 2\.0 users to access streaming instances, you must whitelist the following domains on the network from which users are trying to access the streaming instances\.
+ Session Gateway: \*\.amazonappstream\.com
+ CloudFront: \*\.cloudfront\.net

Amazon Web Services \(AWS\) publishes its current IP address ranges, including the ranges that the Session Gateway and CloudFront domains may resolve to, in JSON format\. For information about how to download the \.json file and view the current ranges, see [AWS IP Address Ranges](http://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the Amazon Web Services General Reference\. Or, if you are using AWS Tools for Windows PowerShell, you can access the same information by using the `Get-AWSPublicIpAddressRange` cmdlet\. For more information, see [Querying the Public IP Address Ranges for AWS](https://aws.amazon.com/blogs/developer/querying-the-public-ip-address-ranges-for-aws/)\.