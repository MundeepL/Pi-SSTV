
Pi SSTV
=========

## What is Pi SSTV?
This first sections covers the need for Pi SSTV and why it was created. If you are only looking for the installation, skip ahead to the [setup](#Prepping-the-Pi).

Pi SSTV is an extension to one of my previous projects [PiFM GTK](https://github.com/mundeeplamport/PiFM-GTK). Pi SSTV is intended for use by ham radio operators as a way to transmit photos that have been captured using the Raspberry Pi camera module. Pi SSTV is heavily based on work by KI4MCW, which can be found [here](https://sites.google.com/site/ki4mcw/Home/sstv-via-uc) and it is thanks to him that we are able to get this project to work. Some of the errors that were in this work have been corrected and made more flexible.

Furthermore, PiFM has been adapted so that the bandwidth can be configured, which is particularly important for narrow-band ham radio transmissions. Another addition is that the timing can be tuned, which is necessary since improper timings can reslt in slanted images.

![](doc/SSTV.jpg)
As it is requires a license to transmit on certain FM frequencies, please read the [legal warning](#warning-and-disclaimer).

## Compatibility
This piece of software is designed to work will all versions of the Raspberry Pi excluding the 4. The installation is designed to be done on Raspbian (lite or full), which is the Official Raspberry Pi Operating System. It is guaranteed to work on any version from August 2015 and later, as the installer is automatically designed to check that all dependencies are present (previous versions do not have the `rpi-mailbox` driver), however it is recommended to use a fresh install to reduce the likelihood of any errors.

## How it works
This program generates an FM modulation, with RDS (Radio Data System) data generated in real time, which isn't particularly relevant for ham radio but it has the capabilities. PiFM modulates the PLLC instead of the clock divider for increased signal purity, meaning that the signal is also less noisy. For the PLLC modulation to be stable there is an additional step. Due to the low-voltage detection, the PLLC frequency can be reduced to a safe value in an attempt to restrict crashes. When this happens, the carrier freqency changes based on the GPU frequency. To prevent this, we can tweak the GPU freqency to match the safe frequency. Now when due the low voltage detection occurs, the PLLC frequency changes to safe value, meaning nothing happens since the normal value and safe value are identical.

This project is based on an earlier FM transmitter developed by [Oliver Mattos and Oskar Weigl](http://www.icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter), and later adapted to using DMA by [Richard Hirst](https://github.com/richardghirst). Christophe Jacquet manipulated it, adding the RDS data generator and modulator, and myself, adding the zenity based interace. The transmitter uses the Raspberry Pi's PWM generator to produce VHF signals.

![](doc/radio.jpg)
PiFM has been developed solely for experimentation only. See the [legal warning](#warning-and-disclaimer).

## Prepping the Pi
**Required Equipment:**
* Raspberry Pi (1a, 1b, 1a+, 1b+, 2b, 3b, 3a+, 3b+, Zero, Zero W are all compatible)
* Acceptable power supply (recommended at least 2A)
* SD Card (4gb minimum with Raspbian Desktop installed. See [installation guide](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2))
* Mini HDMI cable (Pi Zero or Zero W)  (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* HDMI cable (Pi 1a, 1b, 1a+, 1b+, 2b, 3b, 3a+, 3b+) (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* Ethernet cable (unless it has onboard WiFi or you have a WiFi dongle)
* USB keyboard/mouse (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* HDMI monitor/tv to display the desktop (alternatively you can use SSH, for which setup can be found [here](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* Raspberry Pi camera module (any version should work)

**Optional Equipment:**
* Portable display (to make it more compact and portable)
* Portable power bank (so that you can use it on the go)
* Piece of wire to act as an antenna (GPIO 4)

## Installation
PiFM 1.2.1 depends on a number of prerequisites. These are required. to get the transmitter ready.
1. Install Raspbian Desktop onto an SD card (click [here](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2) for a detailed guide)
2. Connect your peripherals to the Raspberry Pi (keyboard/mouse/SD/HDMI/etc...)
3. Once you are ready to start, turn on the Pi and wait until the desktop environment appears.
4. At the top left of the screen click the terminal icon and wait for the terminal window to load
5. Once it has loaded, type in the following commands.
**Prior to Pi 4 Installation**
```
git clone https://github/com/mundeeplamport/Pi-SSTV
```
This will download the software from this repository
```
chmod +x /home/pi/PiFM/setup.sh
```
This changes the permissions to allow you to run the setup
```
./PiFM/setup.sh
```
This begins the installation script for the software and is a fully automated process, and very verbose, so you can see what is happening. Please note that your Raspberry Pi will automatically reboot after the installation is complete.

**Important.** The binaries compiled for each Raspberry Pi is different. Therefore, always re-compile when switching models. To do this, simply re-run the installer.

## Usage
* Find the PiFM-SSTV shortcut in the applications menu in the 'other' submenu.
* Use the shortcut located on the desktop.
* Open a terminal window and type `pifm-sstv` and hit enter.
Once loaded, a terminal will appear providing information about the software as well as well as some information. After 5 seconds, you will be asked to take a photo as well as what frequency to transmit on. After this, the software will start broadcasting the photo.

If at any point you wish to close the broadcast, make the terminal window active and press CTRL and C at the same to interrupt the program.

## Warning and Disclaimer
PiFM SSTV is an **very experimental** program, designed **only for experimentation**. It is in no way intended to become a personal *media center* or a tool to operate a *radio station*, or even broadcast sound to one's own stereo system.

In most countries, transmitting radio waves without a state-issued licence specific to the transmission modalities (frequency, power, bandwidth, etc.) is **illegal**.

Therefore, always connect a shielded transmission line from the Raspberry Pi directly
to a radio receiver, so as **not** to emit radio waves. Never use an antenna.

Even if you are a licensed amateur radio operator, using PiFM SSTV to transmit radio waves on ham frequencies without any filtering between the Raspberry Pi and an antenna is most most likely illegal since the square-wave carrier is very rich in harmonics, so the bandwidth requirements are likely not met.

I can not be held liable for any misuse of your own Raspberry Pi. Any experimentation is done under your own responsibility.

--------
© [Mundeep Lamport](https://instagram.com/mundeep.l) 2020. Released under the GNU GPL v3.
