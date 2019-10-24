---
layout: post
title:  "Creating a Daemon process with Systemd"
categories: [ blog, work]
featured-img: work-update-2
---

Just want to make a note on how to create a daemon process with systemd
service file. When I'm working on Fedora CoreOS Pinger client side, the following systemd service file will hang at the boot process and eventually
timeout afer 1m34s.

```
[Unit]
Description=Telemetry service for Fedora CoreOS
Documentation=https://github.com/coreos/fedora-coreos-pinger
Before=systemd-user-sessions.service
Wants=network-online.target
After=network-online.target

[Service]
DynamicUser=yes
Type=forking
StateDirectory=fedora-coreos-pinger
ExecStart=/usr/libexec/fedora-coreos-pinger

[Install]
WantedBy=multi-user.target

```

The reason behind this is that systemd expects the process called by `ExecStart=` to call `fork()` and terminate the parent process so that
the child processs could be orphaned and finally become a Daemon process that
running in the background.

So to solve this issue, we need to call `fork()` inside fcos pinger main
loop and terminate the parent process and then continue running main logic
in the child process.

Reference:
 - https://unix.stackexchange.com/a/125723
