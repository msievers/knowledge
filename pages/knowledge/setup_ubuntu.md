---
title: Setup Ubuntu
keywords: ubuntu
permalink: setup_ubuntu.html
---

## VirtualBox

For the usage within VirtualBox, you should consider using a Ubuntu derivate which does ***not use Unity***, because features like *seemless windows* work better with simple window managers like LXDE. Therefor and because using LXDE reduces the resources needed to run Ubuntu with X11 inside VirtualBox, let's assume **Lubuntu** as the derivate of choice. Dispite the changed window manager, everything else should be the same.

Another option would be to use the *server* version of Ubuntu, but having X11 around is usefull in some cases, e.g. for running the Android SDK manager interactivly.

### Prerequisites

* VirtualBox >= 5.1

### Download the ISO image

Go to the [download page](https://help.ubuntu.com/community/Lubuntu/GetLubuntu) and download the latest version of **Lubuntu** for *amd64*.

* [lubuntu-16.04.1-desktop-amd64.iso](http://cdimage.ubuntu.com/lubuntu/releases/xenial/release/lubuntu-16.04.1-desktop-amd64.iso)

### Create a new virtual machine

Make sure you select type **Linux** and version **Ubuntu (64-bit)** and choose a reasonable amount of memory size. Select to create a (new) virtual hard disk now.
{% include image.html file="setup_ubuntu/setup_lubuntu_001.png" alt="Create virtual machine" caption="Create virtual machine" %}

Choose a reasonable size for virtual hard disk. When selectin **dynamically allocated** the hard disk image will grow dynamically to the size you specified. So don't be afraid to give your virtual hard disk a fair size, it will just occupy this space when you realy store that much.
{% include image.html file="setup_ubuntu/setup_lubuntu_002.png" alt="Create virtual hard disk" caption="Create virtual hard disk" %}

Per default, there is one network adapter activated and attached to **NAT**. This is perfect to be able to reach the outside from within your virtual machine.
{% include image.html file="setup_ubuntu/setup_lubuntu_004_001.png" alt="First network adapter" caption="First network adapter" %}

In order to access the virtual machine from the outside you should activate a second network adapter attached to **Host-only adapter** which connects the host and the virtual machine.
{% include image.html file="setup_ubuntu/setup_lubuntu_004_002.png" alt="Second network adapter" caption="Second network adapter" %}

Disable audio, because you ain't gonna need it and every device which has not to be emulated saves resources and headaches.
{% include image.html file="setup_ubuntu/setup_lubuntu_004.png" alt="Disable audio" caption="Disable audio" %}

Attach the *Lubuntu* iso image to the IDE controller.
{% include image.html file="setup_ubuntu/setup_lubuntu_007.png" alt="Attach iso image" caption="Attach iso image" %}

### Install Lubuntu

Start the virtual machine which should boot the attached iso image. Choose **Install Lubuntu** to run the installer instead of the live system, which would be started if *Try Lubuntu without installing* would have been selected.
{% include image.html file="setup_ubuntu/setup_lubuntu_011.png" alt="Choose 'Install Lubuntu'" caption="Choose 'Install Lubuntu'" %}

With *Lubuntu 16.04.1* there is a *glitch* with the installer that the window is to big to fit into the virtual screen. To be able to access the *Back* and *Continue* buttons, you have to move to window slightly to the left. 
{% include image.html file="setup_ubuntu/setup_lubuntu_018.png" alt="Move to window to access to button" caption="Move the window to access the button" %}

### Install guest additions

After installation succeeded, you should be able to boot to an LXDE based Xsession. Open a terminal by clicking

* Start -> System Tools -> LXTerminal

{% include image.html file="setup_ubuntu/setup_lubuntu_022_001.png" alt="Open a terminal" caption="Open a terminal" %}

Install the virtual box guest additions from the official ubuntu repositories.

```shell
sudo apt-get install -y virtualbox-guest-dkms
```

Reboot the virtual machine for changes to take effect.

```shell
sudo reboot
```

{% include links.html %}
