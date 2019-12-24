# Isolation on Physical Hosts<a name="physical-isolation"></a>

Different streaming instances on the same physical host are isolated from each other as though they are on separate physical hosts\. The hypervisor isolates CPU and memory, and the instances are provided virtualized disks instead of access to the raw disk devices\.

When you stop or terminate a streaming instance, the memory allocated to it is scrubbed \(meaning, it's set to zero\) by the hypervisor before it is allocated to a new instance, and every block of storage is reset\. This ensures that your data is not exposed to another instance\. 