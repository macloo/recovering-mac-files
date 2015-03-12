# recovering-mac-files
Dead MacBook, no reboot, disk can't be repaired. Forgot to back up. What to do? This. 

## Steps to Recover Your Files

**OS X Yosemite:** Start up in single-user mode. How: 

Press Command (⌘)-S as your Mac starts up.

Source: https://support.apple.com/kb/PH18782?locale=en_US&viewlocale=en_US

**NOTE: This is not for people who never use the command line! You will be at the root of your system. There will be nothing but typing!**

Give yourself the power to write:

`/sbin/mount -uw /`

(The `-u` flag indicates that the status of an already mounted file system should be changed, and the `-w` flag tells the system to mount the file system in read-write mode.)

Create a mount point for the USB drive:

`mkdir /Volumes/usbdrive`

See what names all current drives (and partitions) have:

`ls /dev/disk*`

Insert USB.
See what new name the system has added, meaning the USB drive 
(for example, `/dev/disk2s1`):

`ls /dev/disk*`

Mount the USB drive:

`/sbin/mount_hfs /dev/disk2s1 /Volumes/usbdrive`

### Side note

Oh, wait: Your USB drive might NOT be "hfs." Find out using this guide: 

http://www.tuaw.com/2011/09/19/mac-101-format-choices-for-usb-flash-drives/

(There are lots of commands for "mount" -- this will show them to you: 

`ls /sbin/ | grep mount_`

NOTE: It is okay to mount it to `/Volumes/usbdrive` again and again. 
For example, if you are taking out the USB and then reinserting it. 
See below for how to safely un-mount the USB device.)

### End side note

Now you are ready to copy. The pattern is:

`cp -R /name/of/all/directories/on/source/drive/ /Volumes/usbdrive/newDirectory/`

**Example:**

`cp -R /Users/MarySmith/Documents/Courses/'Code for Journalists'/ /Volumes/usbdrive/code/

**WAIT UNTIL THE PROMPT REAPPEARS** (e.g., `bash-3.2#`). Do not touch any key until then. It might take a while! 

Before removing USB drive:

`umount /dev/disk2s1`

**(NOTE: That is not un -- it is u.)**

Remember, your USB drive might not be named `disk2s1` on your Mac. 

## Sources 

These were the most helpful to me.

http://jsalovaara.com/blog/backing-up-files-to-a-usb-drive-using-single-user-mode.html

http://alvinalexander.com/mac-os-x/mac-osx-single-user-mode-usb-drive

http://www.tuaw.com/2011/09/19/mac-101-format-choices-for-usb-flash-drives/

