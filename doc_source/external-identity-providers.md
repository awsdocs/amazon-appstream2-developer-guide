# Single Sign\-on Access \(SAML 2\.0\)<a name="external-identity-providers"></a>

Amazon AppStream 2\.0 supports identity federation to AppStream 2\.0 stacks through Security Assertion Markup Language 2\.0 \(SAML 2\.0\)\. You can use an identity provider \(IdP\) that supports SAML 2\.0—such as Active Directory Federation Services \(AD FS\) in Windows Server, Ping One Federation Server, or Okta—to provide an onboarding flow for your AppStream 2\.0 users\. 

This feature offers your users the convenience of one\-click access to their AppStream 2\.0 applications using their existing identity credentials\. You also have the security benefit of identity authentication by your IdP\. By using your IdP, you can control which users have access to a particular AppStream 2\.0 stack\.

## Example Authentication Workflow<a name="external-identity-providers-example"></a>

The following diagram illustrates the authentication flow between AppStream 2\.0 and a third\-party identity provider \(IdP\)\. In this example, the administrator has set up a sign\-in page to access AppStream 2\.0, called `applications.exampleco.com`\. The webpage uses a SAML 2\.0–compliant federation service to trigger a sign\-on request\. The administrator has also set up a user to allow access to AppStream 2\.0\.

![\[Amazon AppStream 2.0 SAML diagram\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/aas2-saml.png)

1. The user browses to `https://applications.exampleco.com`\. The sign\-on page requests authentication for the user\.

1. The federation service requests authentication from the organization's identity store\.

1. The identity store authenticates the user and returns the authentication response to the federation service\.

1. On successful authentication, the federation service posts the SAML assertion to the user's browser\.

1. The user's browser posts the SAML assertion to the AWS Sign\-In SAML endpoint \(`https://signin.aws.amazon.com/saml`\)\. AWS Sign\-In receives the SAML request, processes the request, authenticates the user, and forwards the authentication token to AppStream 2\.0\.

   For information about working with SAML in AWS GovCloud \(US\-West\), see [AWS Identity and Access Management](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-iam.html) in the *AWS GovCloud \(US\) User Guide*\.

1. Using the authentication token from AWS, AppStream 2\.0 authorizes the user and presents applications to the browser\.

From the user's perspective, this process happens transparently\. The user starts at your organization's internal portal and is automatically redirected to an AppStream 2\.0 application portal without being required to enter AWS credentials\.