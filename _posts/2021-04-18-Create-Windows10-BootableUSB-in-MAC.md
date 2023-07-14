---
title: "Create a bootable USB for Windows 10/11 on MAC OS"
date: 2021-04-18 T19:34:30-04:00
categories:
  - blog
tags:
  - IT Helpdesk
  - Tutorials
---

You will need a Windows 10/11 ISO file and a USB drive with at least 8GB of free space.

1. Insert your USB drive & Open Terminal.

2. Use the following command to find out the disk number of your USB drive:

    diskutil list

This will display a list of drives, which will have details such as /dev/diskN (N being a number)

3. Unmount your USB drive by typing in the following command, remember to place N with the disk number of your USB drive:

    diskutil unmountDisk /dev/diskN

4. The following command will create the bootable Windows USB, replacing PATH/TO/WINDOWS.ISO with the path to your Windows 10 ISO file. If its in the downloads folder it should be something like /Users/USERNAME/Downloads/windowsfilename.iso (replace USERNAME with your MAC username & windowsfilename.iso with the downloaded ISO file name.)

    sudo dd if=PATH/TO/WINDOWS.ISO of=/dev/diskN bs=1m

5. Once the process is complete, eject the USB drive using the following command. Remember to replace diskN with your USB disk number you discovered earlier.

    diskutil eject /dev/diskN

You now have a bootable Windows USB drive.
