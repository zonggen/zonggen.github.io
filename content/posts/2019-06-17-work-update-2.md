---
layout: post
title:  "Working with CoreOS Assembler Scripts"
categories: [ blog, work]
date: 2019-06-17
draft: false
comment: true
---

### Working with CoreOS Assembler Scripts

```text
$ export COREOS_ASSEMBLER_PRIVILEGED=true
$ cosa init https://github.com/coreos/fedora-coreos-config
$ cosa fetch && cosa build
```

To eliminate the error message:

`[dumb-init] /usr/bin/coreos-assembler: Permission denied`

Run following commands:

```text
$ setfacl -R -m u:1000:rwx /path/to/github.com/coreos/coreos-assembler/
$ setfacl -R -d -m u:1000:rwx /path/to/github.com/coreos/coreos-assembler/
$ chcon -R system_u:object_r:container_file_t:s0 /path/to/github.com/coreos/coreos-assembler/
```
