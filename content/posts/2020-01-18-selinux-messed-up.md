---
layout: post
title:  "Messed up my laptop by trying to run Podman inside Podman"
categories: [selinux, podman]
featured-img: work-update-2
date: 2020-01-18
draft: false
comment: true
---

So I tried to run a container inside a container with podman, which involves
running `podman-compose` inside a wrapper conainer (`fedora:latest`). I've always got this
error message: 
```
ERRO[0000] 'overlay' is not supported over overlayfs
Error: could not get runtime: 'overlay' is not supported over overlayfs: backing file system is unsupported for this graph driver
```

So I ran `sudo podman --privileged -v /var/lib/containers:/var/lib/containers -v /var/run:/var/run ...`,
which is my last hope after trying so many methods. Of course passing container storages and
the whole runtime into the container basically invalidates the meaning of a virtualized container environment.

The second day when I was trying to bootup the machine (my work laptop), everything seemed to be failing (literally...), e.g. NetworkManager, Graphic Driver, and even the _emergency console_ had
problem to start.

After almost one hour of investigation and retrying to boot again and again, I almost felt that reinstalling the system is the only option. 
Luckily, one of my experienced co-worker Jonathan hinted that the inner container might messed up the host by alering the SELinux labelling of the directory
`/var/run`, which means that the host won't have access to all of the sockets and run-time variables.

__Solution__: Edit GRUB entries by pressing `e` during GRUB menu in bootup. Then append `enforcing=0` to the end. Press `ctl-x` to start. After booted, reset the SELinux labels with `restorecon -vR /var/run && restorecon -vR /var/lib/containers`. You might also need to set SELinux to permissive mode and reboot, then switch back to enforcing mode to avoid edit GRUB entries everytime during bootup process.

To view the SELinux labels, use `ll -Z /var/run`, and `matchpathcon -V /var/run` to see the current and default SELinux context.

References:
 - https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide/sect-security-enhanced_linux-working_with_selinux-selinux_contexts_labeling_files
 - https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security-enhanced_linux/sect-security-enhanced_linux-maintaining_selinux_labels_-checking_the_default_selinux_context
 - https://wiki.gentoo.org/wiki/SELinux/Tutorials/Permissive_versus_enforcing
 - https://docs.fedoraproject.org/en-US/quick-docs/changing-selinux-states-and-modes/