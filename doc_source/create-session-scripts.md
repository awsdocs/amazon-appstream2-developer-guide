# Creating Session Scripts<a name="create-session-scripts"></a>

AppStream 2\.0 provides on\-instance session scripts on both Windows\- and Linux\-based streaming instances\. For more information about session scripts, see [Use Session Scripts to Manage Your AppStream 2\.0 Users' Streaming Experience](use-session-scripts.md)\.

Session scripts are specified within an AppStream 2\.0 image\. To locate the session scripts configuration file on a Linux instance, navigate to `/opt/appstream/SessionScripts/config.json`\. The following code is a sample `config.json` file that specifies a session start script named “`test-session-start`” and a session end script named “`test-session-stop`” together with their runtime parameters\. Make sure that the scripts referenced in `config.json` have run permissions and a command interpreter is defined \(for example, \#\!/bin/bash\)\. 

```
{
     "SessionStart": {
          "Executables": [
               {
                    "Context": "system",
                    "Filename": "/opt/appstream/SessionScripts/test-session-start",
                    "Arguments": "arg1",
                    "S3LogEnabled": true
               }
          ],
          "WaitingTime": 30
     },
     "SessionTermination": {
          "Executables": [
               { 
                    "Context": "system",
                    "Filename": "/opt/appstream/SessionScripts/test-session-stop", 
                    "Arguments": "arg2", 
                    "S3LogEnabled": true
               }
          ],
          "WaitingTime": 30
     }
}
```