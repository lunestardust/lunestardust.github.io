---
layout: post
title: RP-DEV-NOTE FPGA development environment for Red Pitaya on Windows 10
date: 2018-09-39 10:57:24.000000000 +08:00
---

The post demonstrates how to set up a FPGA development environment 
for Red Pitaya STEMlab board by installing 
Xilinx Vivado on Windows Subsystem for Linux (WSL).
The method avoids the issues of virtual machine or dual boot option
for Windows 10 users.
The method may be valid on Windows Server 2019,
but I did not test it.

### Install WSL on Window 10

Refer to [Windows Subsystem for Linux on Wikipedia](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
to learn more about WSL.

To install WSL on Windows 10,
you may read the [instructions by Microsoft](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

Please choose the **Ubuntu 18.04 LTS** subsystem.

### Establish desktop environment

The Red Pitaya STEMlab board is based on Xilinx Zynq SoC
and thus,
We need install Xilinx Vivado for further FPGA development.
However,
Vivado runs on desktop environment,
which is not supported on naive WSL.

The solution to the problem can be found in
[this article](https://www.zdnet.com/article/how-to-run-run-the-native-ubuntu-desktop-on-windows-10/).
We can run a X Serve on Windows to host the GUI program on WSL.
Please read it but wait a moment before your implementation,
because I'd like to provide some suggestions.

#### Fist

In my opinion, [Xming](https://sourceforge.net/projects/xming/)
works better than [VcXsrv](https://sourceforge.net/projects/vcxsrv/),
though Xming hasn't been updated for a long time.

#### Second

There is a small mistake in the post.
>After installing X Server on Windows, one should make D-Bus use tcp in place of sockets,using the following command 
> `sudo sed -i 's/<listen>.*<\/listen>/<listen>tcp:host=localhost,port=0<\/listen>/' /etc/dbus-1/session.conf`

However,
`session.conf` does not in the folder `/etc/dbus-1/`.
One WSL,
the file is located in `/etc/dbus-1/`.

### Third

You can find WSL in
`C:\Users\USER_NAME\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs`
but **DO NOT** edit the files of WSL directly by the editors in Windows.
You may change the access permission of the file when saving new contents in it.
If you prefer GUI editors, just install one of them on WSL, e.g. Geany:
`sudo apt-get install geany`.

Similarly,
copy or move files to the folder of WSL on Windows may also lead to problems.
The drivers of Windows are mounted in the folder 
`\mnt` on WSL.
Therefore,
use `cp` or `mv` to copy or move files.

#### Fourth

You could change the sources of Ubuntu
by editing the file `/etc/apt/sources.list`.
[Here is the official archive list for Ubuntu](https://launchpad.net/ubuntu/+archivemirrors).

It is highly recommended to choose a local source mirror
before the following command is executed
`sudo apt-get install ubuntu-desktop`.
Or it may take a long time to install *ubuntu-desktop*.

By the way,
*Uinty* and *compizconfig-settings-manager*
are unnecessary for running Vivado
so you may not install them.


### Install Vivado

[Start programming FPGA using Red Pitaya board](https://red-pitaya-fpga-examples.readthedocs.io/en/latest/_downloads/StartprogrammingFPGAusingRedPitayaboard.pdf)
is an official article which details the steps of installing Vivado on Ubuntu.
However, unlike described in it,
we need Vivado 2017.2 edition to support the FPGA programs running on Red Pitaya OS 0.97.

Enjoy!