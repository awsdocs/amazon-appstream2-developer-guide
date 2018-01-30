# Tutorial: Setting Up the Active Directory<a name="active-directory-directory-setup"></a>

To use Active Directory domain support in AppStream 2\.0, you must first register your directory configuration by creating a Directory Config object using the AppStream 2\.0 management console or using AWS SDK or AWS CLI\. You can then use the directory configuration to launch domain\-joined fleets and image builders\. 


+ [Step 1: Create a Directory Configuration](#active-directory-setup-config)
+ [Step 2: Create an Image Using a Domain\-Joined Image Builder](#active-directory-setup-image-builder)
+ [Step 3: Create a Domain\-Joined Fleet](#active-directory-setup-fleet)
+ [Step 4: Configure SAML 2\.0](#active-directory-setup-saml)

## Step 1: Create a Directory Configuration<a name="active-directory-setup-config"></a>

This step creates the necessary Active Directory configuration in AppStream 2\.0\. The directory configuration is used in later steps\.

If you are using the AWS SDK, you can use the [CreateDirectoryConfig](http://docs.aws.amazon.com/appstream2/latest/APIReference/API_CreateDirectoryConfig.html) operation\. If you are using the AWS CLI, you can use the [create\-directory\-config](http://docs.aws.amazon.com/cli/latest/reference/appstream/create-directory-config.html) command\.

**To create a directory configuration using the console**

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. On the left navigation pane, choose **Directory Configs**, **Create Directory Config**\.

1. For **Directory Name**, provide the fully qualified domain name \(FQDN\) of the Active Directory\. Each region can have only one **Directory Config** value with a specific directory name\.

1. For **Service Account Name**, enter the service account name with the required permissions\. For more information, see [Granting Permissions to Create and Manage Active Directory Computer Objects](active-directory-admin.md#active-directory-permissions)\. The service account name must be in the format `DOMAIN\username`\.

1. For **Password** and **Confirm Password**, type the directory password for the specified service account\.

1. For **Organizational Unit \(OU\)**, type the distinguished name of at least one OU for streaming instance computer objects\. The default Computers container is not an OU and cannot be used by AppStream 2\.0\. For more information, see [Finding the Organizational Unit Distinguished Name](active-directory-admin.md#active-directory-oudn)\.

1. To add more than one OU, select the plus sign \(**\+**\) next to **Organizational Unit \(OU\)**\. To remove OUs, choose the **x** icon\.

1. Choose **Next**\.

1. Review the configuration information and choose **Create**\.

## Step 2: Create an Image Using a Domain\-Joined Image Builder<a name="active-directory-setup-image-builder"></a>

Using the AppStream 2\.0 image builder, create a new image with Active Directory domain\-join capabilities\. Note that the fleet and image can have different domains\. You join the image builder to a domain to enable domain join and to install apps\. Fleet domain join is discussed in the next section\.

**To create an image for launching domain\-joined fleets**

1. Refer to the procedures in [Tutorial: Create a Custom Image](tutorial-image-builder.md)\.

1. For the base image selection step, use an AWS base image released on or after July 24, 2017\. For a current list of released AWS images, see [Amazon AppStream 2\.0 Windows Image Version History](base-image-version-history.md)\.

1. For **Step 3: Configure Network**, select a VPC and subnets with network connectivity to your Active Directory environment\. Select the security groups that are set up to allow access to your directory via your VPC subnets\.

1. Also in **Step 3: Configure Network**, expand the **Active Directory Domain \(Optional\)** section, and select values for **Directory Name** and **Directory OU** to which the image builder should be joined\.

1. Review the image builder configuration and choose **Create**\.

1. Wait for the new image builder to reach a **Running** state, and choose **Connect**\.

1. Log in to the image builder as Administrator or as a directory user with local administrator permissions\. For more information, see [Providing Local Administrator Permissions for Image Builders](active-directory-admin.md#active-directory-image-builder-local-admin)\.

1. Complete the steps provided in [Tutorial: Create a Custom Image](tutorial-image-builder.md) to install apps and create the new image\.

## Step 3: Create a Domain\-Joined Fleet<a name="active-directory-setup-fleet"></a>

Using the private image created in the previous step, create an Active Directory domain\-joined fleet for streaming apps\. The domain can be different than the one that was used for the image builder to create the image\.

**To create a domain\-joined fleet**

1. Follow the procedures in [Create a Fleet](set-up-stacks-fleets.md#set-up-stacks-fleets-create)\.

1. For the image selection step, use the image that was created in the previous step, [Step 2: Create an Image Using a Domain\-Joined Image Builder](#active-directory-setup-image-builder)\.

1. For **Step 4: Configure Network**, select a VPC and subnets with network connectivity to your Active Directory environment\. Select the security groups that are set up to allow communication to your domain\.

1. Also in **Step 4: Configure Network**, expand the **Active Directory Domain \(Optional\)** section, and select values for **Directory Name** and **Directory OU** to which the fleet should be joined\.

1. Review the fleet configuration and choose **Create**\.

1. Complete the remaining steps provided in [Create AppStream 2\.0 Stacks and Fleets](set-up-stacks-fleets.md) so that your fleet is associated with a stack and running\.

## Step 4: Configure SAML 2\.0<a name="active-directory-setup-saml"></a>

Your users must use your SAML 2\.0\-based user federation to launch streaming sessions from your domain\-joined fleet\.

**To configure SAML 2\.0 for single sign\-on access**

1. Refer to the procedures in [Setting Up SAML](external-identity-providers-setting-up-saml.md)\.

1. AppStream 2\.0 requires that the SAML\_Subject "NameID" attribute specifies the domain username for the user logging in\. The username must be provided in the format of "`domain\username`" using the sAMAccountName or "`username@domain.com`" using userPrincipalName\. If using the sAMAccountName format, the `domain` can be specified using either the NetBIOS name or the fully qualified domain name \(FQDN\)\.

1. Provide access to your Active Directory users or groups to enable access to the AppStream 2\.0 stack from your identity provider application portal\.

1. Complete the remaining steps provided in [Setting Up SAML](external-identity-providers-setting-up-saml.md)\.

**To log in a user with SAML 2\.0**

1. Log in to your SAML 2\.0 provider's application catalog and launch the AppStream 2\.0 SAML app created in the previous procedure\.

1. When you see the AppStream 2\.0 app catalog, select an application to launch\.

1. When you see a loading icon, you are prompted to provide a password\. The domain username provided by your SAML 2\.0 identity provider appears above the password field\. Provide your password, and choose **log in**\.

The streaming instance performs the Windows login procedure, and the selected app launches\.