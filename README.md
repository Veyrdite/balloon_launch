Ballon detachment code for http://www.bluesat.unsw.edu.au/

# Requirements
* Raspberry pi
* rtl-sdr dongle
* *nix based OS (eg Debian deriv)
* deps: rtl-fm multimon python bash & the python GPIO libraries for raspi

This codes hardcodes a couple of locations.  Grep for /home/pi if you want to change this for personal use.

# Function and code overview

master.sh runs all of the components.  Currently there are two:
* dtmf_seperation -- Seperated the satellite from the balloon.  RTL-SDR, Raspi, DTMF decoding
* namuru -- Logs GPS data over serial link


## dtmf_seperation
To use:
* ./compile.sh (binary for signal_detect.c not included)
* run ./manager

Each of the components chain onto each other via pipes or fifos.  From start to beginning is:
* rtl-fm (not included) -- reads raw data from RTL-sdr dongle
* multimon (not included) -- processes raw RF data -> finds DTMF codes
* multimon_processing -- strips prefixing "DTMF: " text from multimon output
* signal_detect -- looks for a pattern of DTMF tones and executes setPin.py when an expected pattern is found
* setPin.py -- toggles Raspberry Pi GPIO pins

# Issues
* setPin.py ignores pin owernership, so warnings will spew
* master.sh runs everything on the same terminal, so messages will overlap


# Licence
Todo.  Probably going to be public domain (as there is nothing here worth 'protecting'), but I will check with the team and other authors.
