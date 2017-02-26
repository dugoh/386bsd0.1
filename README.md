# 386bsd0.1

A redo of http://gunkies.org/wiki/Installing_386BSD_on_BOCHS

That guide was made in 2010 for a manual install od 386BSD on Bochs on an AWS Fedora Core 8 box. This does a fully automated install on a Travis CI Ubuntu Trusty box. Due to time constraints within Travis it is not possible to redo the full guide in a single repository. This repository creates a disk image with 386BSD 0.1 installed and has the patch kits on the filesystem for later use.

Last build status:


[![Build Status](https://travis-ci.org/dugoh/386bsd0.1.svg?branch=master)](https://travis-ci.org/dugoh/386bsd0.1)


Artifacts are pushed to https://dugoh.github.io/386bsd0.1/


The disk is bzip2 compressed and then split into 50MB parts. I did not look into "Releases" or "Git Large File Storage" and how to plug that into Travis yet. Grabbing the disk is simple enough though.

```
for i in a b c ; do wget -O - https://dugoh.github.io/386bsd0.1/disk.part-a${i} ; done|bunzip2 >disk.img
```
