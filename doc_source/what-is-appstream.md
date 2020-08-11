# What Is Amazon AppStream 2\.0?<a name="what-is-appstream"></a>

Amazon AppStream 2\.0 is a fully managed application streaming service that provides users with instant access to their desktop applications from anywhere\. AppStream 2\.0 manages the AWS resources required to host and run your applications, scales automatically, and provides access to your users on demand\. AppStream 2\.0 provides users access to the applications they need on the device of their choice, with a responsive, fluid user experience that is indistinguishable from natively installed applications\. 

With AppStream 2\.0, you can easily add your existing desktop applications to AWS and enable your users to instantly stream them\. Windows users can use either the AppStream 2\.0 client or an HTML5\-capable web browser for application streaming\. You can maintain a single version of each of your applications, which makes application management easier\. Your users always access the latest versions of their applications\. Your applications run on AWS compute resources, and data is never stored on users' devices, which means they always get a high performance, secure experience\.

Unlike traditional on\-premises solutions for desktop application streaming, AppStream 2\.0 offers pay\-as\-you\-go pricing, with no upfront investment and no infrastructure to maintain\. You can scale instantly and globally, ensuring that your users always have the best possible experience\.

For more information, see [AppStream 2\.0](https://aws.amazon.com/appstream2/details)\.

## Features<a name="what-is-features"></a>

Using Amazon AppStream 2\.0 provides the following advantages:

**Access desktop applications securely from any supported device**  
Your desktop applications can be accessed securely through an HTML5\-capable web browser on Windows and Linux PCs, Macs, Chromebooks, iPads, and Android tablets\. Or, for supported versions of Windows, the AppStream 2\.0 client can be used for application streaming\.

**Secure applications and data**  
Applications and data remain on AWS — only encrypted pixels are streamed to users\. Applications run on an AppStream 2\.0 instance dedicated to each user so that compute resources are not shared\. Applications can run inside your own virtual private cloud \(VPC\), and you can use Amazon VPC security features to control access\. This enables you to isolate your applications and deliver them in a secure way\.

**Consistent, scalable performance**  
AppStream 2\.0 runs on AWS with access to compute capabilities not available on local devices, which means that your applications run with consistently high performance\. You can instantly scale locally and globally, and ensure that your users always get a low\-latency experience\. Unlike on\-premises solutions, you can quickly deploy your applications to the AWS region that is closest to your users, and start streaming with no incremental capital investment\.

**Integrate with your IT environment**  
Integrate with your existing AWS services and your on\-premises environments\. By running applications inside your VPCs, your users can access data and other resources that you have in AWS\. This reduces the movement of data between AWS and your environment and provides a faster user experience\.  
Integrate with your existing Microsoft Active Directory environment\. This enables you to use existing Active Directory governance, user experience, and security policies with your streaming applications\.  
Configure identity federation, which allows your users to access their applications using their corporate credentials\. You can also allow authenticated access to your IT resources from applications running on AppStream 2\.0\.

**Choose the fleet type that meets your needs**  
There are two types of fleets:  
+ Always\-On — Your instances run all the time, even when no users are streaming applications\. Use an Always\-On fleet to provide your users with instant access to their applications\.
+ On\-Demand — Your instances run only when users are streaming applications\. Idle instances that are available for streaming are in a stopped state\. Use an On\-Demand fleet to optimize your streaming charges and provide your users with access to their applications after a 1\-2 minute wait\.
For more information, see [Amazon AppStream 2\.0 Pricing](https://aws.amazon.com/appstream2/pricing/)\.

## Key Concepts<a name="what-is-concepts"></a>

To get the most out of AppStream 2\.0, be familiar with the following concepts:

**image builder**  
An *image builder* is a virtual machine that you use to create an image\. You can launch and connect to an image builder by using the AppStream 2\.0 console\. After you connect to an image builder, you can install, add, and test your applications, and then use the image builder to create an image\. You can launch new image builders by using private images that you own\.

**image**  
An *image* contains applications that you can stream to your users, and default Windows and application settings to enable your users to get started with their applications quickly\. AWS provides base images that you can use to create images that include your own applications\. After you create an image, you can't change it\. To add other applications, update existing applications, or change image settings, you must create a new image\. You can copy your images to other AWS Regions or share them with other AWS accounts in the same Region\. 

**fleet**  
A *fleet* consists of fleet instances \(also known as streaming instances\) that run the image that you specify\. You can set the desired number of streaming instances for your fleet and configure policies to scale your fleet automatically based on demand\. Note that one user requires one instance\.

**stack**  
A *stack* consists of an associated fleet, user access policies, and storage configurations\. You set up a stack to start streaming applications to users\.

**streaming instance**  
A *streaming instance* \(also known as a fleet instance\) is an EC2 instance that is made available to a single user for application streaming\. After the user’s session completes, the instance is terminated by EC2\.

**user pool**  
Use the *user pool* to manage users and their assigned stacks\.

## How to Get Started<a name="what-is-how-to-start"></a>

If you are using AppStream 2\.0 for the first time, you can use the **Try it Now **feature or follow the [Get Started with Amazon AppStream 2\.0: Set Up With Sample Applications](getting-started.md) tutorial \(both are available in the AppStream 2\.0 console\)\.
+ **Try It Now **provides you with a free trial experience that allows you to easily start desktop applications from your desktop browser\. 
+ The Getting Started tutorial enables you to set up application streaming by using sample applications or your own applications\. If you decide to start by using sample applications, you can always add your own applications later\.

  For more information about these two options, see [Amazon AppStream 2\.0 FAQs](https://aws.amazon.com/appstream2/faqs/)\.

When you use the service for the first time, AppStream 2\.0 creates an [AWS Identity and Access Management \(IAM\)](https://aws.amazon.com/iam/faqs/) role to create and manage AppStream 2\.0 resources on your behalf\. 

**To use the Try It Now feature**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose **Try it now**\.

1. Sign in using your AWS account credentials, if requested\.

1. Read the terms and conditions and choose **Agree and Continue**\.

1. From the list of applications shown, select one to try\.

**To run the Getting Started tutorial**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. Choose **Get Started**\.

1. Select the option to learn more about AppStream 2\.0 resources\.

## Accessing AppStream 2\.0<a name="what-is-accessing"></a>

You can work with AppStream 2\.0 using any of the following interfaces:

**AWS Management Console**  
The console is a browser\-based interface to manage AppStream 2\.0 resources\. For more information, see [Get Started with Amazon AppStream 2\.0: Set Up With Sample Applications](getting-started.md)\.

**AWS command line tools**  
AWS provides two sets of command line tools: the [AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/) \(AWS CLI\) and the [AWS Tools for Windows PowerShell](https://docs.aws.amazon.com/powershell/latest/userguide/)\. To use the AWS CLI to run AppStream 2\.0 commands, see [Amazon AppStream 2\.0 Command Line Reference](https://docs.aws.amazon.com/cli/latest/reference/appstream/)\.

**AWS SDKs**  
You can access AppStream 2\.0 from a variety of programming languages\. The SDKs automatically take care of tasks such as the following:  
+ Setting up an AppStream 2\.0 stack or fleet
+ Getting an application streaming URL to your stack
+ Describing your resources
For more information, see [Tools for Amazon Web Services](https://aws.amazon.com/tools/)\.