# rfxcmd

A forked version of https://github.com/ssjoholm/rfxcmd. The only change made is the addition of installation instructions to this readme. All credit for the actual functionality goes to [Sebastian Sjoholm](https://github.com/ssjoholm)

## Description

RFXcmd is Python script that interfaces the RFX USB devices from RFXcom http://www.rfxcom.com.

~~All documents and other related to RFXcmd can be found at http://www.rfxcmd.eu~~

www.rfxcmd.eu seems to be down, installation instructions for Linux have been added below.

## Requirements

Python 2.7, **does not work with Python 3.x**

----

## Installation: Linux

Details how to install RFXcmd on Linux platform.

### Install Python-serial

To be able to communicate with the RFXCom the serial library needs to be installed.

    $ apt-get install python-serial

### Clone the RFXcmd repo

To your home directory or wherever you fancy (original docs put it in `/opt/rfxcmd`)

    $ git clone https://github.com/digiltd/rfxcmd.git

### Find the RFXcom device

Check your RFXcom that it is installed and visible in the usb printout with 'lsusb'

    $ lsusb

You should see a line with following data

    ID 0403:6001 Future Technology Devices International, Ltd FT232 USB-Serial (UART) IC

This indicates that the RFXcom is available on the system.

There are probably many ways to find the device name, here is one that is at least working on Raspberry Pi running Raspbian.

Looking for the idVendor in dmesg printout will show the usb info

    $ dmesg |grep idVendor=0403
    [508669.109221] usb 1-1.3: New USB device found, idVendor=0403, idProduct=6001
    $

Then using the usb connector info "1-1.3″ (though yours will probably be different) we can find which device it has connected to.

    $ dmesg |grep '1-1.3'
    [508668.984325] usb 1-1.3: new full-speed USB device number 4 using dwc_otg
    [508669.109221] usb 1-1.3: New USB device found, idVendor=0403, idProduct=6001
    [508669.109258] usb 1-1.3: New USB device strings: Mfr=1, Product=2, SerialNumber=3
    [508669.109273] usb 1-1.3: Product: RFXtrx433
    [508669.109287] usb 1-1.3: Manufacturer: RFXCOM
    [508669.109300] usb 1-1.3: SerialNumber: 03VHG0NE
    [508669.198095] ftdi_sio 1-1.3:1.0: FTDI USB Serial Device converter detected
    [508669.198639] usb 1-1.3: Detected FT232RL
    [508669.198670] usb 1-1.3: Number of endpoints 2
    [508669.198688] usb 1-1.3: Endpoint 1 MaxPacketSize 64
    [508669.198704] usb 1-1.3: Endpoint 2 MaxPacketSize 64
    [508669.198718] usb 1-1.3: Setting MaxPacketSize 64
    [508669.200145] usb 1-1.3: FTDI USB Serial Device converter now attached to ttyUSB0
    $

And at the end of the printout we can see that it is attached to the "ttyUSB0″. To make it statically always connected to the same device (in case additional USB devices are connected) the UDEV needs to be used.

### Ready to run

If the RFXCom device is on /dev/ttyUSB0, then you can easily test that it is working with following command that will show the status of the RFXCom device.

    $ ./rfxcmd.py -d /dev/ttyUSB0 -f -v

If you receive the status printout and list of all protocols, you can try to listen to incoming sensors.

    $ ./rfxcmd.py -d /dev/ttyUSB0 -l -v

To use RFXcmd with all options and features you need to use the config.xml file to configure. But the basic functionality can be tested with the command above.

----

## Thanks

Thanks to following users who have helped with testing, patches, ideas, bug reports, and so on (in no special order). Anders, Dimitri, Patrik, Ludwig, Jean-Michel, Jean-Baptiste, Robert, Fabien, Bert, George, Jean-Francois, Mark, Frederic, Matthew, Arno, Jean-Louis, Christophe, Fredrik, Neil, Pierre-Yves and to RFXCOM for their support.

## Notes

RFXCOM is a Trademark of RFSmartLink.

## Copyright

Copyright (C) 2012-2015 Sebastian Sjoholm. This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version. This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program. If not, see <http://www.gnu.org/licenses/>.
