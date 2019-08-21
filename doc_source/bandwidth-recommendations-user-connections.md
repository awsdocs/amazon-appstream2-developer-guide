# Bandwidth Recommendations<a name="bandwidth-recommendations-user-connections"></a>

To optimize the performance of AppStream 2\.0, make sure that your network bandwidth and latency can sustain your users' needs\. 

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