# Fleet Auto Scaling for Amazon AppStream 2\.0<a name="autoscaling"></a>

Fleet Auto Scaling lets you change the size of your AppStream 2\.0 fleet automatically to match the supply of available instances to user demand\. Because one user requires one fleet instance, the size of your fleet determines the number of users who can stream concurrently\. You can define scaling policies that adjust the size of your fleet automatically based on a variety of utilization metrics, and optimize the number of available instances to match user demand\. You can also choose to turn off automatic scaling and make the fleet run at a fixed size\.

**Note**  
As you develop your plan for AppStream 2\.0 fleet scaling, make sure that your network configuration meets your requirements\. For larger deployments that require hundreds or thousands of fleet instances and involve unpredictable user demand, Fleet Auto Scaling may not be the best solution\. For information about how to configure a network environment that supports effective fleet scaling and considerations for larger deployments, see [VPC Setup Recommendations](vpc-setup-recommendations.md)\.

Before you can use Fleet Auto Scaling, Application Auto Scaling needs permissions to access Amazon CloudWatch alarms and AppStream 2\.0 fleets\. For more information, see [Network Access to Your Streaming InstanceUsing AWS Managed Policies and Linked Roles to Manage Administrator Access to AppStream 2\.0 Resources](controlling-administrator-access-with-policies-roles.md) and [Using IAM Policies to Manage Administrator Access to Application Auto Scaling](autoscaling-iam-policy.md)\.

**Note**  
When you use scaling, you work with the Application Auto Scaling API\. For Fleet Auto Scaling to work correctly for AppStream 2\.0, Application Auto Scaling requires permission to describe and update your AppStream 2\.0 fleets and describe your Amazon CloudWatch alarms, and permissions to modify your fleet capacity on your behalf\. For more information, see [Roles Required for AppStream 2\.0 and Application Auto Scaling](roles-required-for-appstream.md) and [Using IAM Policies to Manage Administrator Access to Application Auto Scaling](autoscaling-iam-policy.md)\.

The following topics provide information to help you understand and use AppStream 2\.0 Fleet Auto Scaling\. 

