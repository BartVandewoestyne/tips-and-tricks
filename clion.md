# Installation
In Ubuntu 20.04.4 LTS, you can install CLion as a self-contained snap package.  Since snaps update automatically, your CLion installation will always be up to date.
CLion is distributed via two channels:

* The *stable* channel includes only stable versions.  To install the latest stable release of CLion, run the following command:

 ```
 sudo snap install clion --classic
 ```
The `--classic` option is required because the CLion snap requires full access to the system, like a traditionally packaged application.
* The *edge* channel includes EAP builds.  To install the latest EAP build of CLion, run the following command:

 ```
 sudo snap install clion --classic --edge
 ```

# Running CLion
When the snap is installed, you can launch it by running the `clion.sh` command.

# Post install configuration

* To enable the back and forward navigation buttons, select *View > Appearance* and enable *Toolbar*.
* If you get Inotify-related warnings when running Clion on Linux, increase the limit of watch handles for inotify as explained in the blog post [Inotify Watches Limit (Linux)](https://youtrack.jetbrains.com/articles/IDEA-A-2/Inotify-Watches-Limit-Linux).

# Interesting plugins
* [cppcheck](https://plugins.jetbrains.com/plugin/8143-cppcheck)
* [SonarLint](https://plugins.jetbrains.com/plugin/7973-sonarlint)
* [GitToolBox](https://plugins.jetbrains.com/plugin/7499-gittoolbox)

# Useful features
* [viewing changes for a selection](https://www.jetbrains.com/help/clion/viewing-changes-information.html#changes_history)
