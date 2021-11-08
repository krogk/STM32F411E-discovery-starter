# STM32F411E-discovery-starter

Starter Project for STM32F411E discovery Board & Devlopment setup guide for Linux OS.

# Prerequisites

How do I develop for the STM32F411E discovery board on Linux? Well it is quite simple. 

1. Download & Extract [GNU Arm Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
2. Download, Install [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) and use it to download STM32F411E Board Firmware Package 
3. Download [stlink](https://github.com/stlink-org/stlink)
4. Build the stlink by using make
```
sudo make
```
5. Then create the global paths to the compiler & stlink to make these avaiable for use everywhere. This is done by editing the bashrc file in your home folder
```
sudo nano .bashrc
```
and adding the following lines at the end of the file
```
#GCC ARM Bin Path
export PATH=$PATH:path-to-toolchain-folder/bin

#St-link path
export PATH=$PATH:path-to-stlink-folder/build/Release/bin
```
Update your shell environment
```
source .bashrc
```
Now you should be able to use gcc compiler for arm & stlink:
```
arm-none-eabi-gcc --version
st-info --version
```
Note: I've encountered an error preventing the use of st-info when the stlink was built without sudo command.

6. Use st-info to probe for the board programmer:
```
st-info --probe
```
Note: If the st-info cannot find the st programmer, check if your OS detects the board.
On linux - ubuntu:
```
lsusb
```
If the OS cannot find the board it might be due to board damage or you might be using a power only USB cable.

Note: If you get an access error then you most likley need to allow users access to USB devices. Create a new udev rule by creating a file /etc/udev/rules/45-usb-stlink-v2.rules, make sure the number preceeding the rules filename is unique. 
```
sudo nano /etc/udev/rules/45-usb-stlink-v2.rules
```
Then add the following contents: 
```
#FT232
ATTRS{idProduct}=="6014", ATTRS{idVendor}=="0403", MODE="666", GROUP="plugdev"

#FT2232
ATTRS{idProduct}=="6010", ATTRS{idVendor}=="0403", MODE="666", GROUP="plugdev"

#FT230X
ATTRS{idProduct}=="6015", ATTRS{idVendor}=="0403", MODE="666", GROUP="plugdev"

#STLINK V1
ATTRS{idProduct}=="3744", ATTRS{idVendor}=="0483", MODE="666", GROUP="plugdev"

#STLINK V2
ATTRS{idProduct}=="3748", ATTRS{idVendor}=="0483", MODE="666", GROUP="plugdev"
```
Save & reboot your system, or you can try restarting udev service by

```
sudo service udev restart
```
then unplug and plug back in your board.

# STM32CubeMX Code generation

The Drivers, Core and CubeMX folder contents in this repository have been generated using STM32CubeMX software, it is reccomended to genereate your own code and replace these folders, use Makefile for toolchain/ IDE option. The folder contents of the CubeMX contains the starup, linker scripts and the makefile which are in the root folder of the CubeMX generated project. The other two folders are directly copied.

# Configuration

In the main CMakeLists.txt you should:
1. Set the project name
2. Set the MCU family and model
3. Set CPU parameters

# About

