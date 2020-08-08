## About ChatMe App
ChatMe App is an pplication built using Beeware, a Python framework

BeeWare allows you to write your app in Python and release it on multiple platforms(iOS, Windows, Linux, Android etc). No need to rewrite the app in multiple programming languages. It means no issues with build tools, environments, compatibility, etc.


#### Getting Started
###### Install Python3
If you’re on Linux, you’ll install Python using the system package manager (apt on Debian/Ubuntu/Mint; dnf on Fedora, or pacman on Arch).

For this project I used Ubuntu, a debian based distro which comes with inbuild Python3. If you are using a different OS then I'll refer you to follow [installation guidlines](https://realpython.com/installing-python/)

###### Install dependencies
Next, install the additional dependencies needed for your operating system:
For this case I'll install Ubuntu dependancies, which works for all Debian based distros like Linux Mint, Debian, Kali Linux, Elementary OS, etc


```text
$ sudo apt-get update

$ sudo apt-get install git python3-dev python3-venv libgirepository1.0-dev libcairo2-dev libpango1.0-dev libwebkitgtk-3.0-0 gir1.2-webkit-3.0

```
To get how to install these dependacies on different Os eg Windows, Mac and other Linux distros [check guidance](https://docs.beeware.org/en/latest/tutorial/tutorial-0.html/)

Briefcase also uses a tool called AppImage to build binaries that can be used across Linux distributions. However, building AppImage binaries for Linux is complicated, because of the inconsistent library versions present on each distribution. Briefcase uses Docker to provide a well-controlled binary environment for hosting AppImage builds.

Official installers for [Docker Engine](https://docs.docker.com/engine/install/#server/) are availble for a range of Unix distributions. Follow the instructions for your platform. Once you’ve installed Docker, you should be able to start an Ubuntu 20.04 container:

```text
$ docker run -it ubuntu:20.04
```

This should show you a Unix prompt (something like 
root@84444e31cff9:/#) inside your Docker container. Type 
```text
Ctrl-D
``` 
to exit Docker and return to your local shell.

###### Set up a virtual environment

We’re now going to create a virtual environment - a “sandbox” that we can use to isolate our work on this tutorial from our main Python installation. If we install packages into the virtual environment, our main Python installation (and any other Python projects on our computer) won’t be affected. If we make a complete mess of our virtual environment, we’ll be able to simply delete it and start again, without affecting any other Python project on our computer, and without the need to re-install Python.
```text
$ mkdir beeware
$ cd beeware
$ python3 -m venv beeware-venv
$ source beeware-venv/bin/activate
```
If this worked, your prompt should now be changed - it should have a (beeware-venv) prefix. This lets you know that you’re currently in your BeeWare virtual environment. Whenever you’re working on this tutorial, you should make sure your virtual environment is activated. If it isn’t, re-run the last command (the activate command) to re-activate your environment.

If using a different Os you can do the same using [provided guidlines](https://docs.beeware.org/en/latest/tutorial/tutorial-0.html)


## Getting the repo set/running
#### Install the Beeware tools
First, we need to install Briefcase. Briefcase is a BeeWare tool that can be used to package your application for distribution to end users - but it can also be used to bootstrap a new project.

```text
$ python3 -m pip install briefcase
```
For more OS, see [guidlines.](https://docs.beeware.org/en/latest/tutorial/tutorial-1.html) 

One of the BeeWare tools is Briefcase. Briefcase can be used to package your application for distribution to end users - but it can also be used to bootstrap a new project.

#### Clone the repo
Open a terminal, and type:
```text
$ git clone https://github.com/avosa/ChatMe.git
$ cd ChatMe
```

#### Running the App
```text
$ briefcase dev
```

#### Packaging for distribution
So far, we’ve been running our application in “Developer mode”. This makes it easy for us to run our application locally - but what we really want is to be able to give our application to others.

However, we don’t want to have to teach our users how to install Python, create a virtual environment, clone a git repository, and run Briefcase in developer mode. We’d rather just give them an installer, and have the application Just Work.

Briefcase can be used to package your application for distribution in this way.

#### Creating your application scaffold
Since this is the first time we’re packaging our application, we need to create some confguration files and other scaffolding to support the packaging process. From the "ChatMe" directory, run

```text
$ briefcase create
```

#### Building your application
You can now compile your application. This step performs any binary compilation that is necessary for your application to be executable on your target platform.

```text
$ briefcase build
```

#### Running your app
```text
$ briefcase run
```

This will start to run your native application, using the output of the build command.

You’ll notice that the console output we saw earlier won’t be visible anymore. This is because we are now running a standalone, packaged app that has no (visible) console to which it can output.

You might also notice some small differences in the way your application looks when it’s running. For example, icons and the name displayed by the operating system may be slightly different to those you saw when running under developer mode. This is also because you’re using the packaged application, not just running Python code. From the operating system’s perspective, you’re now running “an app”, not “a Python program”, and this is reflected in how the application appears.

#### Building your installer
You can now package your application for distribution, using the package command. The package command does any compilation that is required to convert the scaffolded project into a final, distributable product. Depending on the platform, this may involve compiling an installer, performing code signing, or doing other pre-distribution tasks.
```text
$ briefcase package
```

#### Taking it Mobile: Android
Now, we’re going to take our application, and deploy it as an Android application.

The process of deploying an application to Android is very similar to the process for deploying as a desktop application. Briefcase handles installing dependencies for Android, including the Android SDK, the Android emulator, and a Java compiler.

#### Create Android app and compile it
```text
$ briefcase create android
```
When you run 

```text
$ briefcase create android
```
for the first time, Briefcase downloads a Java JDK, and the Android SDK. File sizes and download times can be considerable; this may take a while (10 minutes or longer, depending on the speed of your Internet connection). When the download has completed, you will be prompted to accept Google’s Android SDK license.

Once this completes, we’ll now have an android directory in our project. This directory will contain a "ChatMe" folder, which will contain an Android project with a Gradle build configuration. This project will contain your application code, and a support package containing the Python interpreter.

We can then use Briefcase’s "build" command to compile this into an Android APK app file.
```text
$ briefcase build android
```
#### Running the app a virtual device
We’re now ready to "run" our application. You can use Briefcase’s run command to run the app on an Android device. Let’s start by running on an Android emulator.

To run your application, run: 
```text
$ briefcase run android
``` 
When you do this, you’ll be prompted with a list of devices that you could run the app on. The last item will always be an option to create a new Android emulator.
```text
$ briefcase run android
```
We can now choose our desired device. Select the “Create a new Android emulator” option, and accept the default choice for the device name (beePhone).

Briefcase "run" will automatically boot the virtual device. When the device is booting, you will see the Android logo

Once the device has finished booting, Briefcase will install your app on the device. You will briefly see a launcher screen

The app will then start. You’ll see a splash screen while the app starts up

The first time the app starts, it needs to unpack itself onto the device. This may take a few seconds. Once it’s unpacked, you’ll see the Android version of our desktop app

If you fail to see your app launching, you may need to check your terminal where you ran briefcase run and look for any error messages.

In future, if you want to run on this device without using the menu, you can provide the emulator’s name to Briefcase, using: 
```text
$ briefcase run android -d @beePhone 
```
to run on the virtual device directly.


More information can be found on [Beeware Online Tutorial](https://docs.beeware.org/en/latest/tutorial/tutorial-5/android.html)
