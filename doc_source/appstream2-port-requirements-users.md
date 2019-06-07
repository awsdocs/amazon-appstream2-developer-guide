# User Connections to Amazon AppStream 2\.0<a name="appstream2-port-requirements-users"></a>

To optimize the performance of AppStream 2\.0, make sure that your network bandwidth and latency can sustain your users' needs\. To enable AppStream 2\.0 users to connect to streaming instances and stream applications, configure the network to which the users' devices are connected to allow access to certain IP addresses and ports\. 

## Bandwidth Recommendations<a name="bandwidth-recommendations-user-connections"></a>

AppStream 2\.0 uses NICE Desktop Cloud Visualization \(DCV\) to enable your users to securely access and stream your applications over varying network conditions\. To help reduce bandwidth consumption, NICE DCV uses H\.264\-based video compression and encoding\. During streaming sessions, the visual output of applications is compressed and streamed to your users as an AES\-256 encrypted pixel stream over HTTPS\. After the stream is received, it is decrypted and output to your users’ local screen\. When your users interact with their streaming applications, the NICE DCV protocol captures their input and sends it back to their streaming applications over HTTPS\. 

Network conditions are constantly measured during this process and information is sent back to AppStream 2\.0\. AppStream 2\.0 dynamically responds to changing network conditions by changing the video and audio encoding in real time to produce a high\-quality stream for a wide variety of applications and network conditions\.

The recommended bandwidth and latency for AppStream 2\.0 streaming sessions depends on the workload\. For example, a user who works with graphic\-intensive applications to perform computer\-aided design tasks will require more bandwidth and lower latency than a user who works with business productivity applications to write documents\. 

The following table provides guidance on the recommended network bandwidth and latency for AppStream 2\.0 streaming sessions based on common workloads\.

For each workload, the bandwidth recommendation is based on what an individual user might require at a specific point in time\. The recommendation does not reflect the bandwidth required for sustained throughput\. When only a few pixels change on the screen during a streaming session, the sustained throughput is much lower\. Although users who have less bandwidth available can still stream their applications, the frame rate or image quality may not be optimal\.


| Workload | Description | Bandwidth recommended per user | Recommended maximum roundtrip latency | 
| --- | --- | --- | --- | 
| Line of business applications | Document writing applications, database analysis utilities | 2 Mbps | < 150 ms | 
| Graphics applications | Computer\-aided design and modeling applications, photo and video editing | 5 Mbps | < 100 ms | 
| High fidelity | High\-fidelity datasets or maps across multiple monitors | 10 Mbps | < 50 ms | 

## Ports for AppStream 2\.0 User Devices<a name="client-application-ports"></a>

AppStream 2\.0 users' devices require outbound access on port 443 \(TCP\), and if you are using DNS servers for domain name resolution, port 53 \(UDP\)\.
+ Port 443 is used for HTTPS communication between AppStream 2\.0 users' devices and streaming instances\. Typically, when end users browse the web during streaming sessions, the web browser randomly selects a source port in the high range for streaming traffic\. You must ensure that return traffic to this port is allowed\.
+ Port 53 is used for communication between AppStream 2\.0 users' devices and your DNS servers\. The port must be open to the IP addresses for your DNS servers so that public domain names can be resolved\. This port is optional if you are not using DNS servers for domain name resolution\. 

## Whitelisted Domains<a name="whitelisted_ports"></a>

For AppStream 2\.0 users to access streaming instances, you must whitelist the following domain on the network from which users initiate access to the streaming instances\.
+ Session Gateway: \*\.amazonappstream\.com

One or more of the following domains must be whitelisted to enable user authentication\. You must whitelist the domains that correspond to the Regions where AppStream 2\.0 is deployed\. 


| Region | Domain | 
| --- | --- | 
| N\. Virginia | appstream2\.us\-east\-1\.aws\.amazon\.com | 
| Oregon | appstream2\.us\-west\-2\.aws\.amazon\.com | 
| Tokyo | appstream2\.ap\-northeast\-1\.aws\.amazon\.com | 
| Seoul | appstream2\.ap\-northeast\-2\.aws\.amazon\.com | 
| Singapore | appstream2\.ap\-southeast\-1\.aws\.amazon\.com | 
| Sydney | appstream2\.ap\-southeast\-2\.aws\.amazon\.com | 
| Frankfurt | appstream2\.eu\-central\-1\.aws\.amazon\.com | 
| Ireland | appstream2\.eu\-west\-1\.aws\.amazon\.com | 

Amazon Web Services \(AWS\) publishes its current IP address ranges, including the ranges that the Session Gateway and CloudFront domains may resolve to, in JSON format\. For information about how to download the \.json file and view the current ranges, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the Amazon Web Services General Reference\. Or, if you are using AWS Tools for Windows PowerShell, you can access the same information by using the `Get-AWSPublicIpAddressRange` cmdlet\. For more information, see [Querying the Public IP Address Ranges for AWS](https://aws.amazon.com/blogs/developer/querying-the-public-ip-address-ranges-for-aws/)\.