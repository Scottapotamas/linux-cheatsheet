# linux-cheatsheet
Notes for personal tips/tricks/reminders and reference.

# Git

This is all standard stuff but leaving it here incase I have a stroke or something...

Checkout:

`git clone https://github.com/Scottapotamas/$REPO$`

Add files to staging:

'git add README.txt'

Create a commit:

'git commit -m "A useful message goes here"`

Push to the origin/remotes:

'git push'

Pull the latest tarball of a repo (kicad example):

`https://github.com/kicad/kicad-source-mirror/archive/master.tar.gz`



# Serial Ports 

To find out what port some hardware might be on, use

`dmesg | grep tty`

Then work out what /dev/ttyUSB or whatever its on.

If using picocom, then do something like

`picocom -b 115200 /dev/ttyUSB0`

Then to quit a picocom session, CTRL+a then CTRL+x

# Arduino IDE

As per [this thread](https://solus-project.com/forums/viewtopic.php?t=2968) its pretty easy to install. I went to the arduino.cc download page and grabbed the *nix 64 tar though as the version has updated.

Install openjdk from the solus repo.

Alias the libncurses as per

`
cd /usr/lib64
sudo ln -s libncurses.so.5.9 libtinfo.so.5
`

Then install it (and then promptly remove the hideous desktop shortcut it creates...)

`
tar -xf arduino-1.8.4-linux64.tar.xz
cd into the folder
./install.sh
`

Should work fine from that point on.

# ST-Link

Grab the stlink udev rule from [here](http://www.openstm32.org/Installing+System+Workbench+for+STM32+from+Eclipse)

Then untar and extract into /etc/udev/rules.d

`
sudo tar -xf stlink_udev_rule.tar.bz2 -C /etc/udev/rules.d
`

# Eclipse

## Dependancies and install

Install the openjdk from the solus repo.

Download the 64-bit installer from [here](http://www.openstm32.org/Downloading+the+System+Workbench+for+STM32+installer).

Reinstate the permissions with chmod 775, and then run it. Can't use the gui for install because of gksudo not being supported by solus as its "a bucket full of holes".

Run it by executing ./eclipse from the ~/Ac6/SystemWorkbench/ folder.

Seems to work out. Make isn't found by default in the path (or the std libs), so it needs to be added as part of the 'developing with solus' stuff:

`
sudo eopkg it -c system.devel
`

## Starting from the menu/command palette

To add it to the application menu, I used alacarte (menu manager) which was installed from the solus package repo. Eclipse generates an instance in the menu which isn't enabled by default, and it doesn't work for me.

I added a new object called SystemWorkbench, pulled a transparent background logo from their site into ~/Ac6 to act as the icon, and then made it call /Ac6/SystemWorkbench/eclipse

This now launches correctly from the menu and behaves as it should mostly.

## Building STM32 projects

Building a STM32 project requires the arm-none-eabi-gcc tool. This is installed by the SW4 plugin when eclipse runs, but make files don't seem to be able to find it in the install, and manually testing it didn't work.

To fix this, we need to install the 32-bit toolchain! The SW4 install notes do mention this, but its more of an issue with Solus as the installer didn't get everything right.

This has been suggested before and is marked as 'ready for inclusion' as part of solus T426.

# KiCAD nightly or building from source with Solus

Pull the solus kicad repo from their git, and follow my notes in https://solus-project.com/forums/viewtopic.php?f=20&t=9897&p=30728#p30728.

# KiCAD to use libraries from my own git repos

The fp-lib-table and sym-lib-tables are in /home/scott/.config/kicad.

I then removed them, and symlinked them to the files in my personal kicad repos like

`
ln -sfn ~/projects/ECAD/appli-modules/fp-lib-table ~/.config/kicad/fp-lib-table 

ln -sfn ~/projects/ECAD/appli-library/sym-lib-table ~/.config/kicad/sym-lib-table
`


Restart kicad, ensure the .pro doesn't use absolute library references, and there is a reference to the libs path, and things should work reasonably well.

# General Bash Notes

To log something to file while viewing it in the terminal,

`commands | tee filename.txt`

# Particle Photon Boards

[po-util](https://po-util.com/) looks like the go.

TODO actually get this toolchain working.

# Solus stuff

I'm sure plenty will go here over time...

eopkg is the package manager, relearn that instead of apt-get.

`
eopkg it
`

## Stuff in the package manager that is nice

alacarte does menu configuration.



## Reading hardware sensors

To read temps and fan speeds,

`sudo eopkg install lm_sensors`

`inxi -xs`

