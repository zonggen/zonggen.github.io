---
layout: post
title:  "Random Bits During Work"
categories: [notes, work]
date: 2019-06-13
draft: false
comment: true
---

Start looking into [issue#445](https://github.com/coreos/coreos-assembler/issues/445) on CoreOS Assembler:

 - xz format
    - [Downside](https://www.nongnu.org/lzip/xz_inadequate.html)
    - [bzip2 vs. xz vs. gzip2](https://unix.stackexchange.com/questions/108100/why-are-tar-archive-formats-switching-to-xz-compression-to-replace-bzip2-and-wha)
 - [lzma algo](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Markov_chain_algorithm)

Taking notes:
- gzip uses DEFLATE algorithm
- xz uses LZMA2
- Process of `cosa init && cosa build && cosa run`: 
    * download a `cosa` image that has all of the scripts installed
    * spin up a container using the image just downloaded
    * spin up a vm that built from the local fcos image that is built with `FCOS config`, inside the `cosa` container

Run:
- `podman images && podman rmi IMAGE_ID`

Related links:
- https://fedoraproject.org/wiki/Changes/Switch_RPMs_to_zstd_compression

