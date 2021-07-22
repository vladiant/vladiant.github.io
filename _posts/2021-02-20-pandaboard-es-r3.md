---
layout: post
title: "Pandaboard-ES Rev B3 Developer’s Guide"
date: 2021-02-20
tags: pandaboard
---

## Intro
Posted on October 4, 2013 by svtronics in Blog, Pandaboard-ES B3.

[http://www.svtronics.com/support/pandaboard-es-b3-developers-guide/](http://www.svtronics.com/support/pandaboard-es-b3-developers-guide/) - Not active anymore

## Download path for pre-build binaries

[SVT](https://www.dropbox.com/sh/nehzvckcbkdhui6/n3G5wbi-47)

### Ubuntu package directory (boot loader, kernel and file-system)
SVT/PandaboardES_B3_Packages/ubuntu-package/

### Android package directory (boot loader, kernel and file-system)
SVT/PandaboardES_B3_Packages/android-package/

### mkcard.sh (utility to create partitions in SD card for Ubuntu file-system)
SVT/PandaboardES_B3_Packages/

## Steps to prepare SD card for booting Ubuntu
1) Download mkcard.sh (utility to create partitions in SD card for Ubuntu file-
system) and 11.10Ubuntu.tar.gz (Ubuntu pre-built file-system, boot loader and
kernel package) files
2) Connect SD card to the Linux PC
3) Find the partition on which SD card is mounted on the Linux PC
> $ dmesg

Look for a line that looks like the following **at the end of the log**

> [288582.790722] sdc: sdc1 sdc2 sdc3 sdc4 < sdc5 sdc6 >

4) Run mkcard.sh script to create partitions in SD card for Ubuntu
WARNING In the next step, make sure you use /dev/“whatever you see above”.
You can erase your hard drive with the wrong parameter.

> $ chmod +x ./mkcard.sh

> $ sudo ./mkcard.sh <sd card partition>

This will ask for two options:

* To format the boot and rootfs only, enter ‘f’.
* To create the boot, media and rootfs and format them, enter ‘c’.

Enter option ‘f’ here to format boot and rootfs partitions.
Wait until this utility creates two partitions in your SD card.

5) Extract 11.10Ubuntu.tar.gz file. This tar-ball contains directory 11.10 which
contains rootfs and boot directories

> $ tar -xvzf 11.10-Ubuntu.tar.gz

6) Copy contents of the boot directory of extracted image to boot directory of SD
card.

To check mount point of SD card,

> $ mount

Here, the mount point can be seen with its device file entry of SD card partitions
(e.g. /dev/sdc1 on /media/boot, here ‘/media’ is the mount point)

