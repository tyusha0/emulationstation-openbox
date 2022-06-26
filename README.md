# emulationstation-openbox
An xsession that runs Emulationstation on top of an Openbox session

## Install

**Debian/Ubuntu distros**

```bash
./build.sh
sudo dpkg -i emulationstation-openbox.deb
```

**Arch distros**

```bash
sudo pacman -S fakeroot dpkg debtap
./build.sh
debtap emulationstation-openbox.deb
```

This will return an Arch package that can be installed with your favorite package manager, (Pacman, Octopi, Pamac, etc).


**Other Linux distros**

Note, this command manually copies all files to their intended places in the filesystem, meaning they will need to be uninstalled manually.

```bash
sudo cp -r -t /usr emulationstation-openbox/usr/**/*
```

## Usage

On most systems, you should be able to choose your X session at the login screen. Choose "Emulationstation Openbox" and log in to start the session.

### Commands

* **emulationstation-openbox-session** - runs a emulationstation-openbox session
* **emulationstation-openbox-runprogram** - closes emulationstation and runs a command. Emulationstation will reopen when the command completes. Arguments are the command to run

### Openbox background
To set the background color of your openbox session, add the following command to *~/.config/openbox/autostart.sh*
``` bash
xsetroot -solid '#000000'
```
This will set the openbox background color to black, but you can change the hex value to be any color.

### Launching external programs from emulationstation
If you want emulationstation to close when launching an external program, use the **emulationstation-openbox-runprogram** command as your program, and the command you want to run as its arguments.

### Preventing display sleep in external programs
If your display keeps going to sleep outside of emulationstation, it may be caused by a number of different programs.

To prevent gnome desktop from putting your display to sleep, run the following commands in a terminal while logged in as your emulationstation user:
``` bash
# Prevent display from going to sleep
gsettings set org.gnome.desktop.session idle-delay 0
# Prevent session from locking if the display does go to sleep
gsettings set org.gnome.desktop.screensaver lock-enabled false
```
To prevent X11 from putting your display to sleep, add the following commands to *~/.config/openbox/autostart.sh*
``` bash
# Disable screen saver
xset s off
# Disable screen blanking
xset s noblank
# Disable "Display Power Management Signaling"
xset -dpms
```
