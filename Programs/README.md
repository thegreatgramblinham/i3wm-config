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

For more information on how to configure Vim, check out [this repo.](https://github.com/thegreatgramblinham/vim-config)

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

Other
===
Arduino IDE
===
[Arduino IDE](https://www.arduino.cc/en/software) should be available from the main website in a .tar.gz file. Releases can also be found on [the GitHub page.](https://github.com/arduino/arduino-ide)

Note: At the time of writing, v2.0 of the IDE has been released but does not have Linux ARM 32/64 pacages anymore? Unclear if that will be added later. For now, use the last legacy release.
