# Basic Installation

The following describes a fair bit of the process that was followed to
get a Linux Mint system installed, starting from a system that was
running Void.

## Partition Preparations and Backups

* On existing SSD with Void, make a partition that has enough space to
  hold user directories, say stuff under `/home`.  This was doable in
  my case due to the way I tend to not fill up storage devices.
  
* Copy home directories to new partition.
  
* Optionally backup entire ssd somewhere (initially did this to figure
  out subsequent steps, but came back to work on the original SSD once
  I was comfortable that things would work).

* Remove EFS and Void partitions (can do this a bit later too)

## Intallation Media Preparation

* Prepare / get Ventoy boot USB media.

* Get and verify `.iso` for Linux Mint (22.1 and 22.2 both worked) and
  put on Ventoy USB.

## Installation

* Boot machine from Ventoy USB, choosing one of the Mint isos, and
  follow the directions until ending up at a desktop.

* Start the installer via the icon on the desktop.

* Follow the appropriate steps until reaching the partitioning step.

* Choose the last option -- "something else" -- then make efs and
  ext4fs partitions.  I gave EFS 1024 MB and the rest to the ext4fs.
  choose `/` as the mount point for the ext4fs partition.  There
  should be some button to press that indicates continuing the
  installation...press it.

* Continue until installation has finished.  Some of the steps took
  quite long...perhaps there was a fair bit of network congestion or
  retrying?  Who knows...