**Topics**
+ [Scaling Concepts](#autoscaling-concepts)
+ [Managing Fleet Scaling Using the Console](#autoscaling-console)
+ [Managing Fleet Scaling Using the AWS CLI](#autoscaling-cli)
+ [Additional Resources](#autoscaling-additional-resources)

## Scaling Concepts<a name="autoscaling-concepts"></a>

AppStream 2\.0 scaling is provided by Application Auto Scaling\. For more information, see the [Application Auto Scaling API Reference](https://docs.aws.amazon.com/autoscaling/application/APIReference/)\.

For step\-by\-step guidance for working with AppStream 2\.0 Fleet Auto Scaling, see [Scaling Your Desktop Application Streams with Amazon AppStream 2\.0](http://aws.amazon.com/blogs/compute/scaling-your-desktop-application-streams-with-amazon-appstream-2-0/) in the *AWS Compute Blog*\.

To use Fleet Auto Scaling effectively, you must understand the following terms and concepts\.

**Minimum Capacity**  
The minimum number of fleet instances\. The number of fleet instances can't be below this value, and scaling policies will not scale your fleet below this value\. For example, if you set the minimum capacity for a fleet to 2, your fleet will never have less than 2 instances\.

**Maximum Capacity**  
The maximum number of fleet instances\. The number of fleet instances can't be above this value, and scaling policies will not scale your fleet above this value\. For example, if you set the maximum capacity for a fleet to 10, your fleet will never have more than 10 instances\.

**Desired Capacity**  
The total number of fleet instances that are either running or pending\. This value represents the total number of concurrent streaming sessions that your fleet can support in a steady state\. To set the value for **Desired Capacity**, edit **Fleet Details**\. We do not recommend changing the **Desired Capacity** value manually when you use **Scaling Policies**\.   
If the value of **Desired Capacity** is set below the value of **Minimum Capacity** and a scale\-out activity is triggered, Application Auto Scaling scales the **Desired Capacity** value up to the value of **Minimum Capacity** and then continues to scale out as required, based on the scaling policy\. However, in this case, a scale\-in activity does not adjust **Desired Capacity**, because it is already below the **Minimum Capacity** value\.   
If the value of **Desired Capacity** is set above the value of **Maximum Capacity** and a scale\-in activity is triggered, Application Auto Scaling scales the **Desired Capacity** value down to the value of **Maximum Capacity** and then continues to scale in as required, based on the scaling policy\. However, in this case, a scale\-out activity does not adjust **Desired Capacity**, because it is already above the **Maximum Capacity** value\.

**Scaling Policy Action**  
The action that scaling policies perform on your fleet when the **Scaling Policy Condition** is met\. You can choose an action based on **% capacity** or **number of instance\(s\)**\. For example, if **Desired Capacity** is 4 and **Scaling Policy Action** is set to "Add 25% capacity", **Desired Capacity** is increased by 25% to 5 when **Scaling Policy Condition** is met\.

**Scaling Policy Condition**  
The condition that triggers the action set in **Scaling Policy Action**\. This condition includes a scaling policy metric, a comparison operator, and a threshold\. For example, to scale a fleet if the utilization of the fleet is greater than 50%, your scaling policy condition should be "If Capacity Utilization > 50%"\.

**Scaling Policy Metric**  
Your scaling policy is based on this metric\. The following metrics are available for scaling policies:    
**Capacity Utilization**  
The percentage of instances in a fleet that are being used\. You can use this metric to scale your fleet based on usage of the fleet\. For example, **Scaling Policy Condition**: "If Capacity Utilization < 25%" perform **Scaling Policy Action**: "Remove 25 % capacity"\.  
**Available Capacity**  
The number of instances in your fleet that are available for user sessions\. You can use this metric to maintain a buffer in your capacity available for users to start streaming sessions\. For example, **Scaling Policy Condition**: "If Available Capacity < 5" perform **Scaling Policy Action**: "Add 5 instance\(s\)"\.  
**Insufficient Capacity Error**  
The number of session requests rejected due to lack of capacity\. You can use this metric to provision new instances for users who can't start streaming sessions due to lack of capacity\. For example, **Scaling Policy Condition**: "If Insufficient Capacity Error > 0" perform **Scaling Policy Action**: "Add 1 instance\(s\)"\.

## Managing Fleet Scaling Using the Console<a name="autoscaling-console"></a>

You can set up and manage fleet scaling by using the AppStream 2\.0 console in either of the following two ways: During fleet creation, or any time, by using the **Fleets** tab\. Two default scaling policies are associated with newly created fleets after launch\. You can edit these policies on the **Scaling Policies** tab in the AppStream 2\.0 console\. For more information, see [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

For user environments that vary in number, define scaling policies to control how scaling responds to demand\. If you expect a fixed number of users or have other reasons for disabling scaling, you can set your fleet with a fixed number of instances\.

**To set a fleet scaling policy using the console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Fleets**\. 

1. Select the fleet and then choose **Scaling Policies**\.

1. Edit existing policies by choosing the edit icon next to each value\. Set the desired values in the edit field and choose **Update**\. The policy changes go into effect within a few minutes\.

1. Add \(create\) new policies using the **Add Policy** link\. Set the desired values in the edit field and choose **Create**\. The new policy goes into effect within a few minutes\.

You can use the **Fleet Usage** tab to monitor the effects of your scaling policy changes\. The following is an example usage graph of scaling activity when five users connect to the fleet and then disconnect\. This example is from a fleet using the following scaling policy values:
+ Minimum Capacity = 1
+ Maximum Capacity = 5
+ Scale Out = Add 2 instances if Capacity Utilization > 75%
+ Scale In = Remove 1 instance if Capacity Utilization < 25%

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/scaling-graph.png)

**To set a fixed capacity fleet using the console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Fleets**\.

1. Select the fleet\.

1. For **Scaling Policies**, remove all policies associated with the fleet\.

1. For **Fleet Details**, edit the fleet to set **Desired Capacity**\.

The fixed fleet has constant capacity based on the value that you specified as **Desired Capacity**\. Note that a fixed fleet has the desired number of instances available at all times and the fleet must be stopped to stop billing costs for that fleet\.

## Managing Fleet Scaling Using the AWS CLI<a name="autoscaling-cli"></a>

You can set up and manage fleet scaling by using the AWS Command Line Interface \(AWS CLI\)\. For more advanced features such as setting up multiple scaling policies or setting scale\-in and scale\-out cooldown times, use the AWS CLI\. Before running scaling policy commands, you must register your fleet as a scalable target\. To do so, use the following [register\-scalable\-target](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling/register-scalable-target.html) command:

```
aws application-autoscaling register-scalable-target
  --service-namespace appstream \
  --resource-id fleet/fleetname \
  --scalable-dimension appstream:fleet:DesiredCapacity \
  --min-capacity 1 --max-capacity 5
```

**Topics**
+ [Example 1: Applying a Scaling Policy Based on Capacity Utilization](#autoscaling-cli-utilization)
+ [Example 2: Applying a Scaling Policy Based on Insufficient Capacity Errors](#autoscaling-cli-capacity)
+ [Example 3: Applying a Scaling Policy Based on Low Capacity Utilization](#autoscaling-cli-scale-in)
+ [Example 4: Change the Fleet Capacity Based on a Schedule](#autoscaling-cli-schedule)
+ [Example 5: Applying a Target Tracking Scaling Policy](#autoscaling-target-tracking)

### Example 1: Applying a Scaling Policy Based on Capacity Utilization<a name="autoscaling-cli-utilization"></a>

This AWS CLI example sets up a scaling policy that scales out a fleet by 25% if Utilization >= 75%\.

The following [put\-scaling\-policy](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling/put-scaling-policy.html) command defines a utilization\-based scaling policy:

```
aws application-autoscaling put-scaling-policy --cli-input-json file://scale-out-utilization.json
```

The contents of the file `scale-out-utilization.json` are as follows:

```
{
    "PolicyName": "policyname",
    "ServiceNamespace": "appstream",
    "ResourceId": "fleet/fleetname",
    "ScalableDimension": "appstream:fleet:DesiredCapacity",
    "PolicyType": "StepScaling",
    "StepScalingPolicyConfiguration": {
        "AdjustmentType": "PercentChangeInCapacity",
        "StepAdjustments": [
            {
                "MetricIntervalLowerBound": 0,
                "ScalingAdjustment": 25
            }
        ],
        "Cooldown": 120
    }
}
```

If the command is successful, the output is similar to the following, although some details are unique to your account and Region\. In this example, the policy identifier is `e3425d21-16f0-d701-89fb-12f98dac64af`\.

```
{"PolicyARN": "arn:aws:autoscaling:us-west-2:123456789012:scalingPolicy:e3425d21-16f0-d701-89fb-12f98dac64af:resource/appstream/fleet/SampleFleetName:policyName/scale-out-utilization-policy"}
```

Now, set up a CloudWatch alarm for this policy\. Use the names, Region, account number, and policy identifier that apply to you\. You can use the policy ARN returned by the previous command for the `--alarm-actions` parameter\.

```
aws cloudwatch put-metric-alarm 
--alarm-name alarmname \
--alarm-description "Alarm when Capacity Utilization exceeds 75 percent" \
--metric-name CapacityUtilization \
--namespace AWS/AppStream \
--statistic Average \
--period 300 \
--threshold 75 \
--comparison-operator GreaterThanOrEqualToThreshold \
--dimensions "Name=Fleet,Value=fleetname" \
--evaluation-periods 1 --unit Percent \
--alarm-actions "arn:aws:autoscaling:your-region-code:account-number-without-hyphens:scalingPolicy:policyid:resource/appstream/fleet/fleetname:policyName/policyname"
```

### Example 2: Applying a Scaling Policy Based on Insufficient Capacity Errors<a name="autoscaling-cli-capacity"></a>

This AWS CLI example sets up a scaling policy that scales out the fleet by 1 if the fleet returns an `InsufficientCapacityError` error\.

The following command defines a insufficient capacity\-based scaling policy:

```
aws application-autoscaling put-scaling-policy --cli-input-json file://scale-out-capacity.json
```

The contents of the file `scale-out-capacity.json` are as follows:

```
{
    "PolicyName": "policyname",
    "ServiceNamespace": "appstream",
    "ResourceId": "fleet/fleetname",
    "ScalableDimension": "appstream:fleet:DesiredCapacity",
    "PolicyType": "StepScaling",
    "StepScalingPolicyConfiguration": {
        "AdjustmentType": "ChangeInCapacity",
        "StepAdjustments": [
            {
                "MetricIntervalLowerBound": 0,
                "ScalingAdjustment": 1
            }
        ],
        "Cooldown": 120
    }
}
```

If the command is successful, the output is similar to the following, although some details are unique to your account and Region\. In this example, the policy identifier is `f4495f21-0650-470c-88e6-0f393adb64fc`\.

```
{"PolicyARN": "arn:aws:autoscaling:us-west-2:123456789012:scalingPolicy:f4495f21-0650-470c-88e6-0f393adb64fc:resource/appstream/fleet/SampleFleetName:policyName/scale-out-insufficient-capacity-policy"}
```

Now, set up a CloudWatch alarm for this policy\. Use the names, Region, account number, and policy identifier that apply to you\. You can use the policy ARN returned by the previous command for the `--alarm-actions` parameter\.

```
aws cloudwatch put-metric-alarm 
--alarm-name alarmname \
--alarm-description "Alarm when out of capacity is > 0" \
--metric-name InsufficientCapacityError \
--namespace AWS/AppStream \
--statistic Maximum \
--period 300 \
--threshold 0 \
--comparison-operator GreaterThanThreshold \
--dimensions "Name=Fleet,Value=fleetname" \
--evaluation-periods 1 --unit Count \
--alarm-actions "arn:aws:autoscaling:your-region-code:account-number-without-hyphens:scalingPolicy:policyid:resource/appstream/fleet/fleetname:policyName/policyname"
```

### Example 3: Applying a Scaling Policy Based on Low Capacity Utilization<a name="autoscaling-cli-scale-in"></a>

This AWS CLI example sets up a scaling policy that scales in the fleet to reduce actual capacity when `CapacityUtilization` is low\.

The following command defines an excess capacity\-based scaling policy:

```
aws application-autoscaling put-scaling-policy --cli-input-json file://scale-in-capacity.json
```

The contents of the file `scale-in-capacity.json` are as follows:

```
{
    "PolicyName": "policyname",
    "ServiceNamespace": "appstream",
    "ResourceId": "fleet/fleetname",
    "ScalableDimension": "appstream:fleet:DesiredCapacity",
    "PolicyType": "StepScaling",
    "StepScalingPolicyConfiguration": {
        "AdjustmentType": "PercentChangeInCapacity",
        "StepAdjustments": [
            {
                "MetricIntervalUpperBound": 0,
                "ScalingAdjustment": -25
            }
        ],
        "Cooldown": 360
    }
}
```

If the command is successful, the output is similar to the following, although some details are unique to your account and Region\. In this example, the policy identifier is `12ab3c4d-56789-0ef1-2345-6ghi7jk8lm90`\.

```
{"PolicyARN": "arn:aws:autoscaling:us-west-2:123456789012:scalingPolicy:12ab3c4d-56789-0ef1-2345-6ghi7jk8lm90:resource/appstream/fleet/SampleFleetName:policyName/scale-in-utilization-policy"}
```

Now, set up a CloudWatch alarm for this policy\. Use the names, Region, account number, and policy identifier that apply to you\. You can use the policy ARN returned by the previous command for the `--alarm-actions` parameter\.

```
aws cloudwatch put-metric-alarm 
--alarm-name alarmname \
--alarm-description "Alarm when Capacity Utilization is less than or equal to 25 percent" \
--metric-name CapacityUtilization \
--namespace AWS/AppStream \
--statistic Average \
--period 120 \
--threshold 25 \
--comparison-operator LessThanOrEqualToThreshold \
--dimensions "Name=Fleet,Value=fleetname" \
--evaluation-periods 10 --unit Percent \
--alarm-actions "arn:aws:autoscaling:your-region-code:account-number-without-hyphens:scalingPolicy:policyid:resource/appstream/fleet/fleetname:policyName/policyname"
```

### Example 4: Change the Fleet Capacity Based on a Schedule<a name="autoscaling-cli-schedule"></a>

Changing your fleet capacity based on a schedule lets you scale your fleet capacity in response to predictable changes in demand\. For example, at the start of a work day, you might expect a certain number of users to request streaming connections at one time\. To change your fleet capacity based on a schedule, you can use the Application Auto Scaling [PutScheduledAction](https://docs.aws.amazon.com/autoscaling/application/APIReference/API_PutScheduledAction.html) API action or the [put\-scheduled\-action](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling/put-scheduled-action.html) AWS CLI command\.

Before changing your fleet capacity, you can list your current fleet capacity by using the AppStream 2\.0 [describe\-fleets](https://docs.aws.amazon.com/cli/latest/reference/appstream/describe-fleets.html) AWS CLI command\.

```
aws appstream describe-fleets --name fleetname
```

The current fleet capacity will appear similar to the following output \(shown in JSON format\):

```
{
    {
            "ComputeCapacityStatus": {
                "Available": 1,
                "Desired": 1,
                "Running": 1,
                "InUse": 0
            },
}
```

Then, use the `put-scheduled-action` command to create a scheduled action to change your fleet capacity\. For example, the following command changes the minimum capacity to 3 and the maximum capacity to 5 every day at 9:00 AM UTC\.

**Note**  
For cron expressions, specify when to perform the action in UTC\. For more information, see [Cron Expressions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html#CronExpressions)\.

```
aws application-autoscaling put-scheduled-action --service-namespace appstream \
--resource-id fleet/fleetname \
--schedule="cron(0 9 * * ? *)" \
--scalable-target-action MinCapacity=3,MaxCapacity=5 \
--scheduled-action-name ExampleScheduledAction \
--scalable-dimension appstream:fleet:DesiredCapacity
```

To confirm that the scheduled action to change your fleet capacity was successfully created, run the [describe\-scheduled\-actions](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling/describe-scheduled-actions.html) command\.

```
aws application-autoscaling describe-scheduled-actions --service-namespace appstream --resource-id fleet/fleetname
```

If the scheduled action was successfully created, the output appears similar to the following\.

```
{
    "ScheduledActions": [
        {
            "ScalableDimension": "appstream:fleet:DesiredCapacity",
            "Schedule": "cron(0 9 * * ? *)",
            "ResourceId": "fleet/ExampleFleet",
            "CreationTime": 1518651232.886,
            "ScheduledActionARN": "<arn>",
            "ScalableTargetAction": {
                "MinCapacity": 3,
                "MaxCapacity": 5
            },
            "ScheduledActionName": "ExampleScheduledAction",
            "ServiceNamespace": "appstream"
        }
    ]
}
```

For more information, see [Scheduled Scaling](https://docs.aws.amazon.com/autoscaling/application/userguide/application-auto-scaling-scheduled-scaling.html) in the *Application Auto Scaling User Guide*\.

### Example 5: Applying a Target Tracking Scaling Policy<a name="autoscaling-target-tracking"></a>

With target tracking scaling, you can specify a capacity utilization level for your fleet\. 

When you create a target tracking scaling policy, Application Auto Scaling automatically creates and manages CloudWatch alarms that trigger the scaling policy\. The scaling policy adds or removes capacity as required to keep capacity utilization at, or close to, the specified target value\. To ensure application availability, your fleet scales out proportionally to the metric as fast as it can but scales in more gradually\.

The following [put\-scaling\-policy](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling/put-scaling-policy.html) command defines a target tracking scaling policy that attempts to maintain 75% capacity utilization for an AppStream 2\.0 fleet\.

```
aws application-autoscaling put-scaling-policy --cli-input-json file://config.json
```

The contents of the file `config.json` are as follows:

```
{
  "PolicyName":"target-tracking-scaling-policy",
  "ServiceNamespace":"appstream",
  "ResourceId":"fleet/fleetname",
  "ScalableDimension":"appstream:fleet:DesiredCapacity",
  "PolicyType":"TargetTrackingScaling",
  "TargetTrackingScalingPolicyConfiguration":{
    "TargetValue":75.0,
    "PredefinedMetricSpecification":{
      "PredefinedMetricType":"AppStreamAverageCapacityUtilization"
    },
    "ScaleOutCooldown":300,
    "ScaleInCooldown":300
  }
}
```

If the command is successful, the output is similar to the following, although some details are unique to your account and Region\. In this example, the policy identifier is 6d8972f3\-efc8\-437c\-92d1\-6270f29a66e7\.

```
{
    "PolicyARN": "arn:aws:autoscaling:us-west-2:123456789012:scalingPolicy:6d8972f3-efc8-437c-92d1-6270f29a66e7:resource/appstream/fleet/fleetname:policyName/target-tracking-scaling-policy",
    "Alarms": [
        {
            "AlarmARN": "arn:aws:cloudwatch:us-west-2:123456789012:alarm:TargetTracking-fleet/fleetname-AlarmHigh-d4f0770c-b46e-434a-a60f-3b36d653feca",
            "AlarmName": "TargetTracking-fleet/fleetname-AlarmHigh-d4f0770c-b46e-434a-a60f-3b36d653feca"
        },
        {
            "AlarmARN": "arn:aws:cloudwatch:us-west-2:123456789012:alarm:TargetTracking-fleet/fleetname-AlarmLow-1b437334-d19b-4a63-a812-6c67aaf2910d",
            "AlarmName": "TargetTracking-fleet/fleetname-AlarmLow-1b437334-d19b-4a63-a812-6c67aaf2910d"
        }
    ]
}
```

For more information, see [Target Tracking Scaling Policies](https://docs.aws.amazon.com/autoscaling/application/userguide/application-auto-scaling-target-tracking.html) in the *Application Auto Scaling User Guide*\.

## Additional Resources<a name="autoscaling-additional-resources"></a>

For step\-by\-step guidance for working with AppStream 2\.0 Fleet Auto Scaling, see [Scaling Your Desktop Application Streams with Amazon AppStream 2\.0](http://aws.amazon.com/blogs/compute/scaling-your-desktop-application-streams-with-amazon-appstream-2-0/) in the *AWS Compute Blog*\.

To learn more about using the Application Auto Scaling AWS CLI commands or API actions, see the following resources:
+ [application\-autoscaling](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling) section of the *AWS CLI Command Reference*
+ [Application Auto Scaling API Reference](https://docs.aws.amazon.com/autoscaling/application/APIReference/)
+ [Application Auto Scaling User Guide](https://docs.aws.amazon.com/autoscaling/application/userguide/)