# Amazon AppStream 2\.0 Connections to Your VPC<a name="appstream2-port-requirements-appstream2"></a>

To enable AppStream 2\.0 connectivity to network resources and the internet, configure your streaming instances as follows\.

## Network Interfaces<a name="network-interfaces"></a>

Each AppStream 2\.0 streaming instance has the following network interfaces:
+ The customer network interface provides connectivity to the resources within your VPC, as well as the internet, and is used to join the streaming instance to your directory\.
+ The management network interface is connected to a secure AppStream 2\.0 management network\. It is used for interactive streaming of the streaming instance to a user's device, and to allow AppStream 2\.0 to manage the streaming instance\.

AppStream 2\.0 selects the IP address for the management network interface from the following private IP address range: 198\.19\.0\.0/16\. Do not use this range for your VPC CIDR or peer your VPC with another VPC with this range, as this might create a conflict and cause streaming instances to be unreachable\. Also, do not modify or delete any of the network interfaces attached to a streaming instance, as this might also cause the streaming instance to become unreachable\.

## Management Network Interface IP Address Range and Ports<a name="management_ports"></a>

The management network interface IP address range is 198\.19\.0\.0/16\. The following ports must be open on the management network interface of all streaming instances:
+ Inbound TCP on port 8300\. This is used for establishment of the streaming connection\.
+ Inbound TCP on ports 8000 and 8443\. These are used for management of the streaming instance by AppStream 2\.0\.

Limit the inbound range on the management network interface to 198\.19\.0\.0/16\.

Under normal circumstances, AppStream 2\.0 correctly configures these ports for your streaming instances\. If any security or firewall software is installed on a streaming instance that blocks any of these ports, the streaming instance may not function correctly or may be unreachable\.

Do not disable IPv6\. If you disable IPv6, AppStream 2\.0 will not function correctly\. For information about configuring IPv6 for Windows, see [Guidance for configuring IPv6 in Windows for advanced users](https://support.microsoft.com/en-us/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users)\.

**Note**  
AppStream 2\.0 relies on the DNS servers within your VPC to return a non\-existent domain \(NXDOMAIN\) response for local domain names that don’t exist\. This enables the AppStream 2\.0\-managed network interface to communicate with the management servers\.   
When you create a directory with Simple AD, AWS Directory Service creates two domain controllers that also function as DNS servers on your behalf\. Because the domain controllers don't provide the NXDOMAIN response, they can't be used with AppStream 2\.0\.

## Customer Network Interface Ports<a name="primary_ports"></a>
+ For internet connectivity, the following ports must be open to all destinations\. If you are using a modified or custom security group, you need to add the required rules manually\. For more information, see [Security Group Rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#SecurityGroupRules) in the *Amazon VPC User Guide*\. 
  + TCP 80 \(HTTP\)
  + TCP 443 \(HTTPS\)
+ If you join your streaming instances to a directory, the following ports must be open between your AppStream 2\.0 VPC and your directory controllers\. 
  + TCP/UDP 53 \- DNS
  + TCP/UDP 88 \- Kerberos authentication
  + UDP 123 \- NTP
  + TCP 135 \- RPC
  + UDP 137\-138 \- Netlogon
  + TCP 139 \- Netlogon
  + TCP/UDP 389 \- LDAP
  + TCP/UDP 445 \- SMB
  + TCP 1024\-65535 \- Dynamic ports for RPC

  For a complete list of ports, see [Active Directory and Active Directory Domain Services Port Requirements](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772723(v=ws.10)) in the Microsoft documentation\.
+ All streaming instances require that port 80 \(HTTP\) be open to IP address `169.254.169.254` to allow access to the EC2 metadata service\. Any HTTP proxy assigned to your streaming instances must exclude `169.254.169.254`\.