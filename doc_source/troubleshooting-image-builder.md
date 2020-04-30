# Troubleshooting Image Builders<a name="troubleshooting-image-builder"></a>

The following are possible issues you might have while using Amazon AppStream 2\.0 image builders\.

**Topics**
+ [I cannot connect to the internet from my image builder\.](#troubleshooting-01)
+ [When I tried installing my application, I see an error that the operating system version is not supported\.](#troubleshooting-02)
+ [I want to use a Windows PowerShell script to open my applications\.](#use-powershell-launch-application)
+ [I want to make ClickOnce applications available to users\.](#clickonce-applications)
+ [When I connect to my image builder, I see a login screen asking me to enter Ctrl\+Alt\+Delete to log in\. However, my local machine intercepts the key strokes\.](#troubleshooting-03)
+ [When I switched between admin and test modes, I saw a request for a password\. I don't know how to get a password\.](#troubleshooting-04)
+ [I get an error when I add my installed application\.](#troubleshooting-05)
+ [I accidentally quit a background service on the image builder and got disconnected\. I am now unable to connect to that image builder\.](#troubleshooting-06)
+ [The application fails to launch in test mode\.](#troubleshooting-07)
+ [The application could not connect to a network resource in my VPC\.](#troubleshooting-08)
+ [I customized my image builder desktop, but my changes are not available when connecting to a session after launching a fleet from the image I created\.](#troubleshooting-09)
+ [My application is missing a command line parameter when launching\.](#troubleshooting-10)
+ [I am unable to use my image with a fleet after installing an antivirus application\.](#troubleshooting-11)
+ [My image creation failed\.](#troubleshooting-12)
+ [The Image Assistant `create-image` operation failed with an error message that access to the PrewarmManifest\.txt is denied](#create-image-cli-operation-fails)

## I cannot connect to the internet from my image builder\.<a name="troubleshooting-01"></a>

Image builders cannot communicate to the internet by default\. To resolve this issue, launch your image builder in a VPC subnet that has internet access\. You can enable internet access from your VPC subnet using a [NAT gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)\. Or, you can configure an internet gateway in your VPC, and attach an Elastic IP address to your image builder\. For more information, see [Networking and Access for Amazon AppStream 2\.0](managing-network.md)\.

## When I tried installing my application, I see an error that the operating system version is not supported\.<a name="troubleshooting-02"></a>

Only applications that can be installed on Windows Server 2012 R2, Windows Server 2016, and Windows Server 2019 can be added to an AppStream 2\.0 image\. Check if your application is supported on one of these three operating systems, as applicable for your image builder\.

## I want to use a Windows PowerShell script to open my applications\.<a name="use-powershell-launch-application"></a>

You can use Windows PowerShell scripts to open your applications in the fleet instance\. You might want to do this to configure the application or environment before the application opens\. To launch a Windows PowerShell script for your application, specify the PowerShell \.exe file in Image Assistant\. Navigate to `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`, and specify the following launch parameters: 

\-file "C:\\Path\\To\\PowerShell\\Script\.ps1"

**Note**  
To allow the specified script to open the application, you must override the PowerShell script execution policy\. To do so, add **\-ExecutionPolicy Bypass** to the launch parameter\.

## I want to make ClickOnce applications available to users\.<a name="clickonce-applications"></a>

To make a ClickOnce application available to your AppStream 2\.0 users, you must install the application on your image builder first as an Administrator, and then as a Template User\. Because ClickOnce applications require a user\-specific installation, you must install your application as a Template User to enable users to launch the application from fleet instances\. To install the ClickOnce application as an Administrator and then as a Template User, perform these steps\.

1. Open the AppStream 2\.0 console at [https://console\.aws\.amazon\.com/appstream2](https://console.aws.amazon.com/appstream2)\.

1. In the left navigation pane, choose **Images**, **Image Builder**\.

1. In the list, select the image builder that you want to use, and log into it as an Administrator\.

1. Create a batch file that calls the `appref-ms` file within the user profile\. Use the %APPDATA% environment variable to replace C:\\Users\\username\\AppData\\Roaming\. Here is an example batch file call:

   ```
   explorer "%APPDATA%\Microsoft\Windows\Start Menu\Programs\Company\ClickOnce.appref-ms"
   ```

1. On the image builder desktop, open Image Assistant\. 

1. On the **Configure Apps** page, choose **Switch user**\.

1. On the **Local User** tab, choose **Template User**\.

1. After you log in as a Template User, install the application again\. 

1. On the image builder desktop, open Image Assistant\.

1. On the **Configure Apps** page, open the ClickOnce application to verify that it functions correctly\. After you finish testing, choose **Switch user**\.

1. Log back in as an Administrator and perform the required steps in Image Assistant to finish creating your image\.

## When I connect to my image builder, I see a login screen asking me to enter Ctrl\+Alt\+Delete to log in\. However, my local machine intercepts the key strokes\.<a name="troubleshooting-03"></a>

Your client might intercept certain key combinations locally instead of sending them to the image builder session\. To reliably send the Ctrl\+Alt\+Delete key combination to the image builder, choose **Admin Commands**, **Send Ctrl\+Alt\+Delete**\. The **Admin Commands** menu is available on the top right corner of the image builder session toolbar\.

## When I switched between admin and test modes, I saw a request for a password\. I don't know how to get a password\.<a name="troubleshooting-04"></a>

AppStream 2\.0 usually logs you into the user mode that you choose automatically\. On some occasions, the switch might not happen automatically\. If a password is requested, choose **Admin Commands**, **Log me in**\. This sends a one\-time password, securely, to your image builder and pastes it into the **Password** field\.

## I get an error when I add my installed application\.<a name="troubleshooting-05"></a>

Check if your application type is supported\. You can add applications of the types `.exe`, `.lnk`, and `.bat`\.

Check if your application is installed under the `C:\Users` folder hierarchy\. Any application installed under `C:\Users` is not supported\. Select a different installation folder under `C:\` when installing the application\.

## I accidentally quit a background service on the image builder and got disconnected\. I am now unable to connect to that image builder\.<a name="troubleshooting-06"></a>

Try stopping the image builder, restarting it and connecting to it again\. If the problem persists, you must launch \(create\) a new image builder\. Do not stop any background services running on the image builder instance\. Doing so might interrupt your image builder session or interfere with the image creation\.

## The application fails to launch in test mode\.<a name="troubleshooting-07"></a>

Check if your application requires elevated user privileges or any special permissions that are usually available only to an administrator\. The Image Builder Test mode has the same limited permissions on the image builder instance as your end users have on an AppStream 2\.0 test fleet\. If your applications require elevated permissions, they do not launch in the Image Builder Test mode\.

## The application could not connect to a network resource in my VPC\.<a name="troubleshooting-08"></a>

Check if the image builder was launched in the correct VPC subnet\. You might also need to verify that the route tables in your VPC are configured to allow a connection\.

## I customized my image builder desktop, but my changes are not available when connecting to a session after launching a fleet from the image I created\.<a name="troubleshooting-09"></a>

Changes that are saved as part of a local user session, such as time settings, are not persisted when creating an image\. To persist any local user session changes, add them to the local group policy on the image builder instance\.

## My application is missing a command line parameter when launching\.<a name="troubleshooting-10"></a>

You can provide a command line parameter when using image builder to add an application to an image\. If the launch parameters for the application do not change for each user, you can enter them while adding an application to the image in the image builder instance\.

If the launch parameters are different for every launch, you can pass them programmatically when using the `CreateStreamingURL` API\. Set the `sessionContext` and `applicationID` parameters in the API fields\. The sessionContext is included as a command line option when launching the application\.

If the launch parameters must be computed on the fly, you can launch your application using a script\. You can parse the `sessionContext` parameter within your script before launching your application with a computed parameter\.

## I am unable to use my image with a fleet after installing an antivirus application\.<a name="troubleshooting-11"></a>

You can install any tools, including antivirus programs, on your AppStream 2\.0 stack by using the image builder before creating an image\. However, these programs should not block any network ports or stop any processes that are used by the AppStream 2\.0 service\. We recommend testing your application in Image Builder Test mode before creating an image and attempting to use it with a fleet\.

## My image creation failed\.<a name="troubleshooting-12"></a>

Verify that you did not make any changes to AppStream 2\.0 services before starting the image creation\. Try creating your image again; if it fails, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## The Image Assistant `create-image` operation failed with an error message that access to the PrewarmManifest\.txt is denied<a name="create-image-cli-operation-fails"></a>

The application optimization manifest was created with elevated privileges\. To create the image, do either of the following, and then try again:
+ Run the Image Assistant command line interface \(CLI\) executable file \(Image\-Assistant\.exe\) with administrator privileges\.
+ Delete the application optimization manifest file\.