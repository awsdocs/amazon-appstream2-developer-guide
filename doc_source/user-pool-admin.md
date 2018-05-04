# User Pool Administration<a name="user-pool-admin"></a>

To perform administrator actions, sign in to the AppStream 2\.0 console in the AWS Management Console for the desired region and select User Pool in the left navigation pane\. The User Pool dashboard supports bulk operations on a list of users for some actions\. An administrator can select multiple users on which to perform the same action from the **Actions** list\. Bulk user creation or disable is not supported\. User pool users are created and managed on a per\-region basis\.

**Note**  
AppStream 2\.0 sends email to users on your behalf, such as when a new user is created or a user is assigned to a stack\. To ensure that email is delivered, add `no-reply@accounts.aws-region-code.amazonappstream.com` to your whitelist, where `aws-region-code` is a valid AWS region code in which you are working\. If users are having difficulty finding the emails, ask them to check their "spam" email folder\.

**Topics**
+ [Creating a User](#user-pool-admin-create)
+ [Assigning Stacks to Users](#user-pool-admin-assigning)
+ [Unassigning Stacks from Users](#user-pool-admin-unassigning)
+ [Disabling Users](#user-pool-admin-disabling)
+ [Enabling Users](#user-pool-admin-enabling)
+ [Re\-Sending Welcome Email](#user-pool-admin-email)

## Creating a User<a name="user-pool-admin-create"></a>

Users are managed on a per\-region basis\. You must use a valid and unique email address for each new user within a region\. However, you can reuse an email address for a new user in another region\.

When you create a new user, be aware of the following:
+ There is no limit on the number of users in the user pool\. 
+ You can enable or disable a user, but you cannot delete a user\.
+ You cannot change the email address, first name, or last name for a user that you have already created\. To change this information for a user, disable the user\. Then, recreate the user \(as a new user\) and specify the updated information as needed\. 
+ You can assign one or more stacks to the user after the user is created\.

**To create a new user**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **User Pool**, **Create User**\.

1. For **Email**, type the unique email address for this user\.

1. For **First name** and **Last name**, type values\. These fields need not be unique\.

1. Choose **Create User**\.

After the user is created, AppStream 2\.0 sends a welcome email to the user\. This email has the login portal link, the login email address to be used, and a temporary password\. By browsing to the login portal and using the temporary password, the user can set a permanent password to access their applications\. 

By default, the new user's status is **Enabled**, meaning you can assign one or more stacks to the user, or perform other actions\.

## Assigning Stacks to Users<a name="user-pool-admin-assigning"></a>

An AppStream 2\.0 administrator can assign one or more stacks to one or more user pool users\. After being assigned at least one stack, the user can log in and launch applications\. If users are assigned more than one stack, they are presented with a list of stacks as catalogs to choose from before launching applications\. User Pool users cannot be assigned to stacks with fleets that are joined to an Active Directory domain\.

**To assign a stack to users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **User Pool** and select the users\.

1. Choose **Actions**, **Assign stack**\. Note that users cannot be assigned to stacks that have a fleet joined to an Active Directory domain\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

1. Confirm the list of users in the resulting dialog box\. For **Stack**, choose the desired stack\.

1. By default, **Send email notification to user** is enabled\. Clear this option if you do not want to send the notification email to the user at this time\.

1. Choose **Assign stack**\.

## Unassigning Stacks from Users<a name="user-pool-admin-unassigning"></a>

An AppStream 2\.0 administrator can unassign stacks from one or more user pool users\. After being unassigned a stack, the user can no longer launch applications from that stack\.

**To unassign a stack from users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **User Pool** and select the users\.

1. Choose **Actions**, **Unassign stack**\.

1. Confirm the list of users in the resulting dialog box\. For **Stack**, choose the desired stack\. This list includes all stacks, assigned or unassigned\.

1. Choose **Unassign stack**\.

## Disabling Users<a name="user-pool-admin-disabling"></a>

An AppStream 2\.0 administrator can disable one or more user pool users, one at a time\. After being disabled, the user can no longer log in until they are re\-enabled\. This action does not delete the user\. If the user is currently connected when an administrator disables them, their session remains active until the session cookie expires \(about one hour\)\. Stack assignments for the user are retained\. If the user is re\-enabled, the stack assignment becomes active again\.

**To disable a user**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **User Pool** and select the user\.

1. Choose **Actions**, **Disable user**\.

1. Confirm the user in the resulting dialog box and choose **Disable User**\.

## Enabling Users<a name="user-pool-admin-enabling"></a>

An AppStream 2\.0 administrator can enable one or more user pool users, one at a time\. After being enabled, the user can log in and launch applications from the stacks to which they are assigned\. If the user was disabled, these assignments are retained\.

**To enable users**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **User Pool** and select the users\.

1. Choose **Actions**, **Enable user**\.

1. Confirm the user in the resulting dialog box and choose **Enable User**\.

## Re\-Sending Welcome Email<a name="user-pool-admin-email"></a>

An AppStream 2\.0 administrator can re\-send the welcome email with connection instructions to user pool users\. Unused passwords expire after seven days\. To provide a new temporary password, the administrator must re\-send the welcome email\. This option is only available until the user sets their permanent password\. If they've already set a password and have forgotten it, they can set a new one\. For more information, see [Resetting a Forgotten Password](user-pool.md#user-pool-end-user-reset-password)\.

**To resend the welcome email for a user**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **User Pool** and select a user\.

1. For **User Details**, choose **Resend welcome email**\.

1. Confirm the success message at the top of the dashboard\.