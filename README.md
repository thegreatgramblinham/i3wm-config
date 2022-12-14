Overview
=================
This file contains the (roughly) serialized steps to setting up i3wm on a generic, barebones Debian instance.

Installing i3wm
=================
To begin, make sure all current apt packages are up to date and we are referencing most recent versions.
```
sudo apt update
sudo apt upgrade
```

Remove any obsolete packages.
```
sudo apt dist-upgrade
```

Then restart.
```
sudo reboot
```

Now we need to be able to launch an xserver instance to display a desktop.
```
sudo apt install xserver-xorg
sudo apt install xinit
```

Go ahead and grab the utilities package too if it's not already installed. We'll need this later for display configuration.
```
sudo apt x11-xserver-utils
```

Now we can install i3wm itself.
```
sudo apt install i3
```

Hit things with a restart just in case.
```
sudo reboot
```

Once you're back at the command line, fire things up with:
```
startx
```

Resolution Config
=================
Depending on your monitor, you may wish to sway away from the current resolution. To do this, we will use:
```
xrandr
```

This tool was installed from the x11-xserver-utils package an allows us to modify our display in various ways. To change resolution use the command:
```
xrandr --output <display_id> --mode <desired_resolution>
```
i.e.
```
xrandr --output HDMI-1 --mode 1920x1080
```