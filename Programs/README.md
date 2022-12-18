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
//TODO details to come on configuring SSH connectivity

Firefox
===
[Firefox](https://www.mozilla.org) can be installed via Debian package
```
sudo apt install firefox-esr
```
Note: The "esr" variant is the "LTS" version. It literally stands for "extended support release".

VSCode
===
[VSCode](https://code.visualstudio.com/) can be installed via Debian package:
```
sudo apt install code
```
From there, [check out this repository](https://github.com/thegreatgramblinham/vscode-config) for more detailed information on how to set up VSCode.

GNOME Terminal
===
[Gnome Terminal](https://help.gnome.org/users/gnome-terminal/stable/) can be installed via Debian package:
```
sudo apt install gnome-terminal
```
In order to configure the default terminal in your Debian distribuition, run:
```
sudo update-alternatives --config x-terminal-emulator
```
and select your desired terminal from the list.


OS Tools
===
Midnight Commander
===
[Midnight Commander](https://midnight-commander.org/) can be installed via Debian package:
```
sudo apt install mc
```

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

Htop
===
[Htop](https://htop.dev/) can be installed via Debian package:
```
sudo apt install htop
```

Neofetch
===
[Neofetch](https://github.com/dylanaraps/neofetch) can be installed via Debian package:
```
sudo apt install neofetch
```

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
