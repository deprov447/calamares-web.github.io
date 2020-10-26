---
published: true
layout: post
title: "Calamares progress on Google Summer of Code 2018"
---
As explained before by Adriaan de Groot 
in this [post](https://euroquis.nl/bobulate/?p=1860) on his blog,
Calamares have participated in the Google Summer of Code 2018.

Caio Jordão Carvalho worked on finishing LVM support
on Calamares, which include the following updates:
 * Fixed some important LVM bugs, such as crash in
   revert operation when you got a previously created Volume Group.
 * Create new LVM Volume Groups.
 * Resize LVM Volume Groups.
 * Deactivate LVM Volume Groups.
 * Remove LVM Volume Groups.

This [patch](https://github.com/calamares/calamares/commit/3b82e655d720179fe62901a620eb0796f50ef1d5) 
presents the code, 
which was merged to Calamares' master branch. 
Further descriptions about Caio's implementations can be 
seen in his [blog](https://carvalho.site/category/gsoc).

Another update that is part of this GSoC project and will be included to Calamares is RAID support. 
This support involves the visualization of software RAID (i.e. mdraid) arrays 
and manipulation of the partitions from these devices. 
Caio already have commited patches related to it in kpmcore library, 
as you can see [here](https://cgit.kde.org/kpmcore.git/?h=raid-support), and have 
implemented updates on KDE Partition Manager's GUI to allow these operations.

Actually the code in kpmcore is being improved to provide more stability and these functionalities 
will be available soon for Calamares.
