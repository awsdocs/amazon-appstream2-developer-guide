# Manage Access Using the AppStream 2\.0 User Pool<a name="user-pool"></a>

The AppStream 2\.0 user pool offers a simplified way to manage access to applications for your end users through a persistent portal for each region\. This feature is offered as a built\-in alternative to user management through Active Directory and SAML 2\.0 federation\. To use external identity providers for user management, see [Single Sign\-on Access to AppStream 2\.0 Using SAML 2\.0](external-identity-providers.md)\. To join your Active Directory domain to AppStream 2\.0, see [Using Active Directory Domains with AppStream 2\.0](active-directory.md)\.

**Note**  
User pool users cannot be assigned to stacks with fleets that are joined to an Active Directory domain\.

The AppStream 2\.0 user pool offers the following key features:

+ Users can access application stacks through a persistent URL and login credentials using their email address and a password that they choose\.

+ Administrators can assign a user multiple stacks, offering multiple application catalogs to the user when they log in\.

+ When an administrator creates a new user, a welcome email is automatically sent to the end user with a login portal link and instructions\.

+ After being created, a user in the pool remains valid and usable unless an administrator specifically disables that user\.

+ Administrators can control which users have access to which application stacks, or disable access completely\.

## User Pool End User Experience<a name="user-pool-end-user"></a>

With the user pool, the following flow of actions summarizes the initial connection experience for the end user\. 

1. An administrator creates a new user in the desired region using the end user's email address\.

1. AppStream 2\.0 sends a welcome email with instructions and a temporary password\.

1. An administrator assigns the user one or more stacks\. 

1. AppStream 2\.0 sends an optional notification email to the end user with information and instructions for the stacks to which the user is newly assigned\.

1. Using the information in the welcome email, the end user connects to the login portal and uses their temporary password to set a permanent password\. The login portal link never expires and can be used anytime\.

1. Using the email address and permanent password they set up earlier, the end user signs in and is presented with their application catalogs\.

The login portal link provided in the welcome email should be saved for future use, as it does not change and is valid for all user pool users\. Note that the login portal URL and user pool user are managed on a per\-region basis\.

### Resetting a Forgotten Password<a name="user-pool-end-user-reset-password"></a>

If a user forgets their password, they can connect to the login portal link \(provided in the welcome email\) to choose a new password\.

**To choose a new password**

1. Open the AppStream 2\.0 login portal using the login link provided in the welcome email\.

1. Choose **Forgot Password?**\.

1. Type the email address used to create your user pool user\. Choose **Next**\.

1. Check your email for the password reset request message\. If you are having difficulty finding the email, check your spam email folder\. Type the verification code from the email in **Verification Code**\.
**Note**  
The verification code is valid for 24 hours\. If a new password is not chosen within this time, request a new verification code\.

1. Following the password rules shown, type and confirm your new password\. Choose **Reset Password**\.