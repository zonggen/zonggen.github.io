---
layout: post
title:  "[TLDR] GRUB, dracut, systemd and Bootup Process"
categories: [linux]
date: 2019-06-27
draft: false
comment: true
---

 1. **BIOS POST**: issues interrupt INT13H to find boot sectors on bootable device
 2. **Boot Loaders** (LILO / GRUB / GRUB2): loads Linux Kernel into memory and running
    * **stage1**: runs bootstrap code that loaded by BIOS POST in Master Boot Record (MBR)
        * stage1 does not understand file system, the only purpose of stage1 is to locate and load stage1.5
    * **stage2**: locates the stage 2 files in the /boot filesystem and load the needed drivers.
        * understands common filesystem drivers, e.g. EXT, FAT, NTFS, etc.
        * stored in core.img
    * **stage3**: locates and loads a Linux kernel into RAM and turns control over to the kernel
        * located in `/boot/grub2`
        * runtime kernel modules located in `/boot/grub2/i386-pc`
 3. **Kernel**: located in `/boot` along with initramfs image and device maps of the hard drives
    * de-compressed in memory
    * executes initrd, an initial RAM disk image generated by [**dracut**](https://dracut.wiki.kernel.org/index.php/Main_Page)
        * _note_: The initramfs has (basically) one purpose in life -- getting the rootfs mounted so that we can transition to the real rootfs.
    * [**systemd**](http://man7.org/linux/man-pages/man1/systemd.1.html): PID=1, init process, [daemon](https://en.wikipedia.org/wiki/Daemon_(computing))
        * responsible for probing all remaining hardware, mounting all necessary file systems and spawning all configured services.


References:

 - http://man7.org/linux/man-pages/man7/boot.7.html
 - http://man7.org/linux/man-pages/man7/bootup.7.html
 - http://man7.org/linux/man-pages/man7/systemd.special.7.html
 - http://man7.org/linux/man-pages/man7/dracut.bootup.7.html
 - https://opensource.com/article/17/2/linux-boot-and-startup
 - https://wiki.gentoo.org/wiki/Initramfs/Guide
 - https://unix.stackexchange.com/questions/364418/when-the-os-is-loaded-does-the-kernel-continue-to-run-as-a-normal-program