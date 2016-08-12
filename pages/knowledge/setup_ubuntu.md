---
title: Setup Ubuntu
keywords: ubuntu
permalink: setup_ubuntu.html
---

## VirtualBox

*Note*

For the usage within VirtualBox, you should consider using a Ubuntu derivate which does ***not use Unity***, because features like *seemless windows* work better with simple window managers like LXDE. Therefor and because using LXDE reduces the resources needed to run Ubuntu with X11 inside VirtualBox, let's assume **Lubuntu** as the derivate of choice. Dispite the changed window manager, everything else should be the same.

Another option would be to use the *server* version of Ubuntu, but having X11 around is usefull in some cases, e.g. for running the Android SDK manager interactivly.

### Prerequisites

* VirtualBox >= 5.1

### Download the ISO image

Go to the [download page](https://help.ubuntu.com/community/Lubuntu/GetLubuntu) and download the latest version of **Lubuntu** for *amd64*.

* [lubuntu-16.04.1-desktop-amd64.iso](http://cdimage.ubuntu.com/lubuntu/releases/xenial/release/lubuntu-16.04.1-desktop-amd64.iso)

### Create a new virtual machine

{% include image.html file="setup_ubuntu/setup_lubuntu_001.png" alt="Create virtual machine" caption="Create virtual machine" %}
{% include image.html file="setup_ubuntu/setup_lubuntu_002.png" alt="Create virtual hard disk" caption="Create virtual hard disk" %}
{% include image.html file="setup_ubuntu/setup_lubuntu_004.png" alt="Disable audio" caption="Disable audio" %}
{% include image.html file="setup_ubuntu/setup_lubuntu_007.png" alt="Attach iso image" caption="Attach iso image" %}

### Install Lubuntu

{% include image.html file="setup_ubuntu/setup_lubuntu_011.png" alt="Choose 'Install Lubuntu'" caption="Choose 'Install Lubuntu'" %}

***to be continued***

{% include links.html %}
