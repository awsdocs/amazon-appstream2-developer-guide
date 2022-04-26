# Creating Default Application Settings for Your Users<a name="create-default-app-settings"></a>

You can create default application settings for your users' applications\. This allows your users to get started without having to individually configure the applications they need\. You can create default application settings by copying the corresponding config files to the `/etc/skel` folder\. You can either copy all of the config files, or only the config files for the individual applications you need, to the `/etc/skel` folder\. 

If you want to make all of the settings on the Linux Image Builder instance available to streaming users, run the following commands: 

\[ImageBuilderAdmin\]$ sudo mkdir /etc/skel/\.config/

\[ImageBuilderAdmin\]$ sudo cp \-R \~/\.config/\* /etc/skel/\.config

If you want to make the settings of specific applications available to streaming users, run the following commands, where `your-app` is the folder containing your application's files: 

\[ImageBuilderAdmin\]$ sudo mkdir /etc/skel/\.config

\[ImageBuilderAdmin\]$ sudo cp \-R \~/\.config/*your\-app* /etc/skel/\.config 