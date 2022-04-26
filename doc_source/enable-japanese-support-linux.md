# Tutorial: Enable Japanese Support for Your Linux Images<a name="enable-japanese-support-linux"></a>

This tutorial describes how to enable Japanese support for a Linux image\. This enables applications on the image to display Japanese characters, and streaming users to use the Japanese input method in the streaming sessions from the image\.

**Topics**
+ [Step 1: Install Japanese Font and Input Method](#tutorial-japanese-font)
+ [Step 2: Set the System Time Zone](#tutorial-japanese-zone)
+ [Step 3: Set the System Locale and Display Language](#tutorial-japanese-locale)
+ [Step 4: Configure the Input Methods](#tutorial-japanese-input)
+ [Step 5: Set the Keyboard Layout](#tutorial-japense-keyboard)
+ [Step 6: Verify on Image Builder](#tutorial-japense-verify)
+ [Step 7: Create the Image](#tutorial-japanese-create)

## Step 1: Install Japanese Font and Input Method<a name="tutorial-japanese-font"></a>

In this step, you connect a Linux image builder and install the font and input method packages of your choice\.

**To install Japanese font and input method**

1. Connect to the image builder by doing either of the following: 
   + [Use the AppStream 2\.0 console](managing-image-builders-connect.md#managing-image-builders-connect-console) \(for web connections only\)
   + [Create a streaming URL](managing-image-builders-connect.md#managing-image-builders-connect-streaming-URL) \(for web or AppStream 2\.0 client connections\)
**Note**  
You will be logged in as an ImageBuilderAdmin user to the Amazon Linux GNOME desktop and have root admin privileges\.

1. Install the font and input method that you need\. To do this, open the Terminal application, then run the following commands:

   sudo yum install vlgothic\-p\-fonts\.noarch

   sudo yum install ibus\-kkc\.x86\_64

## Step 2: Set the System Time Zone<a name="tutorial-japanese-zone"></a>

To set the system time zone, run the following command:

sudo timedatectl set\-timezone "Asia/Tokyo"

## Step 3: Set the System Locale and Display Language<a name="tutorial-japanese-locale"></a>

To set the system local and display language, run the following commands\. 

**To set the system locale and display language**

1. Update the `cloud-init config` file by running the command sudo vim /etc/cloud/cloud\.cfg, and change **local** to **locale: ja\_JP\.utf8**, then save and close the file\.

1. Update the system settings by running sudo localectl set\-locale LANG=ja\_JP\.utf8\.

1. Update the Gnome shell settings by running sudo gsettings set org\.gnome\.system\.locale region "ja\_JP\.utf8"\.

## Step 4: Configure the Input Methods<a name="tutorial-japanese-input"></a>

Configure the input methods for the application you want to add to the image\. For more information about how install an application, generate a manifest file, and create default settings, see [Tutorial: Create a Custom Linux\-Based AppStream 2\.0 Image](tutorial-create-linux-image.md)\. In this step, we assume that you’ve already installed the application Firefox, which is located at `/usr/local/firefox/firefox`\.

**To configure the input methods**

1. Create a script by running the command sudo vim /usr/local/bin/update\-input\-method\.sh, and add the following content to the script:

   ```
   #!/bin/bash
   
   function start_process()
   {
       command=$1
       process_name=$2
   
       process_count=$(pgrep $process_name -c)
       echo "$(date) current $process_name count: $process_count"
       while [ $process_count -lt 1 ]
       do
           echo "$(date) starting $process_name"
           eval $command
           sleep 1
           process_count=$(pgrep $process_name -c)
       done
       echo "$(date) $process_name started"
   }
   
   start_process "ibus-daemon --xim &" "ibus-daemon"
   start_process "/usr/libexec/ibus-engine-kkc --ibus &" "ibus-engine-kkc"
   
   gsettings set org.gnome.desktop.input-sources sources "[('ibus','kkc'), ('xkb', 'us')]"
   gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Control>space']"
   gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward "['<Shift><Control>space']"
   
   echo "$(date) updated input source and switch shortcut"
   ```

   In the script above, the first input source \(‘ibus’, ‘kkc’\) is the default input method\. You can change the default input method by changing the order of input sources\. In addition, “Control\+Space” and “Shift\+Control\+Space” are specified as shortcut key combinations for switching between input methods\. You can specify your own key combinations that your users can use to switch input methods during streaming sessions\.

1. Create the script for launching the application \(Firefox\) that you will add to the image\. To do this, run the command sudo vim /usr/local/bin/firefox\-jp\.sh, then add following content to the script:

   ```
   #!/bin/bash
   
   /usr/local/bin/update-input-method.sh > /var/tmp/update-input-method.log 2>&1 &
   
   /usr/local/firefox/firefox &
   ```

1. Add run permission to both scripts by running following the commands:

   sudo chmod \+x /usr/local/bin/update\-input\-method\.sh

   sudo chmod \+x /usr/local/bin/firefox\-jp\.sh

1. If you already created the optimization manifest file for the application run the following commands to add the application launch script to the application catalog:

   ```
   sudo AppStreamImageAssistant add-application \
   --name firefox \
   --absolute-app-path /usr/local/bin/firefox-jp.sh \
   --display-name firefox \
   --absolute-icon-path /usr/local/firefox/browser/chrome/icons/default/default128.png \
   --absolute-manifest-path /tmp/firefox-manifest.txt
   ```

Alternatively, you can also configure the input methods by adding the script update\-input\-method\.sh as a separate application to the application catalog for the image\. During streaming sessions, your users can launch this application to enable Japanese input, and switch between input methods with specified shortcut keys within the same session\.

## Step 5: Set the Keyboard Layout<a name="tutorial-japense-keyboard"></a>

Set the keyboard layout to match the keyboards your users will use during streaming sessions\. You can use the command localectl list\-keymaps to list all the available keymaps, and use the command sudo localectl set\-keymap jp106 to set the keymap to the Japanese keyboard of 106 keys, for example\.

## Step 6: Verify on Image Builder<a name="tutorial-japense-verify"></a>

To verify on image builder, first reboot the image builder by running the command sudo shutdown \-r now\. After reboot, connect to the image builder again, and verify that everything, including time zone, locale, language, and input method, works as expected\.

## Step 7: Create the Image<a name="tutorial-japanese-create"></a>

Create the image on the image builder\. For more information, see [Tutorial: Create a Custom Linux\-Based AppStream 2\.0 Image](tutorial-create-linux-image.md)\. Make sure to create default application settings, including the regional settings you just configured\. For more information, see "Creating Default Application Settings for Your Users" in [Create Your Linux\-Based Images](create-linux-based-images.md)\.

All of the Linux fleet instances created from this image will have the same default time zone, locale, language, and input method settings that you configured for the image\.