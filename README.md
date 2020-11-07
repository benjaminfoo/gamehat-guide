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

### Download the drivers from www.waveshare.com
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
The previous steps are targeted towards increased usability, boot- update- and compile-times, etc:

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

### mount usb-drive 
Open fstab file using ```sudo nano /etc/fstab``` - append the following line:
```/dev/sda1 /media/usb1 auto defaults 0 0```

### Log in to emulationstation on boot 
In retropie setup script > Configuration / tools > autostart > Start EmulationStation at Boot

### Install famicon-mini-theme
In retropie setup script > Configuration / tools > esthemes > Install ruckage/famicom-mini

### Install xfce desktop-environment
sudo apt-get install --no-install-recommends xserver-xorg
sudo apt-get install --no-install-recommends xinit
sudo apt-get install xfce4 xfce4-terminal

### FAQ: Where are emulationstation-themes stored?
The themes are stored in: /etc/emulationstation/themes/

# Performance
## Analyze bootup performance
systemd-analyze blame

## Disable bluetooth
* sudo nano /boot/config.txt
* add "dtoverlay=pi3-disable-bt" to the bottom of the file
* add "dtoverlay=disable-bt" for newer versions
* save and close your editor of choice

## Disable bluetooth services
- sudo systemctl disable hciuart.service
- sudo systemctl disable bluealsa.service
- sudo systemctl disable bluetooth.service

## Disable samba / netbios daemon
- sudo systemctl stop smbd
- sudo systemctl disable smbd
- sudo systemctl stop nmbd
- sudo systemctl disable nmbd



# Additional information / resources
 * https://www.waveshare.com/wiki/Game_HAT
 * https://retropie.org.uk/
 * https://emulationstation.org/
 * https://scribles.net/disabling-bluetooth-on-raspberry-pi/
