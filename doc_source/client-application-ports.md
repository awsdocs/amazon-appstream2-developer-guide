# IP Address and Port Requirements for AppStream 2\.0 User Devices<a name="client-application-ports"></a>

AppStream 2\.0 users' devices require outbound access on port 443 \(TCP\) when using the internet endpoints, and if you are using DNS servers for domain name resolution, port 53 \(UDP\)\.
+ Port 443 is used for HTTPS communication between AppStream 2\.0 users' devices and streaming instances when using the internet endpoints\. Typically, when end users browse the web during streaming sessions, the web browser randomly selects a source port in the high range for streaming traffic\. You must ensure that return traffic to this port is allowed\.
**Note**  
Streaming through interface VPC endpoints requires additional ports\. For more information, see [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)\.
+ Port 53 is used for communication between AppStream 2\.0 users' devices and your DNS servers\. The port must be open to the IP addresses for your DNS servers so that public domain names can be resolved\. This port is optional if you are not using DNS servers for domain name resolution\. 