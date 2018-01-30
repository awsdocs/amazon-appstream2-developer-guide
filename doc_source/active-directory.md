# Using Active Directory Domains with AppStream 2\.0<a name="active-directory"></a>

You can join your Amazon AppStream 2\.0 fleets and image builders to Microsoft Active Directory domains\. You can use your existing Microsoft Active Directories, either cloud\-based or on\-premises, for launching domain\-joined streaming instances\. You can also use AWS Directory Service to create an Active Directory and use that to support your AppStream 2\.0 resources\. For more information about using AWS Directory Service, see [Microsoft Active Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_microsoft_ad.html) in the *AWS Directory Service Administration Guide*\.

Joining AppStream 2\.0 to your Active Directory domain offers the following key benefits:

+ Allow your users and applications to access your Active Directory resources such as printers and file shares from streaming sessions\.

+ Apply directory\-based group policies to your streaming instances to configure and control the end user experience\.

+ Stream applications such as Microsoft SharePoint or Microsoft Outlook that require users to be authenticated using their Active Directory login credentials\.

+ Apply your enterprise compliance and security policies to your AppStream 2\.0 streaming instances\.


+ [Overview of Active Directory Domains](active-directory-overview.md)
+ [Before You Begin Using Active Directory with AppStream 2\.0](active-directory-prerequisites.md)
+ [Tutorial: Setting Up the Active Directory](active-directory-directory-setup.md)
+ [AppStream 2\.0 Active Directory Administration](active-directory-admin.md)
+ [More Info](active-directory-more-info.md)