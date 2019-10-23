# Using Active Directory with AppStream 2\.0<a name="active-directory"></a>

You can join your Amazon AppStream 2\.0 fleets and image builders to domains in Microsoft Active Directory and use your existing Active Directory domains, either cloud\-based or on\-premises, to launch domain\-joined streaming instances\. You can also use AWS Directory Service for Microsoft Active Directory, also known as AWS Managed Microsoft AD, to create an Active Directory domain and use that to support your AppStream 2\.0 resources\. For more information about using AWS Managed Microsoft AD, see [Microsoft Active Directory](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_microsoft_ad.html) in the *AWS Directory Service Administration Guide*\.

By joining AppStream 2\.0 to your Active Directory domain, you can:
+ Allow your users and applications to access Active Directory resources such as printers and file shares from streaming sessions\.
+ Use Group Policy settings that are available in the Group Policy Management Console \(GPMC\) to define the end user experience\.
+ Stream applications that require users to be authenticated using their Active Directory login credentials\.
+ Apply your enterprise compliance and security policies to your AppStream 2\.0 streaming instances\.

**Topics**
+ [Overview of Active Directory Domains](active-directory-overview.md)
+ [Before You Begin Using Active Directory with AppStream 2\.0](active-directory-prerequisites.md)
+ [Tutorial: Setting Up Active Directory](active-directory-directory-setup.md)
+ [AppStream 2\.0 Active Directory Administration](active-directory-admin.md)
+ [More Info](active-directory-more-info.md)