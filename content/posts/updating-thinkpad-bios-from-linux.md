+++
title = "Updating My ThinkPad BIOS from Linux"
date = "2021-09-03"
tags = ["thinkpad", "linux", "bios", "E14"]
description = "Today I updated my ThinkPad BIOS from Linux and here is a description of it."
+++

About a year ago, I got a ThinkPad E14 Gen 2 (Ryzen) and wanted to update its BIOS.

However, I didn't want to install Windows just to update the BIOS. After some research online, I discovered that Lenovo releases BIOS updates for ThinkPad in two formats - one is through the Bios Update Utility (Windows), which is a .exe file, and the other is a .iso file that can be flashed through a USB thumb drive.

Here's how to update the BIOS under Linux:

1. Get the latest version of the BIOS in .iso format for your model from the Lenovo support site.

2. Download `geteltorito`, a Perl script that extracts the boot image from the bios.iso file. You can grab it from [**here**](https://userpages.uni-koblenz.de/~krienke/ftp/noarch/geteltorito/geteltorito/geteltorito.pl).

3. Extract the boot image from the bios.iso file (in my case, the file was r1auj38wd.iso) using the command `$ geteltorito.pl -o bios_update.img r1auj38wd.iso`.

4. Copy the image to USB using the `dd` command: `$ sudo dd if=bios_update.img of=/dev/sda`. Note that you should replace `/dev/sda` with the corresponding device name for your system.

5. Boot from your USB drive, follow the instructions, and update the BIOS.

At first, I was nervous about what would happen if anything went wrong, but everything worked out just fine :)
