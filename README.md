# 386bsd0.1

An automated redo of http://gunkies.org/wiki/Installing_386BSD_on_BOCHS

The guide was made in 2010 for a manual install of 386BSD on Bochs on an AWS Fedora Core 8 box. This repo does a fully automated install using a Travis CI Ubuntu Trusty box. Due to time constraints within Travis it is not possible to redo the full guide in a single repository. This repository creates a Bochs disk image with 386BSD 0.1 installed and has the patch kits on the filesystem for later use. At least some patching and kernel recompilation is required. You can pick up the guide at "Fourth boot, multiuser mode".


All artifacts are pushed to https://dugoh.github.io/386bsd0.1/. The disk is bzip2 compressed and then split into 50MB parts. Grabbing the disk is simple enough though.

```
for i in a b c ; do wget -O - https://dugoh.github.io/386bsd0.1/disk.part-a${i} ; done|bunzip2 >disk.img
```

Once you have bochsrc, boot.img, disk.img, tunconfig present and Boch installed you should be able to get it to boot.

If you want networking, check tunconfig and setcap CAP_NET_ADMIN,CAP_NET_RAW=eip your bochs binary, alternatively configure slirp.

The inittodr function used in usr/src/sys.386bsd/i386/isa/clock.c suffers from a Y2K bug. Setting the time to the current date results in timestamps set to to 1970. If you want sensible timestamps you can set time0 in bochsrc until you patched.

Reasonable values are:

 - 711244800 - release date
 - 735327993 - first patch kit
 - 740756888 - second patch kit

In this build a pristine 386bsd 0.1 as released is installed and the 2 patch kits are placed on the filesystem for convenience, hence the choice for something slightly over 740756888. This is done so the arrow of time doesn't look broken when looking at the timestamps on the filesystem.


Last build status:

[![Build Status](https://travis-ci.org/dugoh/386bsd0.1.svg?branch=master)](https://travis-ci.org/dugoh/386bsd0.1)
