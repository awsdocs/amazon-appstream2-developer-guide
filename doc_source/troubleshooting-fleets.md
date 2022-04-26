# Troubleshooting Fleets<a name="troubleshooting-fleets"></a>

The following are issues that might occur when users connect to Amazon AppStream 2\.0 streaming sessions launched from fleet instances\.

**Topics**
+ [I tried to increase my fleet capacity, but the update isn't taking effect\.](#troubleshooting-fleet-scale-up-policy-not-working-quota-limit-exceeded)
+ [My applications won't work correctly unless I use the Internet Explorer defaults\. How do I restore the Internet Explorer default settings?](#troubleshooting-restore-ie-defaults)
+ [I need to persist environment variables across my fleet instances\.](#troubleshooting-persist-environment-variables)
+ [I want to change the default Internet Explorer home page for my users\.](#troubleshooting-change-homepage)
+ [When my users end a streaming session and then start a new one, they see a message that says no streaming resources are available\.](#troubleshooting-no-resources-available-new-streaming-session)

## I tried to increase my fleet capacity, but the update isn't taking effect\.<a name="troubleshooting-fleet-scale-up-policy-not-working-quota-limit-exceeded"></a>

You can increase your fleet capacity in either of the two following ways:
+ Manually, by increasing the **Minimum capacity** value on the **Scaling Policies **tab for the fleet in the AppStream 2\.0 console\.
+ Automatically, by configuring a fleet scaling policy that manages your capacity for the fleet\.

If your manual modification or scaling policy exceeds your current AppStream 2\.0 quota for your fleet instance type and size, the new values will not take effect\. If you experience this issue, you can use the AWS Command Line Interface \(CLI\) [describe\-scaling\-activities](https://docs.aws.amazon.com/cli/latest/reference/application-autoscaling/describe-scaling-activities.html) command to verify whether your capacity request exceeds your quota for the applicable fleet instance type and size\. This command uses the following format:

```
aws application-autoscaling describe-scaling-activities
  --service-namespace appstream \
  --resource-id fleet/fleetname \
```

For example, the following command provides information for the **TestFleet** fleet in the **us\-west\-2** AWS Region\.

```
aws application-autoscaling describe-scaling-activities --service-namespace appstream --resource-id fleet/TestFleet --region us-west-2
```

The following JSON output shows that a scaling policy for **TestFleet** with a **Minimum capacity** value of 150 was set\. This value exceeds the limit \(quota\) for **TestFleet**, which is 100, so the new scaling policy doesn’t take effect\. In the output, the **StatusMessage** parameter provides detailed information about the cause of the error, including the fleet instance type \(in this case, stream\.standard\.medium\), and the current quota, which is 100\.

**Note**  
AppStream 2\.0 instance type and size quotas are per Amazon Web Services account, per AWS Region\. If you have multiple fleets in the same Region that use the same instance type and size, the total number of instances in all fleets in that Region must be less than or equal to the applicable quota\.

```
{
    "ScalingActivities": [
        {
            "ActivityId": "id",
            "ServiceNamespace": "appstream",
            "ResourceId": "fleet/TestFleet",
            "ScalableDimension": "appstream:fleet:DesiredCapacity",
            "Description": "Setting desired capacity to 150.",
            "Cause": "minimum capacity was set to 150",
            "StartTime": 1596828816.136,
            "EndTime": 1596828816.646,
            "StatusCode": "Failed",
            "StatusMessage": "Failed to set desired capacity to 150. Reason: The Instance type 'stream.standard.medium' capacity limit for fleet TestFleet' was exceeded. Requested: 150, Limit: 100 (Service: AmazonAppStream; Status Code: 400; Error Code: LimitExceededException; Request ID: id; Proxy: null)."
```

If you run the `describe-scaling-activities` command and the output indicates that your capacity request exceeds your current quota, you can resolve the issue by:
+ Changing your capacity request to a value that doesn’t exceed your quota\.
+ Requesting a quota increase\. To request a quota increase, use the [AppStream 2\.0 Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-appstream2)\.

## My applications won't work correctly unless I use the Internet Explorer defaults\. How do I restore the Internet Explorer default settings?<a name="troubleshooting-restore-ie-defaults"></a>

If your AppStream 2\.0 environment includes applications that render elements, you might need to restore the Internet Explorer default settings to enable full enable access to the internet\. 

**To automatically restore the Internet Explorer default settings**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. Choose the image builder on which to restore the Internet Explorer default settings, verify that it is in the **Running** state, and choose **Connect**\.

1. Log in to the image builder by doing either of the following:
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Template User**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, enter the credentials for a domain user who does not have local administrator permissions on the image builder, and then choose **Log in**\.

1. Open Internet Explorer and reset your settings by doing the following:

   1. In the upper right area of the Internet Explorer browser window, choose the **Tools** icon, then choose **Internet options**\.

   1. Choose the **Advanced** tab, and then choose **Reset**\.

   1. When prompted to confirm your choice, choose **Reset** again\.

   1. When the **Reset Internet Explorer Settings** message is displayed, choose **Close**\.

1. In the upper right area of the image builder desktop, choose **Admin Commands**, **Switch User**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/admin-commands-switch-user.png)

1. This disconnects your current session and opens the login menu\. Do either of the following: 
   + If your image builder is not joined to an Active Directory domain, on the **Local User** tab, choose **Administrator**\.
   + If your image builder is joined to an Active Directory domain, choose the **Directory User** tab, and log in as a domain user who has local administrator permissions on the image builder\.

1. On the image builder desktop, open Image Assistant\.

1. Follow the required steps in Image Assistant to finish creating your image\. For more information, see [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

## I need to persist environment variables across my fleet instances\.<a name="troubleshooting-persist-environment-variables"></a>

Environment variables enable you to dynamically pass settings across applications\. You can make user environment variables and system environment variables available across your fleet instances\. You can also create environment variables with limited scope, which is useful when you need to use the same environment variable with different values across different applications\. For more information, see [Persist Environment Variables](customize-fleets.md#customize-fleets-persist-environment-variables)\.

## I want to change the default Internet Explorer home page for my users\.<a name="troubleshooting-change-homepage"></a>

You can use Group Policy to set the default home page in Internet Explorer for your users\. You can also enable users to change the default page that you set\. For more information, see [Change the Default Internet Explorer Home Page for Users' Streaming Sessions](customize-fleets.md#customize-fleets-change-ie-homepage)\.

## When my users end a streaming session and then start a new one, they see a message that says no streaming resources are available\.<a name="troubleshooting-no-resources-available-new-streaming-session"></a>

When a user ends a session, AppStream 2\.0 terminates the underlying instance and creates a new instance if needed to meet the desired capacity of the fleet\. If a user tries to start a new session before AppStream 2\.0 creates the new instance and all other instances are in use, the user will receive an error stating that no streaming resources are available\. If your users start and stop sessions frequently, consider increasing your fleet capacity\. For more information, see [Fleet Auto Scaling for Amazon AppStream 2\.0](autoscaling.md)\. Or, consider increasing the maximum session duration for your fleet and instructing your users to close their browser during periods of inactivity rather than ending their session\.