Overview
===
This section will cover basic setup of prefered programs.

These instructions are intended for, and have been tested on, Raspberry Pi OS - Lite (64bit).


Core Applications
===
Git
===
[Git](https://git-scm.com/), the ubiquitous SCM, can be installed via Debian package:
```
sudo apt install git
```

Firefox
===
[Firefox](https://www.mozilla.org) can be installed via Debian package
```
sudo apt install firefox-esr
```
Note: The "esr" variant is the "LTS" version. It literally stands for "extended support release".

GNOME Terminal
===
[Gnome Terminal](https://help.gnome.org/users/gnome-terminal/stable/) can be installed via Debian package:
```
sudo apt install gnome-terminal
```
In order to configure the default terminal in your Debian distribution, run:
```
sudo update-alternatives --config x-terminal-emulator
```
and select your desired terminal from the list.

Vim
===
[Vim](https://www.vim.org/) can be installed via Debian package:
```
sudo apt install vim-gtk
```
(the gtk variant is complied with extra features like system clipboard integration)

In order to configure the default editor in your Debian distribution, run:
```
sudo update-alternatives --config editor
```
and select your desired editor from the list.

For more information on how to configure Vim, including building from source, check out [this repo.](https://github.com/thegreatgramblinham/vim-config)

OS Tools
===
Midnight Commander
===
[Midnight Commander](https://midnight-commander.org/) can be installed via Debian package:
```
sudo apt install mc
```

Tip: While configuring mc, 'Options > Panel Options > Lynx-like motion' allows you to move up and down directory levels with the arrow keys. Super useful.

When you're happy with all configurations made to the program, use 'Options > Save setup' to commit your settings for next boot.

Ranger
===
(This has largely replaced Midnight Commander for me)
[Ranger](https://github.com/ranger/ranger) can be installed via Debian package:
```
sudo apt install ranger
```
Check out [the repo](https://github.com/thegreatgramblinham/ranger-config) for specific instructions and config.

GParted
===
[GParted](https://gparted.org/) can be installed via Debian package:
```
sudo apt install gparted
```

Raspberry Pi Imager
===
[Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager) can be installed via Debian package:
```
sudo apt install rpi-imager
```

Pulse Audio Control
===
[Pulse Audio Control]() is a gui tool to control the pulse audio service. It can be installed via Debian
package:
```
sudo apt install pavucontrol
```

Feh
===
[feh]() is a cli image viewer that is also compatable with Ranger. It can be installed via Debian
package:
```
sudo apt install feh
```

Htop
===
[Htop](https://htop.dev/) can be installed via Debian package:
```
sudo apt install htop
```

TCPDump
===
[TCPDump](https://www.tcpdump.org/) can be installed via Debian package:
```
sudo apt install TCPDump
```

Neofetch
===
[Neofetch](https://github.com/dylanaraps/neofetch) can be installed via Debian package:
```
sudo apt install neofetch
```

Ripgrep
===
[ripgrep](https://github.com/BurntSushi/ripgrep) can be installed via Debian package:
```
sudo apt install ripgrep
```
Grep features with ease of use improvements.

3D Printing Applications
===
OpenSCAD
===
[OpenSCAD](https://openscad.org/) can be installed via Debian package:
```
sudo apt install openscad
```

Slic3r
===
[Slic3r](https://slic3r.org/) can be installed via Debian package:
```
sudo apt install slic3r
```

PrusaSlicer
===
Built on top of Slic3r and is much more stable. Has to be built from source from the [git repo](https://github.com/prusa3d/PrusaSlicer) where there are [build instructions for Linux](https://github.com/prusa3d/PrusaSlicer/blob/master/doc/How%20to%20build%20-%20Linux%20et%20al.md)

KiCad
===
The easiest way to get the most recent binaries is to use flatpak:
```
sudo flatpak install --from https://flathub.org/repo/appstream/org.kicad.KiCad.flatpakref
```
then after, it can be run with:
```
flatpak run org.kicad.KiCad
```


Other
===
Arduino IDE
===
[Arduino IDE](https://www.arduino.cc/en/software) should be available from the main website in a .tar.gz file. Releases can also be found on [the GitHub page.](https://github.com/arduino/arduino-ide)

There is technically not an official arm binary yet, but there are v2 app images complied [here.](https://github.com/koendv/arduino-ide-raspberrypi)

Gmsh
===
[Gmsh](https://gmsh.info/) can be installed via Debian package:
```
sudo apt install gmsh
```

Flameshot
===
[Flameshot](https://flameshot.org/) can be installed via Debian package:
```
sudo apt install flameshot
```

Armcord
===
[Armcord](https://github.com/ArmCord/ArmCord) can be installed via package source.
Details are included on their GitHub page.
