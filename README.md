# linux-cheatsheet
Notes for personal tips/tricks/reminders and reference.

# Git

git clone https://github.com/Scottapotamas/$REPO$



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

# General Bash

To log something to file while viewing it in the terminal,

`commands | tee filename.txt`


# Solus stuff

I'm sure plenty will go here over time...

eopkg is the package manager, relearn that instead of apt-get

## Reading hardware sensors

To read temps and fan speeds,

`sudo eopkg install lm_sensors`

`inxi -xs`

