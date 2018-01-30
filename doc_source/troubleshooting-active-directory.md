# Troubleshooting Active Directory Domain Join<a name="troubleshooting-active-directory"></a>

The following are possible issues you might have while setting up and using Active Directory with Amazon AppStream 2\.0\. For help troubleshooting notification codes, see [Troubleshooting Notification Codes](troubleshooting-notification-codes.md)\.


+ [My image builders and fleet instances are stuck in "pending" status](#troubleshooting-active-directory-1)
+ [My users aren't able to log in with the SAML app](#troubleshooting-active-directory-2)
+ [My fleet instances work for one user but don't cycle correctly](#troubleshooting-active-directory-3)
+ [My user Group Policy Objects aren't applying successfully](#troubleshooting-active-directory-4)
+ [My AppStream 2\.0 streaming instances aren't joining the Active Directory domain](#troubleshooting-active-directory-5)
+ [User login is taking a long time to complete on a domain\-joined streaming session](#troubleshooting-active-directory-6)
+ [The changes I made in the image builder aren't reflected in end user streaming sessions](#troubleshooting-active-directory-7)
+ [Unable to access a domain resource in a domain joined streaming session but could access the resource from a domain\-joined image builder](#troubleshooting-active-directory-8)

## My image builders and fleet instances are stuck in "pending" status<a name="troubleshooting-active-directory-1"></a>

Image builders and fleet instances can take up to 25 minutes to move into a ready state and become available\. If your instances are taking longer than 25 minutes to become available, check your Active Directory to see if new computer objects were created in the organizational units \(OUs\)\. If there are new objects, the streaming instances will be available soon\. If the objects aren't there, check the directory configuration details in your AppStream 2\.0 Directory Config: Active Directory fully qualified domain name, service account username and password, and the OU distinguished name\. 

Image builder and fleet errors are available in the AppStream 2\.0 console in the notifications tab when viewing the image builder or fleet details\. Fleet errors are also available using the AppStream 2\.0 API via the [DescribeFleets](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeFleets.html) operation, or the CLI command [describe\-fleets](http://docs.aws.amazon.com/cli/latest/reference/appstream/describe-fleets.html)\.

## My users aren't able to log in with the SAML app<a name="troubleshooting-active-directory-2"></a>

AppStream 2\.0 relies on the SAML\_Subject "NameID" attribute from your identity provider to populate the username field to log in your user\. The username can either be formatted as "`domain\username`", or "`user@domain.com`"\. If using "`domain\username`" format, `domain` can either be the NetBIOS name or the fully qualified domain name\. If using "`user@domain.com`" format, the UserPrincipalName attribute can be used\. If you've verified your SAML\_Subject attribute is configured correctly and the problem persists, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## My fleet instances work for one user but don't cycle correctly<a name="troubleshooting-active-directory-3"></a>

Fleet instances are cycled after a user completes a session, ensuring that each user has a new instance\. When the cycled fleet instance is brought online, it joins the domain using the computer name of the previous instance\. To ensure that this operation happens successfully, the service account requires **Change Password** and **Reset Password** permissions on the organizational unit \(OU\) to which the computer object is joining\. Check the service account permissions and try again\. If the problem persists, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## My user Group Policy Objects aren't applying successfully<a name="troubleshooting-active-directory-4"></a>

By default, computer objects apply computer\-level policies based on the OU in which the computer object resides, while applying user\-level policies based on the OU in which the user resides\. If your user\-level policies aren't being applied, you can do one of the following: 

+ Move the user\-level policies to the OU in which the user Active Directory object resides

+ Enable computer\-level "loopback processing", which applies the user\-level policies in the computer object OU\. 

For more information, see [Loopback processing of Group Policy](https://support.microsoft.com/en-us/help/231287/loopback-processing-of-group-policy) at Microsoft Support\.

## My AppStream 2\.0 streaming instances aren't joining the Active Directory domain<a name="troubleshooting-active-directory-5"></a>

The Active Directory domain to use with AppStream 2\.0 must be accessible through its fully qualified domain name \(FQDN\) via the VPC in which your streaming instances are launched\.

**To test that your domain is accessible**

1. Launch an Amazon EC2 instance in the same VPC, subnet, and security groups that you use with AppStream 2\.0\.

1. Manually join the EC2 instance to your Active Directory domain using the FQDN \(for example, `yourdomain.exampleco.com`\) with the service account that you intend to use with AppStream 2\.0\. Use the following command in a Windows PowerShell console:

   ```
   netdom join computer /domain:FQDN /OU:path /ud:user /pd:password
   ```

   If this manual join fails, proceed to the next step\.

1. If you cannot manually join to your domain, open a command prompt and verify that you can resolve the FQDN using the `nslookup` command\. For example:

   ```
   nslookup yourdomain.exampleco.com
   ```

   Successful name resolution returns a valid IP address\. If you are unable to resolve your FQDN, you may need to update your VPC DNS servers by using a DHCP option set for your domain\. Then, come back to this step\. For more information, see [DHCP Options Sets](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html) in the *Amazon VPC User Guide*\.

1. If the FQDN resolves, validate connectivity by using the following `telnet` command\.

   ```
   telnet yourdomain.exampleco.com 389
   ```

   A successful connection shows a blank command prompt window without any connection errors\. You may need to install the Telnet Client feature on your EC2 instance\. For more information, see [Install Telnet Client](https://technet.microsoft.com/en-us/library/cc771275.aspx) in the Microsoft documentation\.

If you were not able to manually join the EC2 instance to your domain, but were successful in resolving the FQDN and testing connectivity with the Telnet Client, your VPC security groups may be preventing access\. Active Directory requires certain network port settings\. For more information, see [Active Directory and Active Directory Domain Services Port Requirements](https://technet.microsoft.com/en-us/library/dd772723.aspx) in the Microsoft documentation\.

## User login is taking a long time to complete on a domain\-joined streaming session<a name="troubleshooting-active-directory-6"></a>

AppStream 2\.0 performs a Windows login action after the end user provides their domain password, and then launches the application after successful authentication\. The login and launch time is impacted by many variables, such as network contention to the domain controllers or time taken to apply group policies to the streaming instance\. If domain authentication takes too long to complete, try the following actions\.

+ Minimize the network latency from your AppStream 2\.0 region to your domain controllers by choosing the correct domain controllers\. For example, if your fleet is in us\-east\-1, use domain controllers with high bandwidth and low latency to us\-east\-1 through Active Directory Sites and Services zone mappings\. For more information, see [Active Directory Sites and Services](https://technet.microsoft.com/en-us/library/cc730868.aspx) in the Microsoft documentation\.

+ Ensure that your group policies and user login scripts don't take prohibitively long to apply or execute\.

If your login to AppStream 2\.0 fails after 3 minutes with a message "An unknown error occurred," validate that your group policies are not restricting third\-party credential providers\. There are two policies that block AppStream 2\.0 from authenticating your domain users:

+ **Computer Configuration > Administrative Templates > Windows Components > Windows Logon Options > Disable or Enable software Secure Attention Sequence** — This policy should be set to **Enabled** for **Services**\.

+ **Computer Configuration > Administrative Templates > System > Logon > Exclude credential providers** — Ensure that the following CLSID is *not* listed: `e7c1bab5-4b49-4e64-a966-8d99686f8c7c`

## The changes I made in the image builder aren't reflected in end user streaming sessions<a name="troubleshooting-active-directory-7"></a>

User\-specific settings in the image builder are saved in the specific user profile, and do not persist to the streaming instances\. Examples include drive mounting, wallpaper changes, browser customizations, or Internet Explorer customizations\. You need to manage these settings using the Microsoft Active Directory Group Policy settings that are applied to the OUs under which your streaming instances are created\. 

To quickly test whether your Group Policy settings are applied to the end user, connect to your image builder, login as a domain user and test the experience\. For more information, see [Group Policy for Beginners](https://technet.microsoft.com/en-us/library/hh147307.aspx) in the Microsoft documentation\.

## Unable to access a domain resource in a domain joined streaming session but could access the resource from a domain\-joined image builder<a name="troubleshooting-active-directory-8"></a>

Confirm that your fleet is created in the same VPC, subnets, and security groups that your image builder is in, and that your user has the appropriate permission to access and use the domain resource\.