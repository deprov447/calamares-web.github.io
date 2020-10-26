---
published: true
layout: post
title: "Important e2fsprogs issue discovered"
---
A critical issue involving Calamares and e2fsprogs has been brought to our attention.

Some of our downstream distributors deploy Calamares 1.1.2 with **e2fsprogs 1.42.12** or earlier. The 1.1 series of Calamares internally uses a submodule based on KDE Partition Manager, and this submodule in turn queries certain programs in the e2fsprogs package to support filesystem management operations with ext2, ext3 and ext4. 

Unfortunately, `dumpe2fs` from e2fsprogs 1.42.12 can segfault when called with no arguments. This is not expected behavior, and it causes the Calamares partition management component to report filesystem resize operations as unsupported. Because of this, Calamares disables Alongside install support.

The bug has already been reported upstream, and a fix is available.

**The solution is to package and deploy e2fsprogs 1.42.13 or later.**

Distributions known to be affected include Arch Linux derivatives as of today (2015-09-08, the core repository reports e2fsprogs 1.42.12-2) and likely many others.

The Calamares team wishes to remind you that if you experience any issue with Calamares, you are welcome to tell us all about it on the [**Calamares issue tracker**](https://calamares.io/bugs/).

<!--more-->
