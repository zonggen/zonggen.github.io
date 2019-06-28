---
layout: post
title:  "Work Update #2"
categories: [ blog, work]
featured-img: work-update-2
---

### Hacking on CoreOS Assembler Scripts
```
$ export COREOS_ASSEMBLER_PRIVILEGED=true
$ cosa init https://github.com/coreos/fedora-coreos-config
$ cosa fetch && cosa build
```
To eliminate the error message:

`[dumb-init] /usr/bin/coreos-assembler: Permission denied`

Run following commands:

```shell
$ setfacl -R -m u:1000:rwx /path/to/github.com/coreos/coreos-assembler/
$ setfacl -R -d -m u:1000:rwx /path/to/github.com/coreos/coreos-assembler/
$ chcon -R system_u:object_r:container_file_t:s0 /path/to/github.com/coreos/coreos-assembler/
```
