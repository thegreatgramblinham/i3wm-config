Overview
===
This file contains the (roughly) serialized steps to setting up [i3wm](https://i3wm.org) on a generic, barebones Debian-based Linux instance. For more advanced configuration, refer to the [i3wm User's Guide](https://i3wm.org/docs/userguide.html).

These instructions are intended for, and have been tested on, Raspberry Pi OS - Lite (64bit).

Basic i3wm Shortcut Reference
===
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

Reload i3wm                    => mod+shift+r
Exit i3wm                      => mod+shift+e
```

Installing i3wm
===
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

Go ahead and grab some utilities packages too if it's not already installed. We'll need this later for configuration:
```
sudo apt install x11-xserver-utils
sudo apt install xinput
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

First boot
===
Upon first boot of i3wm, you'll be asked if you want to generate a config file. Accept this. Then you'll be asked to specific the modifier key. I highly recommend the binding the mod key to the OS key.

i3wm Config
===
The heart of i3wm config lives in the home directory (represented as "~/") under
```
~/.config/i3/config
```
be sure to use the command
```
ls -al
```
to be able to see hidden files.

This file controls most of the behavior of i3wm, including keybindings and start up commands (exec). There is a copy of this file in the repository so it should not have to be created after each fresh install.

One time startup command line functions can be added with the prefix:
```
exec <command>
```

Commands that need to be run *each* time i3wm is restarted (meaing mid-session) must be prefixed with:
```
exec_always <command>
```

Variables can be allocated with the following syntax:
```
set $variableName "<text_value>"
```
This will set <text_value> anywhere below where "$variableName" is defined.

Keyboard Config
===
Keyboard layout is stored in the file:
```
/etc/default/keyboard
```
Mouse Config
===
To change things like mouse pointer acceleration (:vomiting_face:), we first need to call xinput:
```
xinput --list
```
From there we can get the "device id" or name of our pointing device we want to modify.

At the time of writing, mouse acceleration is controled by an xorg .conf file located:
```
/etc/X11/xorg.conf.d/50-mouse-acceleration.conf
```
The current version of that file will be maintained in this repo.

Additional configuration options can be found in the documentation, [found here.](https://xorg.freedesktop.org/wiki/Development/Documentation/PointerAcceleration/#Introduction)

[And here @ ArchLinuxWiki - MouseAcceleration](https://wiki.archlinux.org/title/Mouse_acceleration)

Time/Date Config
===
To set your current timezone, we'll use:
```
timedatectl list-timezones
```
Once you've found yours, simply use the set command. For example:
```
timedatectl set-timezone America/New_York
```

Display Config
===
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


To enable a secondary monitor, provide ID and a position like so:
```
xrandr --output HDMI-2 --right-of HDMI-1
```

This call can be inserted into i3wm just like any other. i3wm only seems to like *ONE* call to xrandr in the config file, but multiple command can be passed together. For example:
```
exec xrandr --output HDMI-1 --mode 1920x1080 --output HDMI-2 --mode 1920x1080 --output HDMI-2 --right-of HDMI-1
```

Font Config
===
Any .ttf file can be placed into the home directory under:
```
~/.fonts
```
From there, it should be available as an installed font.

Desktop Background Config
===
An addtional program is needed to manage our background image. Here we'll be using feh.
```
sudo apt install feh
```
This call can be inserted into i3wm just like any other to ensure it starts with each boot.



