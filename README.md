### elementary OS Freya on a Mac (using rEFInd & EFI stub loading)

**NOTE**: I'm making a few assumptions about the way your computer is set up. Namely:

#### I assume your ESP partition is located at disk0s1
(If it's not, make sure you use the proper location. It should be though.)
![wheres-esp](img/wheres-esp.png)

#### I assume you don't have FileVault2/full disk encryption on
(Actually this *should* work with FDE on, but it's more complicated)
![no-fde](img/no-fde.png)

0. Back up all of your files.
0. No really, make sure you have a working backup. This procedure has been tested multiple times, but it's still possible things will go wrong and you could lose data. Time Machine is very good for this on the OS X side.
1. Download rEFInd (http://www.rodsbooks.com/refind/getting.html)
2. Install rEFInd to the ESP partition (`install.sh --esp`)
3. Mount your ESP partition (`mkdir /Volumes/ESP && sudo mount -t msdos /dev/disk0s1 /Volumes/ESP/`)
4. Rename the the refind directory (`mv /Volumes/ESP/EFI/refind /Volumes/ESP/EFI/BOOT`)
5. Rename the refind EFI blob (`mv /Volumes/ESP/EFI/BOOT/refind_x64.efi /Volumes/ESP/EFI/BOOT/bootx64.efi`)
6. Copy the `drivers_x64` folder (which can be found in the rEFInd tarball you downloaded) into the `BOOT` directory on your ESP. 
6. Fire up Disk Utility and make a new partition/replace your old Linux install partition with a new partition formatted as FAT. Name it something catchy, like "FREYA" (it'll be overwritten in step #11)
7. Plug your USB drive with elementary OS Freya (If you need to make one, [check this out](https://github.com/aroman/freya-on-a-mac/tree/master/iso-to-usb)) into your computer.
8. Pray
9. Reboot and choose the option that indicates that the OS lives on an external/USB disk.
10. Choose to "Try Elementary OS" and, when it boots, search for Terminal
11. Type `ubiquity -b` into the Terminal window - when the installer asks about partitioning, make sure you choose **Something Else...**.
12. Find the partiton you created in step #7 and format that as Ext4 and set its mount point to `/`. GRUB will not be installed, since you used the `-b` option for the installer. This setup is completely GRUB free, using rEFInd & EFI-stub loading (the new hotness).
13. Finish installing and restart.
14. Pray
15. Assuming all went well, you should see Ubuntu options in the rEFInd menu. Choose it.
16. Pray
17. You're now dual-booting Freya and OS X. Woot.
18. (optional) Make your rEFInd nicer. You can install a theme, get rid of the duplicate entries, etc. If you want to know how to do that stuff let me know and I'll document it. You can get your stuff looking this sexy:
