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

### Setup networking

During the creation of the virtual machine, you activated two network interfaces

1. *NAT* interface
2. *Host-only* interface

The *NAT* interface was used during the installation to fetch packages from the internet. To be able to access your virtual machine from the host it runs on, the *Host-only* adapter is used. It spans a network with the host, but has no connection to the outside.

Normally, this interfaces gets an IP address assigned by a VirtualBox DHCP server which can be configured for this network by clicking

* File -> Preferences
  * Network -> Host-only Networks

{% include image.html file="setup_ubuntu/setup_lubuntu_031.png" alt="VirtualBox network settings" caption="VirtualBox network settings" %}

The problem with DHCP is, that the virtual machine may get different IP addresses, depending on various circumstances. To avoid this and in order to have **this** virtual machine always be reachable under the **same** IP address, you have to configure the *Host-only* interface to have a static address.

#### Know your interfaces

Open a terminal (Start -> System Tools -> LXTerminal) and list the network devices.

```shell
ifconfig
```

This should print out something like the following. Note the `HWaddr` of the interface with the IP address from the `192.168.56.x` net, because this is the *Host-only* interface, whereas the `10.0.2.x` interface is the *NAT* interface. In this example the `HWaddr` of the *Host-only* adapter is `08:00:27:e0:8d:d0`.

```shell
enp0s3    Link encap:Ethernet  HWaddr 08:00:27:e1:d9:cb  
          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
          inet6 addr: fe80::6219:e247:e65f:899b/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25 errors:0 dropped:0 overruns:0 frame:0
          TX packets:40 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:7188 (7.1 KB)  TX bytes:3827 (3.8 KB)

enp0s8    Link encap:Ethernet  HWaddr 08:00:27:e0:8d:d0  
          inet addr:192.168.56.101  Bcast:192.168.56.255  Mask:255.255.255.0
          inet6 addr: fe80::6edb:b05f:215d:2599/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
          TX packets:10 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:1180 (1.1 KB)  TX bytes:1308 (1.3 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:52 errors:0 dropped:0 overruns:0 frame:0
          TX packets:52 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:7424 (7.4 KB)  TX bytes:7424 (7.4 KB)

```

#### Setup a static IP address

Open **Network Connections**

{% include image.html file="setup_ubuntu/setup_lubuntu_032.png" alt="Network Connections" caption="Network Connections" %}

The reason for noting the hardware address of the *Host-only* interface in the first place was, that now there show up two interfaces, which are labeled

* Wired Connection 1
* Wired Connection 2

To assign a static IP address to the right interface (*Host-only* interface), one has to compare the hardware address.

{% include image.html file="setup_ubuntu/setup_lubuntu_033.png" alt="Network Connections" caption="Network Connections" %}

For this example, it's `Wired Connection 1` which corresponds to the *Host-only* interface.

{% include image.html file="setup_ubuntu/setup_lubuntu_034.png" alt="Editing Connection" caption="Edition Connection" %}

Please consider the following constraints before choosing an IP address.

* the IP address has to be inside the adapters network, for this example inside `192.168.56.x`
* the IP address cannot be the `.1` address, because this is (normally) already assigned to the host
* if the DHCP server for this network is enabled, the address should not be within the DHCP assigned range

Now click the `IPv4` tab. Change the method from `DHCP` to `Manual` and click `Add` next to the addresses table.

* IP address `192.168.56.2`
* netmask `24`
* leave the `gateway` blank
  * do **not** set this to the host IP address

You are free to rename this connection to something more descriptive by chaning the connection name.

* `Wired Connection 1` -> `Host-only connection`

Click `Save` to persist your changes.

{% include image.html file="setup_ubuntu/setup_lubuntu_035.png" alt="Editing Connection" caption="Edition Connection" %}

Reboot the virtual machine for changes to take effect. After the machine has rebooted open a terminal and run

```shell
ifconfig
```

The interface with the hardware address `08:00:27:e0:8d:d0` should now have the IP address `192.168.56.2`.

```shell
enp0s3    Link encap:Ethernet  HWaddr 08:00:27:e1:d9:cb  
          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
          inet6 addr: fe80::cd05:7301:3c51:520a/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25 errors:0 dropped:0 overruns:0 frame:0
          TX packets:41 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:7172 (7.1 KB)  TX bytes:3992 (3.9 KB)

enp0s8    Link encap:Ethernet  HWaddr 08:00:27:e0:8d:d0  
          inet addr:192.168.56.2  Bcast:192.168.56.255  Mask:255.255.255.0
          inet6 addr: fe80::6edb:b05f:215d:2599/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:624 (624.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:52 errors:0 dropped:0 overruns:0 frame:0
          TX packets:52 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:7408 (7.4 KB)  TX bytes:7408 (7.4 KB)
```

### Setup OpenSSH server

Open a terminal.

{% include image.html file="setup_ubuntu/setup_lubuntu_022_001.png" alt="Open a terminal" caption="Open a terminal" %}

Run the following command to install the `OpenSSH server`.

```shell
sudo apt-get install -y openssh-server
```

### Update software packages

Log into your virtual machine by SSH or open a termin and issue the following commands

```shell
sudo apt-get update
sudo apt-get -y upgrade
```

If in doubt, reboot your virtual machines for changes to take effect.

```shell
sudo reboot
```

{% include links.html %}
