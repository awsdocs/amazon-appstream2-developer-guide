# Overview of Active Directory Domains<a name="active-directory-overview"></a>

Using Active Directory domains with AppStream 2\.0 requires some understanding of how they work together, and the tasks required\. The following tasks must be completed by an administrator:

1. Set the group policies controlling the end user experience and security requirements for applications\.

1. Create the domain\-joined application stack in AppStream 2\.0\.

1. Create the AppStream 2\.0 app in the SAML 2\.0 identity provider and assign it to end users either directly or with Active Directory groups\.

To authenticate users for proper access to the joined domain from within their streaming apps, there are several steps that occur when a user initiates an AppStream 2\.0 streaming session\. The following diagram illustrates the end\-to\-end user authentication flow from the initial browser request through all the SAML and Active Directory authentication steps\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/appstream2/latest/developerguide/images/domain-join.png)

**User Authentication Flow**

1. The user browses to `https://applications.exampleco.com`\. The sign\-on page requests authentication for the user\.

1. The federation service requests authentication from the organization's identity store\.

1. The identity store authenticates the user and returns the authentication response to the federation service\.

1. On successful authentication, the federation service posts the SAML assertion to the user's browser\.

1. The user's browser posts the SAML assertion to the AWS Sign\-In SAML endpoint \(`https://signin.aws.amazon.com/saml`\)\. AWS Sign\-In receives the SAML request, processes the request, authenticates the user, and forwards the authentication token to the AppStream 2\.0 service\.

1. Using the authentication token from AWS, AppStream 2\.0 authorizes the user and presents applications to the browser\.

1. The user chooses an app and is prompted to enter login information for the domain\.

1. The domain controller is contacted for user authentication\.

1. After being authenticated with the domain, the user's session starts with domain connectivity\.

From the user's perspective, the process happens transparently: The user starts at your organization's internal portal and lands at an AppStream 2\.0 application portal, without ever having to supply any AWS credentials\. Only Active Directory domain login credentials are required\.

The administrator's tasks, such as to set up the Active Directory with entitlements and group policies, and to create a domain\-joined application stack, must be completed before the user can initiate this authentication process\.