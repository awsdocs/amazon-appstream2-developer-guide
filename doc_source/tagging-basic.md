# Tagging Your Amazon AppStream 2\.0 Resources<a name="tagging-basic"></a>

AWS enables you to assign metadata to your AWS resources in the form of tags\. You can use these tags to help manage your AppStream 2\.0 image builders, images, fleets, and stacks, and also organize data, including billing data\. 

You can:

+ Logically group resources in different ways \(for example, by purpose, owner, or environment\)\.

  This is useful when you have many resources of the same type\.

+ Quickly identify a specific resource based on the tags that you've assigned to it

+ Identify and control AWS costs

For example, you can identify and group AppStream 2\.0 fleets that are in different environments \(such as Development or Production\) or that are assigned to different business units \(such as HR or Marketing\)\. You can then track the associated AWS costs for these fleets on a detailed level\. To do this, sign up to get your AWS account bill with tag key values included\. For more information about setting up a cost allocation report with tags, see [Monthly Cost Allocation Report](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/configurecostallocreport.html) in the *AWS Billing and Cost Management User Guide*\. 

Contents

## Tagging Basics<a name="tagging-introduction"></a>

Tags consist of a key\-value pair, similar to other AWS services tags\. To tag a resource, you specify a *key* and a *value* for each tag\. A key can be a general category, such as "project", "owner", or "environment", with specific associated values, and you can share the same key and value across multiple resources\. You can tag an AppStream 2\.0 resource immediately after you create it or later on\. If you delete a resource, the tags are removed from that resource on deletion\. However, other AppStream 2\.0 and AWS resources that have the same tag key are not impacted\.

You can edit tag keys and values, and you can remove tags from a resource at any time\. You can set the value of a tag to an empty string, but you can't set the name of a tag to null\. If you add a tag that has the same key as an existing tag on that resource, the new value overwrites the old value\. If you delete a resource, any tags for the resource are also deleted\. 

**Note**  
If you plan to set up a monthly cost allocation report to track AWS costs for AppStream 2\.0 resources, keep in mind that tags added to existing AppStream 2\.0 resources appear in your cost allocation report on the first of the following month for resources that are renewed in that month\. 

## Tag Restrictions<a name="tag-restrictions"></a>

+ The maximum number of tags per AppStream 2\.0 resource is 50\.

+ The maximum key length is 128 Unicode characters in UTF\-8\.

+ The maximum value length is 256 Unicode characters in UTF\-8\.

+ Tag keys and values are case\-sensitive\.

+ Do not use the "aws:" prefix in your tag names or values because it is a system tag that is reserved for AWS use\. You cannot edit or delete tag names or values with this prefix\. Tags with this prefix do not count against your tags per resource limit\.

+ You can only use the following special characters: \+ \- = \. \_ : / @\.

+ Although you can share the same key and value across multiple resources, you cannot have duplicate keys on the same resource\.

+ Tags can only be added to resources that are already created \(you cannot specify tags on resource creation\)\.

## Working with Tags in the AppStream 2\.0 Console<a name="basic-tagging-console"></a>

You can add, edit, and delete tags for existing resources by using the AppStream 2\.0 console\. 

**To add, edit, or delete tags for an existing AppStream 2\.0 resource**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. From the navigation bar, select the region that contains the resource for which you want to add, edit, or delete tags\. 

1. In the navigation pane, select the resource type\. The resource type can be an image builder, image, fleet, or stack\.

1. Select the resource from the resource list\. 

1. Choose **Tags**, **Add/Edit Tags**, and then do one or more of the following:

   + To add a tag, choose **Add Tag**, and then specify the key and value for each tag\.

   + To edit a tag, modify the key and value for the tag as needed\.

   + To delete a tag, choose the **Delete** icon \(X\) for the tag\.

1. Choose **Save**\.

## Working with Tags by Using the AppStream 2\.0 API, an AWS SDK, or AWS CLI<a name="basic-tagging-API-SDK-CLI"></a>

If you're using the AppStream 2\.0 API, an AWS SDK or the AWS Command Line Interface \(CLI\), you can use the following AppStream 2\.0 actions to add, edit, remove, or list tags for your resources: 


| Task | AWS CLI | API Action | 
| --- | --- | --- | 
| Add or overwrite one or more tags for a resource\. | [tag\-resource](http://docs.aws.amazon.com/cli/latest/reference/appstream/tag-resource.html)  |  [TagResource](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_TagResource.html)  | 
| Remove one or more tags for a resource\. | [untag\-resource](http://docs.aws.amazon.com/cli/latest/reference/appstream/untag-resource.html) |  [UntagResource](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_UntagResource.html)  | 
| List one or more tags for a resource\. |  [list\-tags\-for\-resource](http://docs.aws.amazon.com/cli/latest/reference/appstream/list-tags-for-resource.html)  |  [ListTagsForResource](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_ListTagsForResource.html)  | 

When you use the AppStream 2\.0 API, an AWS SDK, or AWS CLI actions to add, edit, remove, or list tags for an AppStream 2\.0 resource, specify the resource by using its Amazon Resource Name \(ARN\)\. An ARN uniquely identifies an AWS resource and uses the following general syntax\.

```
arn:aws:appstream:region:account:resourceType/resourceName
```

***region***  
The AWS Region in which the resource was created \(for example, `us-east-1`\)\.

***account***  
The AWS account ID, with no hyphens \(for example, `123456789012`\)\.

***resourceType***  
The type of resource\. You can tag the following AppStream 2\.0 resource types: `image-builder`, `image`, `fleet`, and `stack`\.

***resourceName***  
The name of the resource\.

For example, you can obtain the ARN for an AppStream 2\.0 fleet by using the AWS CLI [describe\-fleets ](http://docs.aws.amazon.com/cli/latest/reference/appstream/describe-fleets.html)command\. Copy the following command\.

```
aws appstream describe-fleets
```

For an environment that contains a single fleet named `TestFleet`, the ARN for this resource would appear in the JSON output similar to the following\. 

```
"Arn": "arn:aws:appstream:us-east-1:123456789012:fleet/TestFleet"
```

After you obtain the ARN for this resource, you can add two tags by using the [tag\-resource](http://docs.aws.amazon.com/cli/latest/reference/appstream/tag-resource.html) command: 

```
aws appstream tag-resource --resource arn:awsappstream:us-east-1:123456789012:fleet/TestFleet --tags Environment=Test,Department=IT
```

The first tag, `Environment=Test`, indicates that the fleet is in a test environment\. The second tag, `Department=IT`, indicates that the fleet is in the IT department\. 

You can use the following command to list the two tags that you added to the fleet\.

```
aws appstream list-tags-for-resource --resource arn:aws:appstream:us-east-1:123456789012:fleet/TestFleet
```

For this example, the JSON output appears as follows: 

```
{
    "Tags": {
       "Environment" : "Test",
       "Department" : "IT"
    }
}
```