> $ cp 11.10/boot/* <mount point of sd card>/boot/.

7) Extract ubuntu-core-11.10-core-armel.tar.gz file of the rootfs directory in rootfs
partition of SD card with ‘sudo’ permission.

> $ sudo tar -xvzf 11.10/rootfs/ubuntu-core-11.10-core-armel.tar.gz -C <mount
point of sd card>/rootfs/.

8) Unmount SD card from your Linux pc.

> $ unmount <mount point of sd card>/rootfs <mount point of sd card>/boot

9) Configure serial console with baud rate as 115200
10) Connect SD card to pandaboard rev b3 and power up the board
11) The boot prints should be seen on the serial console
12) Use the user name as ‘root’ to login to the file-system

## Steps to prepare SD card for booting Linaro Android
### Get linaro image tools
1) Run these commands to get all the dependencies for linaro-image-tools
and the tip of linaro-image-tools

> $ sudo add-apt-repository ppa:linaro-maintainers/tools

> $ sudo apt-get update

> $ sudo apt-get install linaro-image-tools

### Create media (SD card)
1) Download android-filesystem.tar.gz and extract this tar-ball
2) Install dconf and dconf-config packages in Linux pc

> $ sudo apt-get install dconf dconf-config (for Ubuntu host OS)

3) Disable automount (instructions provided for Gnome)

>$ TMP1=$(dconf read /org/gnome/desktop/media-handling/automount)

> $ TMP2=$(dconf read /org/gnome/desktop/media-handling/automount-
open)

> $ dconf write /org/gnome/desktop/media-handling/automount false

> $ dconf write /org/gnome/desktop/media-handling/automount-open false

4) Insert an SD card to the Linux pc
5) Find the partition on which SD card is mounted on the linux PC

> $ dmesg

Look for a line that looks like the following at the end of the log

> [288582.790722] sdc: sdc1 sdc2 sdc3 sdc4 < sdc5 sdc6 >

6) Run linaro image tools

**WARNING** In the next step, make sure you use /dev/“whatever you see
above”. You can erase your hard drive with the wrong parameter.

> $ sudo linaro-android-media-create –mmc /dev/**<sd card partition>** –dev
panda –boot boot.tar.bz2
–system system.tar.bz2
–userdata
userdata.tar.bz2

7) Restore automount

> $ dconf write /org/gnome/desktop/media-handling/automount $TMP1

> $ dconf write /org/gnome/desktop/media-handling/automount-open $TMP2

8) Configure serial console with baud rate as 115200
9) Connect SD card to pandaboard rev b3 and power up the board
10) The boot prints should be seen on the serial console

## PandaboardES B3 Source GIT

1) Source Code for u-boot (for ubuntu and android file-system)

[http://github.com/svtronics/u-boot-pandaboard-ES-RevB3](http://github.com/svtronics/u-boot-pandaboard-ES-RevB3)

2) Source Code for Kernel (for Ubuntu file-system)

[http://github.com/svtronics/kernel-pandaboard-ES-RevB3](http://github.com/svtronics/kernel-pandaboard-ES-RevB3)

## Steps to compile u-boot (Can be used with Ubuntu and Linaro Android)
1) Checkout u-boot source for Panadaboard ES RevB3 from GIT

> $ git clone git://github.com/svtronics/u-boot-pandaboard-ES-RevB3.git

2) Compile u-boot source

> $ cd u-boot-pandaboard-ES-RevB3/

> $ make CROSS_COMPILE=arm-linux-gnueabi- omap4_panda

3) You should get u-boot image(u-boot.img, u-boot.bin & MLO) at u-boot-linaro-
stable directory.
4) For booting Ubuntu replace binary (u-boot.bin & MLO) in SD card under “boot”
partition.

> $ cp MLO u-boot.bin <mount point of sd card>/boot

5) For booting Android replace the binaries (u-boot.img, u-boot.bin & MLO) in SD
card under “boot” partition.

> $ cp MLO u-boot.bin u-boot.img <mount point of sd card>/boot

## Steps to compile Ubuntu Kernel
1) Checkout Ubuntu kernel source for Panadaboard ES from GIT

> $ git clone git://github.com/svtronics/kernel-pandaboard-ES-RevB3.git

2) Compile kernel source and kernel modules

> $ cd kernel-pandaboard-ES-RevB3/

> $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
omap4plus_defconfig

> $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- uImage

> $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- uImage modules

3) You should get kernel image at arch/arm/boot/ path. Replace it in SD card under
“boot” partition and boot Ubuntu. Also install kernel modules in rootfs partition of
SD card.

> $ cp arch/arm/boot/uImage <mount point of sd card>/boot

> $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- modules_install
INSTALL_MOD_PATH=<mount point of sd card>/rootfs/

## References

1) Inactive: [http://www.svtronics.com/support/pandaboard-es-b3-developers-guide/](http://www.svtronics.com/support/pandaboard-es-b3-developers-guide/)

2) Inactive: [http://www.svtronics.com/support/support/blog/](http://www.svtronics.com/support/support/blog/)

3) Inactive: [https://hackpad.com/Setup-Ubuntu-14.04.1-for-Pandaboard-ES-Rev.-B3-in-Ubuntu-14.10-zSnXFECi2kc](https://hackpad.com/Setup-Ubuntu-14.04.1-for-Pandaboard-ES-Rev.-B3-in-Ubuntu-14.10-zSnXFECi2kc)

4) [Pandaboard bootup issue](http://stackoverflow.com/questions/19292993/pandaboard-bootup-issue)

5) [RISC OS Open Forums/Code review/OMAP4](https://www.riscosopen.org/forum/forums/3/topics/2459)

6) Inactive: [http://wiki.hbrobotics.org/index.php?title=Installing_Ubuntu_With_Real_Time_Patches_On_The_PandaBoard](http://wiki.hbrobotics.org/index.php?title=Installing_Ubuntu_With_Real_Time_Patches_On_The_PandaBoard)

