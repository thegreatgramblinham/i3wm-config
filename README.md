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

In order to change the DPI scaling of your xserver instance include the following option in the .Xresources file in your home directory:
```
Xft.dpi: 120
```

Font Config
===
Any .ttf file can be placed into the home directory under:
```
~/.fonts
```
From there, it should be available as an installed font.

Desktop Wallpaper Config
===
An addtional program is needed to manage our wallpaper image. Here we'll be using feh.
```
sudo apt install feh
```

An example call to set a background image using the "scale" layout would be:
```
feh --bg-scale <Path to file>
```
This call can be inserted into i3wm just like any other to ensure it starts with each boot.

If only a solid color is disired, that can be done with the command:
```
xsetroot -solid "$desktopBgClr"
```

i3wm Window Color Config
===
All window and bar color selection is done through the main i3wm config file. There is an example of these file in the repository with many colors pre-defined. Simply modify those values to make further changes however you like. A few useful resources for planning changes may be:

- [Online i3 Color Configuration Tool](https://thomashunter.name/i3-configurator/)
- [Hex Color Picker](https://colors-picker.com/hex-color-picker/)

GTK Theme Config
===
Most applications refer to gtk2.0 or gtk3.0 to theme themselves according to your system. Configuring your gtk theme is akin to setting the overall system theme. To do this, we will use lxappearance. It can be installed via Debian package with:
```
sudo apt install lxappearance
```
Note: I attempted to install 'kde-config-gtk-style' since lxappearence seems to be not actively developed anymore. However I was too dumb to figure out how to launch the config dialog and reverted to lxappearance.

From there, common themes can be installed via Debian package. The classic Arc theme can be installed with:
```
sudo apt install arc-theme
```
Afterwards, the themes should be selectable in your config dialog of choice.

i3wm Bar Layout Config
===
Install i3blocks with:
```
sudo apt install i3blocks
```
Move the default conf file, created when i3blocks was installed, to the i3 config directory:
```
sudo cp /etc/i3blocks.conf ~/.config/i3
```
There is a copy of the i3blocks.conf file in this repository, in the expected relative location. The i3wm config file will need a line to make sure the i3blocks command runs instead of the default, which should also already be added.