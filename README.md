
Pi SSTV (Currently a working progress, therefore some files are missing. Instead try out my other project, PIFM-GTK!)
=========

## What is Pi SSTV?
This first sections covers the need for Pi SSTV and why it was created. If you are only looking for the installation, skip ahead to the [setup](#Prepping-the-Pi).

Pi SSTV is an extension to one of my previous projects [PiFM GTK](https://github.com/mundeeplamport/PiFM). Pi SSTV is intended for use by ham radio operators as a way to transmit photos that have been captured using the Raspberry Pi Camera Module. Furthermore, it is designed for regular FM radio (87.5 - 108.0MHz) to transmit, however the software does allow you to choose values outside this range. The purpose of designing it in this way is so that people who do not have a ham radio setup are still able to understand and interact with the software and see how it functions.

![](doc/SSTV.jpg)
As it is requires a license to transmit on certain FM frequencies, please read the [legal warning](#warning-and-disclaimer).

## Compatibility
This piece of software is designed to work on all versions of the Raspberry Pi including the 4! The installation is designed to be done on Raspberry Pi OS which is the Official Raspberry Pi Operating System. From testing, the operating system must be from at least 2015 as the `rpi-mailbox` driver is not included in earlier versions. To have the greatest chance of the software working, it is recommended to use a fresh install of Raspberry Pi OS as it has the most up-to-date drivers with support for the latest versions of the Raspberry Pi.

## How it works
This program generates an FM modulation, with RDS (Radio Data System) data generated in real-time, which isn't particularly relevant for ham radio, but it has the capabilities. PiFM modulates the PLLC instead of the clock divider for increased signal purity, meaning that the signal is also less noisy. For the PLLC modulation to be stable, there is an additional step. Due to the low-voltage detection, the PLLC frequency can be reduced to a safe value in an attempt to restrict crashes. When this happens, the carrier freqency changes based on the GPU frequency. To prevent this, we can tweak the GPU freqency to match the safe frequency. Now when due the low voltage detection occurs, the PLLC frequency changes to safe value, meaning nothing happens since the normal value and safe value are identical.

This project is based on an earlier FM transmitter developed by [Oliver Mattos and Oskar Weigl](http://www.icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter), and later adapted to using DMA by [Richard Hirst](https://github.com/richardghirst). Christophe Jacquet manipulated it, adding the RDS data generator and modulator, and myself, adding the zenity based interace. The SSTV conversion is based on work by KI4MCW (which can be found [here](https://sites.google.com/site/ki4mcw/Home/sstv-via-uc)). The transmitter uses the Raspberry Pi's PWM generator to produce VHF signals.

![](doc/radio.jpg)
PiFM has been developed solely for experimentation only. See the [legal warning](#warning-and-disclaimer).

## Prepping the Pi
**Required Equipment:**
* Raspberry Pi (1a, 1b, 1a+, 1b+, 2b, 3b, 3a+, 3b+, Zero, Zero W, 4 are all compatible)
* Acceptable power supply (recommended at least 2A)
* SD Card (4gb minimum with Raspberry Pi OS Desktop installed. See [installation guide](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2))
* Mini HDMI cable (Pi Zero, Zero W)  (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* HDMI cable (Pi 1a, 1b, 1a+, 1b+, 2b, 3b, 3a+, 3b+, 4) (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* Ethernet cable (unless it has onboard WiFi or you have a WiFi dongle)
* USB keyboard/mouse (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* HDMI monitor/tv to display the desktop (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* Raspberry Pi camera module (any version should work)

**Optional Equipment:**
* Portable display (to make it more compact and portable)
* Portable power bank (so that you can use it on the go)
* Piece of wire to act as an antenna

## Installation
PiFM SSTV depends on a number of prerequisites. These are required. to get the transmitter ready.
1. Install Raspberry Pi OS Desktop onto an SD card (click [here](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2) for a detailed guide)
2. Connect your peripherals to the Raspberry Pi (keyboard/mouse/SD/HDMI/etc...)
3. Once you are ready to start, turn on the Pi and wait until the desktop environment appears.
4. At the top left of the screen click the terminal icon and wait for the terminal window to load
5. Once it has loaded, type in the following commands.

**Pi 4 Installation**
```
git clone https://github/com/mundeeplamport/PiFM-SSTV
```
This will download the software from this repository
```
chmod +x /home/pi/PiFM-SSTV/setup-pi4.sh
```
This changes the permissions to allow you to run the setup
```
./PiFM-SSTV/setup-pi4.sh
```
**Previous Pi Versions**
```
git clone https://github/com/mundeeplamport/PiFM-SSTV
```
This will download the software from this repository
```
chmod +x /home/pi/PiFM-SSTV/setup.sh
```
This changes the permissions to allow you to run the setup
```
./PiFM-SSTV/setup.sh
```
This begins the installation script for the software and is a fully automated process, and very verbose, so you can see what is happening. Please note that your Raspberry Pi will automatically reboot after the installation is complete.

**Important.** The binaries compiled for each Raspberry Pi is different. Therefore, always re-compile when switching models. To do this, simply re-run the installer.

## Usage
* Find the PiFM SSTV shortcut in the applications menu in the 'other' submenu.
* Use the shortcut located on the desktop.
* Open a terminal window and type `pifm-sstv` and hit enter.
Once loaded, a terminal window will appear providing information about the software as well as well as some information. After 5 seconds, you will be asked to take a photo as well as what frequency to transmit on. After this, the software will start broadcasting the photo.

If at any point you wish to close the broadcast, make the terminal window active and press CTRL and C at the same to interrupt the program.

## Warning and Disclaimer
PiFM SSTV is an **very experimental** program, designed **only for experimentation**. It is in no way intended to become a personal *photo transmitter* or a tool to operate a *broadcast station*, or even broadcast sound to one's own system.

In most countries, transmitting radio waves without a state-issued licence specific to the transmission modalities (frequency, power, bandwidth, etc.) is **illegal**.

Therefore, always connect a shielded transmission line from the Raspberry Pi directly
to a radio receiver, so as **not** to emit radio waves. Never use an antenna.

Even if you are a licensed amateur radio operator, using PiFM SSTV to transmit radio waves on ham frequencies without any filtering between the Raspberry Pi and an antenna is most most likely illegal since the square-wave carrier is very rich in harmonics, so the bandwidth requirements are likely not met.

I can not be held liable for any misuse of your own Raspberry Pi. Any experimentation is done under your own responsibility.

--------
© [Mundeep Lamport](https://instagram.com/mundeep.l) 2020. Released under the GNU GPL v3.
