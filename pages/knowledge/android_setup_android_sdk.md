---
title: Setup Android SDK
keywords: android
last_updated: July 3, 2016
sidebar: knowledge_sidebar
permalink: setup_android_sdk.html
folder: knowledge
---

## Mac

## Ubuntu LTS

### Download the SDK

```shell
sudo apt-get install -y curl
mkdir -p ~/Downloads && cd ~/Downloads
curl -O https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
```

### Extract the SDK

You can extract the SDK to any location you like. For this guide, it will be extracted into the users home directory.

```shell
# this will create ~/android-sdk-linux
tar -xzf android-sdk_r24.4.1-linux.tgz -C ~/
```

### Add the android tools to your path

There are different files which will be evaluated depending on the shell being started interactivly or as a login shell. On Ubuntu, because `.bashrc` is included by `.bash_profile`, it is sufficient, to add the path to your `.bashrc` by appending the following lines.

```shell
export ANDROID_HOME="$HOME/android-sdk-linux"
export PATH="$PATH:$ANDROID_HOME/tools"
```

*You should restart your terminal for the changes to take effect.*

### Install/Update SDK components

There are two ways to run the Android SDK package manager.

* interactivly (needs X to be running)
* headless

#### Interactivly

If you have X up and running, you can run the Android SDK manager simply by executing `android`, which should bring up the UI. There you can select packages to be installed.

{% include image.html file="setup_android_sdk/sdk_manager.png" alt="Android SDK manager" caption="Android SDK manager" %}

#### Headless

You can get a list of all packages available by issuing

```shell
android list sdk --all --extended
```

Let's assume you want to install the packages needed to develop for Android API Level `22`/`5.1.1`.

The following packages are needed for every API Level

* `tools`, `platform-tools`, `build-tools-24.0.1` (*check the last one for version changes*)

The following packages are needed for API Level `22`

* `android-22`, `addon-google_apis-google-22`

The following packages should be installed optionally

* `extra-android-m2repository`, `extra-google-google_play_services`, `extra-google-webdriver`

The command to install the mentioned packages is

```shell
android update sdk --filter tools,platform-tools,build-tools-24.0.1,android-22,addon-google_apis-google-22,extra-android-m2repository,extra-google-google_play_services,extra-google-webdriver
```

*You will be prompted to accept the license. Type `y` or `yes` to proceed.*

### Add the platform tools to your path

Assuming that you have set the `ANDROID_HOME` variable as described above, simply append the following to your `.bashrc`.

```shell
export PATH="$PATH:$ANDROID_HONE/platform-tools"
```

# Links
* http://stackoverflow.com/questions/17963508/how-to-install-android-sdk-build-tools-on-the-command-line

{% include links.html %}
