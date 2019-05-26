# Waveshare Game-HAT guide
This guide provides step-by-step instructions on setting up the Game-HAT from Waveshare.
\
\
Its basically a setup-guide for the installation of a headless RetroPie-build but also contains additional 
instructions / settings / recommondations to greatly enhance the handheld-aspect of the system.

## Pre-Setup
This steps are necessary to get the rpi up and running properly.
* Assemble WaveShares Game-HAT
* Download the latest RetroPie image to your computer
* Flash the image to the sdcard via etcher / dd / win32diskimager 
  * **(Optional)** Create a ssh file on sdcard/boot to enable the secure shell server
  * **(Optional)** Create a wpa_supplicant.conf within the same directory to enable headless wifi
* Insert the sdcard into the raspberry pi and power it on

### Example for wpa_supplicant.conf
This is an example configuration for the wpa_supplicant application - change it to your needs.
```
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="set ssid here"
    psk="set pre-shared key here"
}
```

## Setup
These steps are required to get the Game-HAT hardware working properly.

### Connect to the raspberry-pi
``ssh pi@<ip-adress> (the default RetroPie-password is "raspberry")``

### Download the drivers from www.gameshare.com
``wget https://www.waveshare.com/w/upload/b/b4/Game-HAT-180720.tar.gz``

### Extract the driver archive
``tar -xvzf Game-HAT-180720.tar.gz``

### Change the current directory to the extracted archive
``cd Game_HAT``

### Execute the installation-script of the driver
``sudo ./Game-HAT``

... and thats it - now you've got a properly working game-hat handheld.
If you're interested in further steps in order to optimize some aspects of the device, follow this guide until the end. 

# Post-Setup
These steps enhance the overall experience of the system.
The previous steps are targeted towards general use, but because im a 
very picky person, I like to modify some things to increase usability, boot- update- and compile-times, etc:

#### Change the default password
``passwd``

#### Expand the filesystem
Launch ``raspi-config`` select ``advanced options`` and ``expand filesystem``

#### Update, upgrade and reboot the system (this will take a while)
``
sudo apt-get update
sudo apt-get upgrade 
sudo reboot
``

# Additional information / resources
 * https://www.waveshare.com/wiki/Game_HAT
 * https://retropie.org.uk/
 * https://emulationstation.org/
