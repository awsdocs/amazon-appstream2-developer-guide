# Attribute\-Based Application Entitlements Using a Third\-Party SAML 2\.0 Identity Provider<a name="application-entitlements-saml"></a>

Application entitlements control access to specific applications within your AppStream 2\.0 stacks\. This works by using SAML 2\.0 attribute assertions from a third\-party SAML 2\.0 identity provider\. The assertion is matched to a value when a user identity federates to an AppStream 2\.0 2\.0 SAML application\. If the entitlement is true, and the attribute name and value match, access is entitled for the user identity to one or more applications within the stack\.

Attribute\-based application entitlements using a third\-party SAML 2\.0 identity provider do not apply in the following scenarios\. In other words, the entitlement is ignored in cases such as the following:
+ AppStream 2\.0 user pool authentication\. For more information, see [AppStream 2\.0 User Pools](user-pool.md)\.
+ AppStream 2\.0 streaming URL authentication\. For more information, see [Streaming URL](use-client-start-streaming-session.md#use-client-start-streaming-session-streaming-URL)\.
+ The desktop application when AppStream 2\.0 fleets are configured for **Desktop Stream view**\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
+ Stacks using the Dynamic Application Framework\. Dynamic Application Framework provides separate application entitlement features\. For more information, see [Application Entitlements from a Dynamic App Provider Using the Dynamic Application Framework](dynamic-app-framework.md)\.
+ When users federate to the AppStream 2\.0 application catalog, application entitlements will only display the applications the user is entitled to\. Applications are not restricted from running within the AppStream 2\.0 session\. For example, in a fleet configured for Desktop Stream view, a user can launch an application directly from the desktop\.

## Create Application Entitlements<a name="manage-application-entitlements"></a>

Before you create application entitlements, you must do the following:
+ Create an AppStream 2\.0 fleet and stack with an image containing one or more applications \(Always\-On or On\-Demand fleet\) or assigned applications \(Elastic fleet\) that will meet your needs\. For more information, see [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md)\.
+ Provide user access to the stack using a third\-party SAML 2\.0 identity provider\. For more information, see [Single Sign\-on Access \(SAML 2\.0\)](external-identity-providers.md)\. If you are using an existing SAML 2\.0 identity provider that you setup previously, see [Step 2: Create a SAML 2\.0 Federation IAM Role](external-identity-providers-setting-up-saml.md#external-identity-providers-grantperms) for the steps to add the sts:TagSession permission to your IAM role trust policy\. For more information, see [Passing session tags in AWS STS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html)\. This permission is required to use application entitlements\.

**To create an application entitlement**

1. [Open the AppStream 2\.0 console](managing-image-builders-connect.md#managing-image-builders-connect-console)\.

1. In the left navigation pane, choose **Stacks**, and select the stack for which to manage application entitlements\.

1. In the **Application Entitlements** dialog box, choose **Create**\.

1. Enter a **Name** and **Description** for your entitlement\.

1. Define the attribute name and value for your entitlement\.

   When mapping attributes, specify the attribute in the format https://aws\.amazon\.com/SAML/Attributes/PrincipalTag:\{TagKey\}, where \{TagKey\} is one of the following attributes: 
   + roles
   + department
   + organization
   + groups
   + title
   + costCenter
   + userType

   The attributes that you defined are used to entitle applications in your stack to a user when they federate into an AppStream 2\.0 session\. Entitlement works by matching the attribute name to a key value name in the SAML assertion created during federation\. For more information, see [SAML PrincipalTag Attribute](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_saml_assertions.html#saml_role-session-tags.html)\.
**Note**  
One or more values can be included in any supported attribute, separated by a colon \(:\)\.   
For example, groups information can be passed in a SAML attribute name https://aws\.amazon\.com/SAML/Attributes/PrincipalTag:groups with value “group1:group2:group3” and your entitlement can allow applications based on a single group value, i\.e\. “group1”\. For more information, see [SAML PrincipalTag Attribute](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_saml_assertions.html#saml_role-session-tags.html)\.

1. Configure application settings in your stack to entitle all applications, or select applications\. Choosing **All applications \(\*\)** applies all applications available on the stack, including applications that are added in the future\. Choosing **Select applications** will filter on specific application names\.

1. Review your settings and create your entitlement\. You can repeat the process and create additional entitlements\. Entitlement to applications in a stack will be a union of all entitlements that match the user based on attribute names and values\.

1. In your SAML 2\.0 identity provider, configure your AppStream 2\.0 SAML application attribute mappings to send the attribute and value defined in your entitlement\. When users federate to the AppStream 2\.0 application catalog, application entitlements will only display the applications the user is entitled to\.

## SAML 2\.0 Multi\-Stack Application Catalog<a name="saml-application-catalog"></a>

With attribute\-based application entitlements using a third\-party SAML 2\.0 identity provider, you can enable access to multiple stacks from a single relay state URL\. Remove the stack and app \(if present\) parameters from the relay state URL, as follows:

```
https://relay-state-region-endpoint?accountId=aws-account-id-without-hyphens
```

When users federate to the AppStream 2\.0 application catalog, they will be presented with all of the stacks where application entitlements have matched one or more applications to the user for the account ID and relay state endpoint associated with the Region in which your stacks are located\. When a user selects a catalog, application entitlements will only display the applications the user is entitled to\. For more information, see [Step 6: Configure the Relay State of Your Federation](external-identity-providers-setting-up-saml.md#external-identity-providers-relay-state)\.

**Note**  
To use SAML 2\.0 Multi\-Stack Application Catalogs, you need to configure the inline policy for your SAML 2\.0 Federation IAM Role\. For more information, see [Step 3: Embed an Inline Policy for the IAM Role](external-identity-providers-setting-up-saml.md#external-identity-providers-embed-inline-policy-for-IAM-role)\. 