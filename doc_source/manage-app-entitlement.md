# Manage App Entitlement with the Dynamic Application Framework<a name="manage-app-entitlement"></a>

Amazon AppStream 2\.0 supports dynamically building the application catalog that displays for your users when they stream from an AppStream 2\.0 stack\. You can use the API operations provided by AppStream 2\.0 to develop a dynamic app provider that modifies, in real time, the applications that users can access on the streaming instance\. Alternatively, you can implement a third\-party dynamic app provider that uses these API operations\. 

**Note**  
This feature requires an AppStream 2\.0 fleet that is joined to a Microsoft Active Directory domain\. For more information, see [Using Active Directory with AppStream 2\.0](active-directory.md)\.

**Topics**
+ [Example API Operations Work Flow for the Dynamic Application Framework](manage-app-entitlement-sample-api-workflow.md)
+ [Use the AppStream 2\.0 Dynamic Application Framework to Build a Dynamic App Provider](build-dynamic-app-provider.md)
+ [Enable and Test Dynamic App Providers](enable-test-dynamic-app-providers.md)
+ [Third\-Party Dynamic App Providers](third-party-dynamic-app-providers.md)