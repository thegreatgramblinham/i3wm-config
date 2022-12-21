File System Operations
===
Mounting a storage device
===
Before plugging in any device run the following command 
```
sudo fdisk -l
```
This will list all the storage devices visible to the system. We do this beforehand so we can more readily identify the storage device once it is connected (it will be the new device in the diff)

Now plug in your device and rerun the above command. A new device/name should have appeared in this output. Double check by looking for the expected number of partitions and their sizes.

Next, create a mount point for this device's data to be mounted to:
```
mkdir /media/<name of your choice>
(i.e. mkdir /media/usb-drive)
```
Afterwards, simply point the device's partition name you identified to that mount point similar to this:
```
sudo mount /dev/sdb1 /media/usb-drive
```
Then all that device's data should be accessible in your mount point directory. The root command 'mount' can also be used to list mounted devices.

When the time comes to unmount your device, make sure all programs and terminals no longer point to the mount point directory, otherwise you will be told the 'device is busy'. Then run 'umount' on your mount point similar to this:
```
sudo umount /media/usb-drive
```
Note: This command is named *umount* not unmount. This is not a spelling mistake.

Some GUI applications (like file explorers) can still register the device as mounted, so be sure to eject the device there too as to not ultize it erroneously. Still not sure what is up with this. Will update as I learn more.


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
sudo dd bs=4M if=/dev/mmcblk0 of=/dev/sda conv=fsync status=progress
```
In this example 'mmcblk0' is the root node of our working file system and that is being copied to the *unmounted* storage device located at the 'sda' root node.

Tip: The 'bs' flag stands for "block size" and a reasonable place to start if you desire to specify your own block size (the default is 512) is by running the 'stat' command on the directory you are copying. For example, in the line above:
```
stat /dev/mmcblk0
```
The return will be in the "IO Block:" field. This may not be the actual fastest value for bs, but it should serve as a decent starting point.

An image file can be created by specifing the 'of' varible to a location on the filesystem and appending '.img' as in this example:
```
sudo dd if=/dev/sda of=~/image-of-drive.img status=progress
```
