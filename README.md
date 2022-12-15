Overview
=================
This file contains the (roughly) serialized steps to setting up [i3wm](https://i3wm.org) on a generic, barebones Debian-based Linux instance. For more advanced configuration, refer to the [i3wm User's Guide](https://i3wm.org/docs/userguide.html).

Basic i3wm Shortcut Reference
=================
```
Open terminal                  => mod+enter
Move tile focus                => mod+arrow
Close current tile             => mod+shift+q
Application run menu           => mod+d
Next tile split vertical       => mod+v
Enter resize mode              => mod+r

Shift curr tile location       => mod+shift+arrow
Move to workspace#             => mod+number
Move curr tile to workspace#   => mod+shift+number

Switch to stack view           => mod+s
Switch to tile view            => mod+e
Switch to tab view             => mod+w

Exit i3wm                      => mod+shift+e
```

Installing i3wm
=================
To begin, make sure all current apt packages are up to date and we are referencing most recent versions:
```
sudo apt update
sudo apt upgrade
```

Remove any obsolete packages:
```
sudo apt dist-upgrade
```

Then restart:
```
sudo reboot
```

Now we need to be able to launch an xserver instance to display a desktop:
```
sudo apt install xserver-xorg
sudo apt install xinit
```

Go ahead and grab the utilities package too if it's not already installed. We'll need this later for display configuration:
```
sudo apt x11-xserver-utils
```

Now we can install i3wm itself:
```
sudo apt install i3
```

Hit things with a restart just in case:
```
sudo reboot
```

Once you're back at the command line, fire things up with:
```
startx
```

i3wm Config
=================
The heart of i3wm config lives in the home directory (represented as "~/") under
```
~/.config/i3/config
```
This file controls most of the behavior of i3wm, including keybindings and start up commands (exec). There is a copy of this file in the repository so it should not have to be created after each fresh install. 

Display Config
=================
Depending on your monitor, you may wish to sway away from the current resolution. To do this, enter:
```
xrandr
```

This tool was installed from the x11-xserver-utils package an allows us to modify our display in various ways. 
To change resolution use the command:
```
xrandr --output <display_id> --mode <desired_resolution>
```
i.e.
```
xrandr --output HDMI-1 --mode 1920x1080
```

Enable a secondary monitor, provide ID and a position like so:
```
xrandr --output HDMI-2 --right-of HDMI-1
```

Desktop Background Config
=================
//TODO

Keyboard Config
=================
Keyboard layout is stored in the file:
```
/etc/default/keyboard
```


