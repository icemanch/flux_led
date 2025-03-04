# Magic Flux Led 

[![Build Status](https://travis-ci.org/icemanch/flux_led.svg?branch=master)](https://travis-ci.org/icemanch/flux_led)

- `Repository:` https://github.com/icemanch/flux_led

[<kbd>Download as a ZIP Archive</kbd>][ZIP Archive]

-----

**Table of Contents**


<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3,4" -->

- [Welcome](#welcome)
- [Installation](#installation)
- [Examples](#examples)
- [Credits](#credits)

<!-- /MarkdownTOC -->

-----
# Welcome

This is a utility for controlling stand-alone Flux WiFi LED light bulbs.
The protocol was reverse-engineered by studying packet captures between a 
bulb and the controlling "Magic Home" mobile app.  The code here dealing 
with the network protocol is littered with magic numbers, and ain't so pretty.
But it does seem to work!

So far most of the functionality of the apps is available here via the CLI
and/or programmatically.

The classes in this project could very easily be used as an API, and incorporated into a GUI app written 
in PyQt, Kivy, or some other framework.

##### Available:
* Discovering bulbs on LAN
* Turning on/off bulb
* Get state information
* Setting "warm white" mode
* Setting RGB
* Setting RGBW
* Setting RGBWW
* Setting "CCT"  (White Temp)
* Setting preset pattern mode
* Setting custom pattern mode
* Reading timers
* Setting timers
* Sync clock
	
##### Some missing pieces:
* Initial administration to set up WiFi SSID and passphrase/key.
* Remote access administration
* Music-relating pulsing. This feature isn't so impressive on the Magic Home app, 
and looks like it might be a bit of work.
	  
##### Cool feature:
* Specify colors with names or web hex values.  Requires that python "webcolors" 
package is installed.  (Easily done via pip, easy_install, or apt-get, etc.) Use --listcolors to show valid color names.

-----
# Installation
* Flux_led package available at https://pypi.python.org/pypi/magic-flux-led/
```
pip install magic_flux_led

easy_install magic_flux_led
```
-----
# Examples
```
Scan network:
	python -m magic_flux_led -s

Scan network and show info about all:
	python -m magic_flux_led -sSti

Turn on:
	python -m magic_flux_led 192.168.1.100 --on
	python -m magic_flux_led 192.168.1.100 -192.168.1.101 -1

Turn on all bulbs on LAN:
	python -m magic_flux_led -sS --on

Turn off:
	python -m magic_flux_led 192.168.1.100 --off
	python -m magic_flux_led 192.168.1.100 --0
	python -m magic_flux_led -sS --off
	
Set warm white, 75%
	python -m magic_flux_led 192.168.1.100 -w 75 -1

Set fixed color red :
	python -m magic_flux_led 192.168.1.100 -c Red
	python -m magic_flux_led 192.168.1.100 -c 255,0,0
	python -m magic_flux_led 192.168.1.100 -c "#FF0000"
	
Set preset pattern #35 with 40% speed:	
	python -m magic_flux_led 192.168.1.100 -p 35 40
	
Set custom pattern 25% speed, red/green/blue, gradual change:
	python -m magic_flux_led 192.168.1.100 -C gradual 25 "red green (0,0,255)"

Sync all bulb's clocks with this computer's:
	python -m magic_flux_led -sS --setclock
		
Set timer #1 to turn on red at 5:30pm on weekdays:
	python -m magic_flux_led 192.168.1.100 -T 1 color "time:1730;repeat:12345;color:red"
	
Deactivate timer #4:
	python -m magic_flux_led 192.168.1.100 -T 4 inactive ""

Use --timerhelp for more details on setting timers
```
	
##### Show help:
```	
$ python -m magic_flux_led -h
Usage: usage: __main__.py [-sS10cwpCiltThe] [addr1 [addr2 [addr3] ...].

A utility to control Flux WiFi LED Bulbs.

Options:
  -h, --help            show this help message and exit
  -s, --scan            Search for bulbs on local network
  -S, --scanresults     Operate on scan results instead of arg list
  -i, --info            Info about bulb(s) state
  --getclock            Get clock
  --setclock            Set clock to same as current time on this computer
  -t, --timers          Show timers
  -T NUM MODE SETTINGS, --settimer=NUM MODE SETTINGS
                        Set timer. NUM: number of the timer (1-6). MODE:
                        inactive, poweroff, default, color, preset, or
                        warmwhite. SETTINGS: a string of settings including
                        time, repeatdays or date, and other mode specific
                        settings.   Use --timerhelp for more details.

  Program help and information option:
    -e, --examples      Show usage examples
    --timerhelp         Show detailed help for setting timers
    -l, --listpresets   List preset codes
    --listcolors        List color names

  Power options (mutually exclusive):
    -1, --on            Turn on specified bulb(s)
    -0, --off           Turn off specified bulb(s)

  Mode options (mutually exclusive):
    -c COLOR, --color=COLOR
                        Set single color mode.  Can be either color name, web
                        hex, or comma-separated RGB triple
    -w LEVEL, --warmwhite=LEVEL
                        Set warm white mode (LEVEL is percent)
    -p CODE SPEED, --preset=CODE SPEED
                        Set preset pattern mode (SPEED is percent)
    -C TYPE SPEED COLORLIST, --custom=TYPE SPEED COLORLIST
                        Set custom pattern mode. TYPE should be jump, gradual,
                        or strobe. SPEED is percent. COLORLIST is a space-
                        separated list of color names, web hex values, or
                        comma-separated RGB triples
```
-----
# Credits

The majority of this code was written by - __[Danielhiversen]__ —Daniel Hjelseth Høyer

<!-- People Links -->
[Danielhiversen]: https://github.com/Danielhiversen "View @Danielhiversen's GitHub profile"

<!-- repo links -->

[ZIP Archive]: https://github.com/icemanch/flux_led/archive/master.zip "Download a ZIP file of this project (without Git contents)"


