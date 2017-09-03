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

