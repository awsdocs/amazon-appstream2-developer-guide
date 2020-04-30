# Troubleshooting Active Directory Domain Join<a name="troubleshooting-active-directory"></a>

The following are possible issues you might have while setting up and using Active Directory with Amazon AppStream 2\.0\. For help troubleshooting notification codes, see [Troubleshooting Notification Codes](troubleshooting-notification-codes.md)\.

**Topics**
+ [My image builders and fleet instances are stuck in the PENDING state\.](#troubleshooting-active-directory-1)
+ [My users aren't able to log in with the SAML application\.](#troubleshooting-active-directory-2)
+ [My fleet instances work for one user but don't cycle correctly\.](#troubleshooting-active-directory-3)
+ [My user Group Policy objects aren't being successfully applied\.](#troubleshooting-active-directory-4)
+ [My AppStream 2\.0 streaming instances aren't joining the Active Directory domain\.](#troubleshooting-active-directory-5)
+ [User login is taking a long time to complete on a domain\-joined streaming session\.](#troubleshooting-active-directory-6)
+ [My users can't access a domain resource in a domain\-joined streaming session, but they can access the resource from a domain\-joined image builder\.](#troubleshooting-active-directory-8)

## My image builders and fleet instances are stuck in the PENDING state\.<a name="troubleshooting-active-directory-1"></a>

Image builders and fleet instances can take up to 25 minutes to move into a ready state and become available\. If your instances are taking longer than 25 minutes to become available, in Active Directory, verify whether new computer objects were created in the correct organizational units \(OUs\)\. If there are new objects, the streaming instances will be available soon\. If the objects aren't there, check the directory configuration details in your AppStream 2\.0 Directory Config: Directory name \(the fully qualified domain name of the directory, service account username and password, and the OU distinguished name\. 

Image builder and fleet errors are displayed in the AppStream 2\.0 console on the **Notifications** tab for the fleet or image builder\. Fleet errors are also available using the AppStream 2\.0 API through the [DescribeFleets](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_DescribeFleets.html) operation or the CLI command [describe\-fleets](https://docs.aws.amazon.com/cli/latest/reference/appstream/describe-fleets.html)\.

## My users aren't able to log in with the SAML application\.<a name="troubleshooting-active-directory-2"></a>

AppStream 2\.0 relies on the SAML\_Subject "NameID" attribute from your identity provider to populate the username field to log in your user\. The username can either be formatted as "`domain\username`", or "`user@domain.com`"\. If you are using "`domain\username`" format, `domain` can either be the NetBIOS name or the fully qualified domain name\. If using "`user@domain.com`" format, the UserPrincipalName attribute can be used\. If you've verified your SAML\_Subject attribute is configured correctly and the problem persists, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## My fleet instances work for one user but don't cycle correctly\.<a name="troubleshooting-active-directory-3"></a>

Fleet instances are cycled after a user completes a session, ensuring that each user has a new instance\. When the cycled fleet instance is brought online, it joins the domain using the computer name of the previous instance\. To ensure that this operation happens successfully, the service account requires **Change Password** and **Reset Password** permissions on the organizational unit \(OU\) to which the computer object is joining\. Check the service account permissions and try again\. If the problem persists, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## My user Group Policy objects aren't being successfully applied\.<a name="troubleshooting-active-directory-4"></a>

By default, computer objects apply computer\-level policies based on the OU in which the computer object resides, while applying user\-level policies based on the OU in which the user resides\. If your user\-level policies aren't being applied, you can do one of the following: 
+ Move the user\-level policies to the OU in which the user Active Directory object resides
+ Enable computer\-level loopback processing, which applies the user\-level policies in the computer object OU\. 

For more information, see [Loopback processing of Group Policy](https://support.microsoft.com/en-us/help/231287/loopback-processing-of-group-policy) at Microsoft Support\.

## My AppStream 2\.0 streaming instances aren't joining the Active Directory domain\.<a name="troubleshooting-active-directory-5"></a>

The Active Directory domain to use with AppStream 2\.0 must be accessible through its fully qualified domain name \(FQDN\) through the VPC in which your streaming instances are launched\.

**To test that your domain is accessible**

1. Launch an Amazon EC2 instance in the same VPC, subnet, and security groups that you use with AppStream 2\.0\.

1. Manually join the EC2 instance to your Active Directory domain using the FQDN \(for example, `yourdomain.exampleco.com`\) with the service account that you intend to use with AppStream 2\.0\. Use the following command in a Windows PowerShell console:

   ```
   netdom join computer /domain:FQDN /OU:path /ud:user /pd:password
   ```

   If this manual join fails, go to the next step\.

1. If you cannot manually join to your domain, open a command prompt and verify that you can resolve the FQDN using the `nslookup` command\. For example:

   ```
   nslookup yourdomain.exampleco.com
   ```

   Successful name resolution returns a valid IP address\. If you are unable to resolve your FQDN, you might need to update your VPC DNS servers by using a DHCP option set for your domain\. Then, come back to this step\. For more information, see [DHCP Options Sets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_DHCP_Options.html) in the *Amazon VPC User Guide*\.

1. If the FQDN resolves, use the `telnet` command to validate connectivity\.

   ```
   telnet yourdomain.exampleco.com 389
   ```

   A successful connection shows a blank command prompt window without any connection errors\. You might need to install the Telnet Client feature on your EC2 instance\. For more information, see [Install Telnet Client](https://technet.microsoft.com/en-us/library/cc771275.aspx) in the Microsoft documentation\.

If you were not able to manually join the EC2 instance to your domain, but were successful in resolving the FQDN and testing connectivity with the Telnet Client, your VPC security groups might be preventing access\. Active Directory requires certain network port settings\. For more information, see [Active Directory and Active Directory Domain Services Port Requirements](https://technet.microsoft.com/en-us/library/dd772723.aspx) in the Microsoft documentation\.

## User login is taking a long time to complete on a domain\-joined streaming session\.<a name="troubleshooting-active-directory-6"></a>

AppStream 2\.0 performs a Windows login action after users provide their domain password\. After successful authentication, AppStream 2\.0 launches the application\. The login and launch times are impacted by many variables, such as network contention for the domain controllers or the time it takes to apply Group Policy settings to the streaming instance\. If domain authentication takes too long to complete, try performing the following actions\.
+ Minimize the network latency from your AppStream 2\.0 Region to your domain controllers by choosing the correct domain controllers\. For example, if your fleet is in `us-east-1`, use domain controllers with high bandwidth and low latency to `us-east-1` through Active Directory Sites and Services zone mappings\. For more information, see [Active Directory Sites and Services](https://technet.microsoft.com/en-us/library/cc730868.aspx) in the Microsoft documentation\.
+ Ensure that your Group Policy settings and user login scripts don't take prohibitively long to apply or run\.

If your domain users' login to AppStream 2\.0 fails with the message "An unknown error occurred," you might need to update the Group Policy settings described in [Before You Begin Using Active Directory with AppStream 2\.0](active-directory-prerequisites.md)\. Otherwise, these settings might prevent AppStream 2\.0 from authenticating and logging in your domain users\.

## My users can't access a domain resource in a domain\-joined streaming session, but they can access the resource from a domain\-joined image builder\.<a name="troubleshooting-active-directory-8"></a>

Confirm that your fleet is created in the same VPC, subnets, and security groups as your image builder, and that your user has the permissions required to access and use the domain resource\.