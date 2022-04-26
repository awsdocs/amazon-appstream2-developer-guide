# Creating Default Environment Variables for Your Linux Users<a name="create-default-variables-linux"></a>

You can create environment variables on a Linux Image Builder instance\. Creating environment variables makes them available on streaming instances created from that image\. 

**To create environment variables for your users**

1. If the folder `/etc/profile` doesn’t exist, run the following command to create it:

   \[ImageBuilderAdmin\]$ sudo mkdir \-p /etc/profile\.d 

1. To create a new shell script file \(for example, my\-environment\.sh\) in this folder, run the following command:

   \[ImageBuilderAdmin\]$ vim my\-environment\.sh

1. On first line of the script file, add the following content: 

   \#\!/bin/sh 

1. For each subsequent line, add an export command to set the environment variables for your image\. The following example adds `$HOME/bin` to the `PATH` variable: 

   export PATH=”$HOME/bin:$PATH”

1. Press the **Esc** key to return to command mode in vim, then run the following command to save your script and exit vim: 

   :x

1. Run the following command to allow the script to run as a program: 

   \[ImageBuilderAdmin\]$ chmod \+x my\-environment\.sh