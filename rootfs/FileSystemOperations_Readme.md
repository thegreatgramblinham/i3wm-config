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

Creating a shared network folder
===
We will be using Samba which will allow Windows and Linux compatibility for network shares.
```
sudo apt install samba
```
You can check to make sure it was successfully installed with:
```
smbd --version
```

After installation is complete, start the Samba service with:
```
sudo systemctl enable --now smbd
```

From here, we need to edit a configuration file to tell our Samba service what we want to share. Launch your favorite text editor pointed to:
```
sudo nano /etc/samba.smb.conf
```
This is where we will define our new fully public share configuration. It should look something like this:
```
# Header that designates a new share section
[sample-home-dir-share]
comment = This is a sample network share
# Path to the shared directory
path = /home/<user name>
public = yes
browsable = yes
writable = yes
read only = no
force create mode = 0666
force directory mode = 0777
```
TBD: I'll get back to you on what the hell those mode assignments mean, but the rest is pretty self-explainatory.

Once the configuration has been saved, restart the Samba service with:
```
sudo systemctl restart smbd
```

As the final step, we need to designate a user for this share to be used with.

*NOTE: This user also has to be the owner of the share directory.
If you are unsure of a file or directory's owner, navigate just outside the target in the terminal and use:
```
ls -l
```
The third column is the file owner.

In the case of a home directory, this has to be the user who the home directory belongs to. So in our example we need to:
```
# Add the user, then password when prompted
sudo smbpasswd -a <user name>
# Enable the user
sudo smbpasswd -e <user name>
```

This is enough to get a basic share up and running (after another restart of the samba service), but it's not exactly secure. Depending on if the network share requires more robust security we may want to create a separate user to handle a public share.

If we want to create a new user of the share, we instead need to do:
```
sudo adduser sambaguest
```
'sambaguest' is the new user name here. The name is abitrary.

Then provide a password that is as secure as you want it to be. Could be a robust password, or just the username duplicated. (Other new user params can just be taken as default).

Using the same commands as above, the new user will have to be added to samba and enabled.

As the last step, the network share owner will have to be changed to our new user. Warning: This can be a dangerous operation if peformed on the wrong location. Ensure your share is in a user agnostic directory and safe to have its permissions replaced.
To change ownership we use:
```
sudo chown --recursive <directory to>/<network share>
```

Restart the Samba service again and you should be good to go!
```
sudo systemctl restart smbd
```
