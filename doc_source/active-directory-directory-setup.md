# Tutorial: Setting Up Active Directory<a name="active-directory-directory-setup"></a>

To use Active Directory with AppStream 2\.0, you must first register your directory configuration by creating a Directory Config object in AppStream 2\.0\. This object includes the information required to join streaming instances to an Active Directory domain\. You create a Directory Config object by using the AppStream 2\.0 management console, AWS SDK, or AWS CLI\. You can then use your directory configuration to launch domain\-joined fleets and image builders\. 

**Topics**
+ [Step 1: Create a Directory Config Object](#active-directory-setup-config)
+ [Step 2: Create an Image by Using a Domain\-Joined Image Builder](#active-directory-setup-image-builder)
+ [Step 3: Create a Domain\-Joined Fleet](#active-directory-setup-fleet)
+ [Step 4: Configure SAML 2\.0](#active-directory-setup-saml)

## Step 1: Create a Directory Config Object<a name="active-directory-setup-config"></a>

The Directory Config object that you create in AppStream 2\.0 will be used in later steps\.

If you are using the AWS SDK, you can use the [CreateDirectoryConfig](https://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateDirectoryConfig.html) operation\. If you are using the AWS CLI, you can use the [create\-directory\-config](https://docs.aws.amazon.com/cli/latest/reference/appstream/create-directory-config.html) command\.

**To create a Directory Config object by using the AppStream 2\.0 console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the navigation pane, choose **Directory Configs**, **Create Directory Config**\.

1. For **Directory Name**, provide the fully qualified domain name \(FQDN\) of the Active Directory domain \(for example, `corp.example.com`\)\. Each region can have only one **Directory Config** value with a specific directory name\.

1. For **Service Account Name**, enter the name of an account that can create computer objects and that has permissions to join the domain\. For more information, see [Granting Permissions to Create and Manage Active Directory Computer Objects](active-directory-admin.md#active-directory-permissions)\. The account name must be in the format `DOMAIN\username`\.

1. For **Password** and **Confirm Password**, type the directory password for the specified account\.

1. For **Organizational Unit \(OU\)**, type the distinguished name of at least one OU for streaming instance computer objects\. The default Computers container is not an OU and cannot be used by AppStream 2\.0\. For more information, see [Finding the Organizational Unit Distinguished Name](active-directory-admin.md#active-directory-oudn)\.

1. To add more than one OU, select the plus sign \(**\+**\) next to **Organizational Unit \(OU\)**\. To remove OUs, choose the **x** icon\.

1. Choose **Next**\.

1. Review the configuration information and choose **Create**\.

## Step 2: Create an Image by Using a Domain\-Joined Image Builder<a name="active-directory-setup-image-builder"></a>

Next, using the AppStream 2\.0 image builder, create a new image with Active Directory domain\-join capabilities\. Note that the fleet and image can be members of different domains\. You join the image builder to a domain to enable domain join and to install applications\. Fleet domain join is discussed in the next section\.

**To create an image for launching domain\-joined fleets**

1. Follow the procedures in [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md)\.

1. For the base image selection step, use an AWS base image released on or after July 24, 2017\. For a current list of released AWS images, see [AppStream 2\.0 Base Image Version History](base-image-version-history.md)\.

1. For **Step 3: Configure Network**, select a VPC and subnets with network connectivity to your Active Directory environment\. Select the security groups that are set up to allow access to your directory through your VPC subnets\.

1. Also in **Step 3: Configure Network**, expand the **Active Directory Domain \(Optional\)** section, and select values for the **Directory Name** and **Directory OU** to which the image builder should be joined\.

1. Review the image builder configuration and choose **Create**\.

1. Wait for the new image builder to reach a **Running** state, and choose **Connect**\.

1. Log in to the image builder in Administrator mode or as a directory user with local administrator permissions\. For more information, see [Granting Local Administrator Rights on Image Builders](active-directory-admin.md#active-directory-image-builder-local-admin)\.

1. Complete the steps in [Tutorial: Create a Custom AppStream 2\.0 Image by Using the AppStream 2\.0 Console](tutorial-image-builder.md) to install applications and create a new image\.

## Step 3: Create a Domain\-Joined Fleet<a name="active-directory-setup-fleet"></a>

Using the private image created in the previous step, create an Active Directory domain\-joined fleet for streaming applications\. The domain can be different than the one that you used for the image builder to create the image\.

**To create a domain\-joined fleet**

1. Follow the procedures in [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

1. For the image selection step, use the image that was created in the previous step, [Step 2: Create an Image by Using a Domain\-Joined Image Builder](#active-directory-setup-image-builder)\.

1. For **Step 4: Configure Network**, select a VPC and subnets with network connectivity to your Active Directory environment\. Select the security groups that are set up to allow communication to your domain\.

1. Also in **Step 4: Configure Network**, expand the **Active Directory Domain \(Optional\)** section and select the values for the **Directory Name** and **Directory OU** to which the fleet should be joined\.

1. Review the fleet configuration and choose **Create**\.

1. Complete the remaining steps in [Create an AppStream 2\.0 Fleet and Stack](set-up-stacks-fleets.md) so that your fleet is associated with a stack and running\.

## Step 4: Configure SAML 2\.0<a name="active-directory-setup-saml"></a>

Your users must use your SAML 2\.0\-based identity federation environment to launch streaming sessions from your domain\-joined fleet\.

**To configure SAML 2\.0 for single sign\-on access**

1. Follow the procedures in [Setting Up SAML](external-identity-providers-setting-up-saml.md)\.

1. AppStream 2\.0 requires that the SAML\_Subject `NameID` value for the user who is logging in be provided in either of the following formats:
   + `domain\username` using the sAMAccountName
   + `username@domain.com` using the userPrincipalName

   If you are using the sAMAccountName format, you can specify the `domain` by using either the NetBIOS name or the fully qualified domain name \(FQDN\)\.

1. Provide access to your Active Directory users or groups to enable access to the AppStream 2\.0 stack from your identity provider application portal\.

1. Complete the remaining steps in [Setting Up SAML](external-identity-providers-setting-up-saml.md)\.

**To log in a user with SAML 2\.0**

1. Log in to your SAML 2\.0 provider's application catalog and open the AppStream 2\.0 SAML application that you created in the previous procedure\.

1. When the AppStream 2\.0 application catalog is displayed, select an application to launch\.

1. When a loading icon is displayed, you are prompted to provide a password\. The domain user name provided by your SAML 2\.0 identity provider appears above the password field\. Enter your password, and choose **log in**\.

The streaming instance performs the Windows login procedure, and the selected application opens\.