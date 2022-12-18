File System Operations
===
Mounting a drive
===
//TBD


Backing up the root file system
===
Using the "Data Dump" (dd) program common to Linux, drive images can be created or drives can be copied from one location to another.

The following command can transfer the contents of one storage device to another:
```
sudo dd if=<DRIVE TO READ> of=<DRIVE TO WRITE TO>
```
In order to get these drive/device names we can use:
```
lsblk
```
Which will list all the blocks currently visible to the system.

IMPORTANT: Your target drive/device ('of') needs to be unmounted before proceeding with a dd command.

An example of a drive to drive copy:
```
sudo dd bs=4M if=/dev/mmcblk0 of=/dev/sda conv=fsync
```
In this example 'mmcblk0' is the root node of our working file system and that is being copied to the *unmounted* storage device located at the 'sda' root node.

An image file can be created by specifing the 'of' varible to a location on the filesystem and appending '.img' as in this example:
```
sudo dd if=/dev/sda of=~/image-of-drive.img
```