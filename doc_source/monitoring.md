# Monitoring Amazon AppStream 2\.0 Resources<a name="monitoring"></a>

AppStream 2\.0 publishes metrics to Amazon CloudWatch to enabled detailed tracking and deep dive analysis\. These statistics are recorded for an extended period so you can access historical information and gain a better perspective on how your fleets are performing\. For more information, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\.

## Viewing Fleet Usage Using the Console<a name="monitoring-console"></a>

You can monitor Amazon AppStream 2\.0 using the AppStream 2\.0 console or the CloudWatch console\.

**To view fleet usage in the AppStream 2\.0 console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left pane, choose **Fleets**\.

1. Select a fleet and choose its **Fleet Usage** tab\.

1. By default, the graph displays the following metrics: `ActualCapacity`, `InUseCapacity`, and `CapacityUtilization`\. You can select additional metrics to graph or change the period\.

**To view fleet usage in the CloudWatch console**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the left pane, choose **Metrics**\.

1. Choose the **AppStream** namespace and then choose **Fleet Metrics**\.

1. Select the metrics to graph\.

## AppStream 2\.0 Metrics and Dimensions<a name="monitoring-with-cloudwatch"></a>

Amazon AppStream 2\.0 sends the following metrics and dimension information to Amazon CloudWatch\.

### Amazon AppStream 2\.0 Metrics<a name="appstream-metrics"></a>

AppStream 2\.0 sends metrics to CloudWatch one time every minute\. The `AWS/AppStream` namespace includes the following metrics\.


| Metric | Description | 
| --- | --- | 
| ActualCapacity |  The total number of instances that are available for streaming or are currently streaming\. <pre>ActualCapacity = AvailableCapacity + InUseCapacity</pre> Units: Count Valid statistics: Average, Minimum, Maximum  | 
|  AvailableCapacity  |  The number of idle instances currently available for user sessions\. <pre>AvailableCapacity = ActualCapacity - InUseCapacity</pre> Units: Count Valid statistics: Average, Minimum, Maximum  | 
| CapacityUtilization |  The percentage of instances in a fleet that are being used, using the following formula\. <pre>CapacityUtilization = (InUseCapacity/ActualCapacity) * 100</pre> Monitoring this metric helps with decisions about increasing or decreasing the value of a fleet's desired capacity\. Units: Percent Valid statistics: Average, Minimum, Maximum  | 
|  DesiredCapacity  |  The total number of instances that are either running or pending\. This represents the total number of concurrent streaming sessions your fleet can support in a steady state\. <pre>DesiredCapacity = ActualCapacity + PendingCapacity</pre> Units: Count Valid statistics: Average, Minimum, Maximum  | 
|  InUseCapacity  |  The number of instances currently being used for streaming sessions\. One `InUseCapacity` count represents one streaming session\. Units: Count Valid statistics: Average, Minimum, Maximum  | 
|  PendingCapacity  |  The number of instances being provisioned by AppStream 2\.0\. Represents the additional number of streaming sessions the fleet can support after provisioning is complete\. When provisioning starts, it usually takes 10\-20 minutes for an instance to become available for streaming\. Units: Count Valid statistics: Average, Minimum, Maximum  | 
| RunningCapacity |  The total number of instances currently running\. Represents the number of concurrent streaming sessions that can be supported by the fleet in its current state\. This metric is provided for Always\-On fleets only, and has the same value as the `ActualCapacity` metric\. Units: Count Valid statistics: Average, Minimum, Maximum  | 
|  InsufficientCapacityError  |  The number of session requests rejected due to lack of capacity\. You can set alarms to use this metric to be notified of users waiting for streaming sessions\. Units: Count Valid statistics: Average, Minimum, Maximum, Sum  | 

### Dimensions for Amazon AppStream 2\.0 Metrics<a name="appstream-dimensions"></a>

To filter the metrics provided by Amazon AppStream 2\.0, use the following dimension\.


| Dimension | Description | 
| --- | --- | 
|  Fleet  |  The name of the fleet\.  | 