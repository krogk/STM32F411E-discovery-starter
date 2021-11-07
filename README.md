# STM32F411E-discovery-starter

Starter Project for STM32F411E discovery Board & Devlopment guidelines for Linux OS

# Prerequisites

1. Download [GNU Arm Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
2. Download, Install [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) and use it to download STM32F411E Board Firmware Package 
4. Download [stlink](https://github.com/stlink-org/stlink)
5. Build the stlink by using make
```
sudo make
```
5. Then create the paths to the compiler and stlink to make these avaiable. This is done by edditing the bashrc file in your home folder
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
6.Update your shell environment
```
source .bashrc
```
Now you should be able to use & stlink
```
arm-none-eabi-gcc --version
st-info --version
```
Notes: I've encountered an error preventing the use of st-info when the stlink was built without sudo command.
