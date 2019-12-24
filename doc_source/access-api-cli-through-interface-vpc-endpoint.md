# Access AppStream 2\.0 API Operations and CLI Commands Through an Interface VPC Endpoint<a name="access-api-cli-through-interface-vpc-endpoint"></a>

If you use Amazon Virtual Private Cloud to host your AWS resources, you can connect directly to AppStream 2\.0 API operations or command line interface \(CLI\) commands through an [interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) \(interface endpoint\) in your virtual private cloud \(VPC\) instead of connecting over the internet\. Interface endpoints are powered by AWS PrivateLink, a technology that lets you keep streaming traffic within a VPC that you specify by using private IP addresses\. When you use an interface endpoint, communication between your VPC and AppStream 2\.0 is conducted entirely and securely within the AWS network\.

**Note**  
This topic describes how to access the AppStream 2\.0 API operations and CLI commands through an interface endpoint\. For information about how to create and stream from AppStream 2\.0 interface endpoints, see [Creating and Streaming from Interface VPC Endpoints](creating-streaming-from-interface-vpc-endpoints.md)\.

**Prerequisites**

To use interface endpoints, you must meet the following prerequisites:
+ The security groups that are associated with the interface endpoint must allow inbound access to port 443 \(TCP\) from the IP address range from which your users connect\.
+ The network access control list for the subnets must allow outbound traffic from ephemeral network ports 1024\-65535 \(TCP\) to the IP address range from which your users connect\.

## Create an Interface Endpoint to Access AppStream 2\.0 API Operations and CLI Commands<a name="access-api-cli-through-interface-vpc-endpoint-create-interface-endpoint"></a>

Perform the following steps to create an interface endpoint\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Endpoints**, **Create Endpoint**\.

1. Choose **Create Endpoint**\.

1. For **Service category**, ensure that** AWS services** is selected\. 

1. For **Service Name**, choose **com\.amazonaws\.***<AWS Region>***\.appstream\.api**\.

1. Specify the following information\. When you're done, choose **Create endpoint**\. 
   + For **VPC**, select a VPC in which to create the interface endpoint\. 
   + For **Subnets**, select the subnets \(Availability Zones\) in which to create the endpoint network interfaces\. We recommend that you choose subnets in at least two Availability Zones\.
   + Optionally, you can select the **Enable Private DNS Name** check box\.
**Note**  
If you select this option, ensure that you configure VPC and DNS as needed to support private DNS\. For more information, see [Private DNS](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-private-dns) in the *Amazon VPC User Guide*\.
   + For **Security group**, select the security groups to associate with the endpoint network interfaces\. 
**Note**  
The security groups must provide inbound access to the ports from the IP address range from which your users connect\.

While your interface endpoint is being created, the status of the endpoint in the console appears as **Pending**\. After your endpoint is created, the status changes to **Available\.**

## Use an Interface Endpoint to Access AppStream 2\.0 API Operations and CLI Commands<a name="how-to-access-api-cli-through-interface-interface-endpoint"></a>

After the status of the interface VPC endpoint that you create changes to **Available**, you can use the endpoint to access AppStream 2\.0 API operations and CLI commands\. To do so, specify the `endpoint-url` parameter with the DNS name of the interface endpoint when you use these operations and commands\. The DNS name is publicly resolvable, but it only successfully routes traffic in your VPC\. 

The following example shows how to specify the DNS name of the interface endpoint when you use the describe\-fleets CLI command:

```
aws appstream describe-fleets --endpoint-url <vpc-endpoint-id>.api.appstream.<aws-region>.vpce.amazonaws.com
```

The following example shows how to specify the DNS name of the interface endpoint when you instantiate the AppStream 2\.0 Boto3 Python client:

```
appstream2client = boto3.client('appstream',region_name='<aws-region>',endpoint_url='<vpc-endpoint-id>.api.appstream.<aws-region>.vpce.amazonaws.com'
```

Subsequent commands using the `appstream2client` object automatically use the interface endpoint that you specified\.

If you enabled the private DNS host names on the interface endpoint, you don’t need to specify the endpoint URL\. The AppStream 2\.0 API DNS host name that the API and CLI use by default resolves within your VPC\. For more information about private DNS host names, see [Private DNS](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-private-dns) in the *Amazon VPC User Guide*\.