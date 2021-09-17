+++
title = "Updating My ThinkPad BIOS from Linux"
date = "2021-09-03"
tags = ["thinkpad", "linux", "update-bios", "E14"]
description = "Today I updated my ThinkPad BIOS from Linux and here is a description of it."
+++

I got my ThinkPad E14 Gen 2 (Ryzen) about a year ago, and since then there were many versions of BIOS released for this device, which have addressed various problems. I was planning to update my BIOS for a while, but I didn't want to install Windows just to install the BIOS. So I looked upon the Internet to see if I could update it without windows, and it turns out that it is possible to do so.

Lenovo releases BIOS for ThinkPad in two formats. One is through **Bios Update Utility (Windows)** which is a **.exe** file and the other is a **.iso** file, which can be flashed through a USB thumb drive. Here is how to do it under Linux in order to update the BIOS:

- Get the latest version of bios in .iso format for your model from the Lenovo support site.

- Next, we need `geteltorito`, It's a Perl script that extracts the boot image from the **bios.iso** file. Grab it from [**here**](https://userpages.uni-koblenz.de/~krienke/ftp/noarch/geteltorito/geteltorito/geteltorito.pl)

- Extract the boot image from the bios.iso file (r1auj38wd.iso in my case) `$ geteltorito.pl -o bios_update.img r1auj38wd.iso`

- Copy Image to USB using dd `$ sudo dd if=bios_update.img of=/dev/sda`

**Note**: replace `/dev/sda` with your corresponding device. Type very carefully this name or you may end up erasing one of your other disks.

- After that, simply boot from your USB drive, read the instructions and update the BIOS.

In the beginning, I was afraid of what I would do if anything went wrong. But it worked just fine :)
