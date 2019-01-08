# Manage Access Using the AppStream 2\.0 User Pool<a name="user-pool"></a>

The AppStream 2\.0 user pool provides a simplified way to manage access to applications for your users through a persistent portal for each AWS Region\. This feature is a built\-in alternative to user management through Active Directory and SAML 2\.0 federation\. To use external identity providers for user management, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\. To join your Active Directory domain to AppStream 2\.0, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

**Note**  
Stacks can't be assigned to users in the user pool if the stacks are associated with a fleet that is joined to an Active Directory domain\. 

The AppStream 2\.0 user pool provides the following key features:
+ Users can access application stacks through a persistent URL and login credentials by using their email address and a password that they choose\.
+ You can assign multiple stacks to users\. Doing so enables AppStream 2\.0 to display multiple application catalogs to users when they log in\.
+ When you create new users, a welcome email is automatically sent to them\. The email includes instructions, a login portal link, and a temporary password for connecting to the login portal\.
+ After you create users, they are enabled unless you specifically disable them\.
+ You can control which users have access to which application stacks, or disable access completely\.
+ Users can start AppStream 2\.0 streaming sessions by using a web browser\. Currently, the AppStream 2\.0 client is not supported for users in the user pool\.

## User Pool End User Experience<a name="user-pool-end-user"></a>

The following steps summarize the initial connection experience for users in the user pool\. 

1. You create new users in the Region you want by specifying their email addresses\.

1. AppStream 2\.0 sends them a welcome email\.

1. You assign one or more stacks to the users\. 

1. AppStream 2\.0 sends them an optional notification email\. This email includes information about how to access the stacks that are newly assigned to them\.

1. The users connect to the login portal by entering the information included in the welcome email, and they set a permanent password\. The login portal link never expires and can be used any time\.

1. They sign in to AppStream 2\.0 by entering their email address and permanent password\. 

1. After they sign in, the users can view their application catalogs\.

The login portal link provided in the welcome email should be saved for future use, as it does not change and is valid for all users in the user pool\. The login portal URL and users in the user pool are managed on a per\-Region basis\.

### Resetting a Forgotten Password<a name="user-pool-end-user-reset-password"></a>

If users forget their password, follow these steps to connect to the login portal link \(provided in the welcome email\) and choose a new password\.

**To choose a new password**

1. Open the AppStream 2\.0 login portal by using the login link provided in the welcome email\.

1. Choose **Forgot Password?**\.

1. Type the email address that you used to create the user in the user pool, and choose **Next**\.

1. Check your email for the password reset request message\. If you are having difficulty finding the email, check your spam email folder\. Type the verification code from the email in **Verification Code**\.
**Note**  
The verification code is valid for 24 hours\. If a new password is not chosen within this time, request a new verification code\.

1. Following the password rules shown, type and confirm your new password\. Choose **Reset Password**\.