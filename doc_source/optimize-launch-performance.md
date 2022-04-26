# Optimizing the Launch Performance of Your Linux Applications<a name="optimize-launch-performance"></a>

AppStream 2\.0 lets you optimize the launch performance of your applications for your users’ streaming sessions\. When create and you add files to an application optimization manifest, the application will launch faster when first started on a new fleet instance\. However, this also increases the time that it takes for the fleet instances to be made available to users\. The optimization manifest is one line\-delimited text file for every application\.

You can create a manifest file \(such as <*your\-app*>\-manifest\.txt\) either manually or by following with the steps below\.

**To create a manifest file**

1. Make sure that the application that you are trying to optimize is launched and running\.

1. From a terminal in the Linux image builder, run the following command: 

   ps \-ef \| grep <*application\-process\-name*>

1. Search for the smallest PID number from the last step's output\. This is the PID for the root parent process of the application\.

1. Keep the application running and make sure to use the initial components required by your users\. This ensures that these components are captured by the optimization process\. 

1. Create a script file \(e\.g\., `~/getfilestool.sh`\) with the following content:

   ```
   #!/bin/bash
   ## usage getfilestool.sh $pid
   lsof -p $(pstree -p $1 | grep -o '([0-9]\+)' | grep -o '[0-9]\+' | tr '\012' ,)|grep REG | sed -n '1!p' | awk '{print $9}'|awk 'NF'
   ```

1. Make sure that the file can be run with the following command:

   \[ImageBuilderAdmin\]$ chmod u\+x \~/getfilestool\.sh

1. Run the following command to capture all of the running files from the root parent process found in step 3, and save it to a temporary manifest file\.

   \[ImageBuilderAdmin\]$ sudo \~/getfilestool\.sh <*root\-parent\-pid*> > /tmp/<y*our\-app*>\-manifest\.txt 

1. Verify the content of the optimization manifest, which is a line\-delimited text file for every application\.

You can specify the optimization manifest on a per\-application basis by using the Image Assistant command line interface \(CLI\) tool\. For more information, see [Image Assistant CLI Tool for Linux](image-assistant-cli.md)\.