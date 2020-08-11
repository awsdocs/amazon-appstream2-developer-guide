# User Pool Administration<a name="user-pool-admin"></a>

To create and manage users in the user pool, sign in to the AppStream 2\.0 console for the AWS Region you want and choose **User Pool** in the left navigation pane\. The User Pool dashboard supports bulk operations on a list of users for some actions\. You can select multiple users on which to perform the same action from the **Actions** list\. Users in the user pool are created and managed on a per\-Region basis\.

AppStream 2\.0 does not support bulk user creation or disable\. However, you can use Amazon Cognito with the [CreateStreamingURL](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateStreamingURL.html) API action to manage access efficiently for multiple users\. Amazon Cognito user pools let you quickly create your own directory to sign up and sign in users\. In addition, you can use Amazon Cognito user pools to store user profiles\. For information about how to integrate AppStream 2\.0 with your Cognito User Pool, see the [Create a SaaS Portal with Amazon AppStream 2\.0](https://aws.amazon.com/appstream2/getting-started/isv-workshops/saas/) project\.

**Note**  
AppStream 2\.0 sends email to users on your behalf when a new user is created or a user is assigned to a stack\. To ensure the email is delivered, add `no-reply@accounts.aws-region-code.amazonappstream.com` to your allow list, where `aws-region-code` is a valid AWS Region code in which you are working\. If users are having difficulty finding the emails, ask them to check their "spam" email folder\.

**Topics**
+ [Creating a User](#user-pool-admin-create)
+ [Deleting a User](#user-pool-admin-deleting-user)
+ [Assigning Stacks to Users](#user-pool-admin-assigning)
+ [Unassigning Stacks from Users](#user-pool-admin-unassigning)
+ [Disabling Users](#user-pool-admin-disabling)
+ [Enabling Users](#user-pool-admin-enabling)
+ [Re\-Sending Welcome Email](#user-pool-admin-email)

## Creating a User<a name="user-pool-admin-create"></a>

You must enter a valid and unique email address for each new user within a Region\. However, you can reuse an email address for a new user in another Region\.

When you create a new user, be aware of the following:
+ You cannot change the email address, first name, or last name for a user that you have already created\. To change this information for a user, disable the user\. Then, recreate the user \(as a new user\) and specify the updated information as needed\. 
+ Users' email addresses are case\-sensitive\. During login, if they specify an email address that doesn't use the same capitalization as the email address specified when their user pool account was created, a "user does not exist" error message displays\.
+ You can assign one or more stacks to the user after the user is created\.

**To create a new user**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **User Pool**, **Create User**\.

1. For **Email**, type the unique email address for the user\.

1. Type the user's first name and last name in the corresponding fields\. These fields need not be unique\.

1. Choose **Create User**\.

After users are created, AppStream 2\.0 sends them a welcome email\. This email includes the login portal link, the login email address to be used, and a temporary password\. By browsing to the login portal and typing their temporary password, users can set a permanent password to access their applications\. 

By default, the new user's status is **Enabled**, meaning you can assign one or more stacks to the user or perform other administrative actions\.

## Deleting a User<a name="user-pool-admin-deleting-user"></a>

You can enable or disable a user, but you cannot delete a user by using the AppStream 2\.0 console\. To delete a user, you must use the [DeleteUser](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DeleteUser.html) API action\.

## Assigning Stacks to Users<a name="user-pool-admin-assigning"></a>

You can assign one or more stacks to one or more users in the user pool\. After they are assigned to at least one stack, users can log in to AppStream 2\.0 and launch applications\. If users are assigned to more than one stack, they are presented with a list of stacks as catalogs to choose from before launching applications\. 

**Note**  
Stacks can't be assigned to users if the stacks are associated with a fleet that is joined to an Active Directory domain\. 

**To assign a stack to users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **User Pool** and select the users you want\.

1. Choose **Actions**, **Assign stack**\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

1. Review the list to confirm that the correct users are specified\. For **Stack**, choose the stack you want to assign\.

1. By default, **Send email notification to user** is enabled\. Clear this option if you do not want to send the notification email to users now\.

1. Choose **Assign stack**\.

## Unassigning Stacks from Users<a name="user-pool-admin-unassigning"></a>

You can unassign a stack from one or more users in the user pool\. After a stack is unassigned from users, they can't launch applications from the stack\. If users are connected when you unassign the stack, their sessions remain active until the session cookie expires \(about one hour\)\.

**To unassign a stack from users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **User Pool** and select the users you want\.

1. Choose **Actions**, **Unassign stack**\.

1. Review the list to confirm that the correct users are specified\. For **Stack**, choose the stack you want to unassign\. The list includes all stacks, assigned or unassigned\.

1. Choose **Unassign stack**\.

## Disabling Users<a name="user-pool-admin-disabling"></a>

You can disable one or more users in the user pool, one at a time\. After they are disabled, users can no longer log in to AppStream 2\.0 until they are re\-enabled\. This action does not delete users\. If users are connected when you disable them, their sessions remain active until the session cookie expires \(about one hour\)\. Stack assignments for the users are retained\. If the users are re\-enabled, their stack assignments become active again\.

**To disable a user**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **User Pool** and select the user you want\.

1. Choose **Actions**, **Disable user**\.

1. Confirm that the correct user is specified, and choose **Disable User**\.

## Enabling Users<a name="user-pool-admin-enabling"></a>

You can enable one or more users in the user pool, one at a time\. After they are enabled, users can log in to AppStream 2\.0 and launch applications from the stacks to which they are assigned\. If the users were disabled, these assignments are retained\.

**To enable users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **User Pool** and select the user you want\.

1. Choose **Actions**, **Enable user**\.

1. Confirm that the correct user is specified, and choose **Enable User**\.

## Re\-Sending Welcome Email<a name="user-pool-admin-email"></a>

You can re\-send the welcome email with connection instructions to users in the user pool\. Unused passwords expire after seven days\. To provide a new temporary password, you must re\-send the welcome email\. This option is only available until users set their permanent password\. If they've already set their password and forgotten it, they can set a new one\. For more information, see [Resetting a Forgotten Password](user-pool.md#user-pool-end-user-reset-password)\.

**To resend the welcome email for a user**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **User Pool** and select the user you want\.

1. For **User Details**, choose **Resend welcome email**\.

1. Confirm that the success message displays at the top of the User Pool dashboard\.