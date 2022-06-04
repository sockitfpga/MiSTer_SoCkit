# MiSTer port

### Building the SD card and running Mister on SoCKit board

Follow general instructions from Main MiSTer port site https://github.com/MiSTer-Arrow-SoCKit/Main_MiSTer/wiki except for the following points:

step 4) Download SD-Installer-Win64_MiSTer latest release and install to the SD Card

If you are using Linux, use this installer [script]( ./MiSTerSD-linux.sh ) instead of the .exe file. 

`sudo ./MiSTerSD-linux.sh sdX    `     where sdX is your sdcard device

In this step do not update the menu.rbf as it did not work for me. You can update the MiSTer binary.

step 5) Recommended Arrow SoCKit MiSTer.ini worked fine for me

step 6)  do not update the menu.rbf as it did not work for me



### List of cores working with and without SDRAM expansion
![](./Sockit-Mister-cores.png)



### Useful links regarding the MiSTer port:

* Main MiSTer port site https://github.com/MiSTer-Arrow-SoCKit/Main_MiSTer/wiki 
* Mister SDRAM expansion http://modernhackers.com/128mb-sdram-board-on-de10-standard-de1-soc-and-arrow-sockit-fpga-sdram-riser/

* Info about the port http://modernhackers.com/porting-mister-to-arrow-sockit-fpga/

* Comparison of ported cores between platforms http://modernhackers.com/mister/

* ao486 core for https://github.com/MiSTer-Arrow-SoCKit/ao486_MiSTer

