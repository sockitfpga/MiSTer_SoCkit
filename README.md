# Linux script to build a MiSTer SDcard for Arrow SoCkit FPGA

Adapted from https://github.com/michaelshmitty/SD-Installer-macos_MiSTer

* Execute the script [MiSTer-sd-installer-linux.sh](MiSTer-sd-installer-linux.sh) to build the MiSTer SD

* Copy MiSTer.ini to the root folder of SD card

* Copy the rbf cores to SD card (like template core mycore.rbf)

See [old_firmware/](old_firmware/) folder for ModernHackers port (old firmware/framework).



# SoCkit buttons / leds

KEY 0 = OSD   button

KEY 1 = USER  button

KEY 4 = RESET button

LED 0 = USER led

LED 1 = HDD led

LED 2 = POWER led

LED 3 = LOCKED led



# SoCkit HSMC GPIO addon assignments

Read the [HSMC GPIO pinout assignments.md document](HSMC GPIO pinout assignments.md).



# Porting cores to SoCkit

Check this [commit](https://github.com/sockitfpga/Minimig-AGA_SoCkit/commit/7d8dc81285769225788ccfd990858f4c1b4fee2c) changes.

This [guide](Portando_a_SoCkit.md) is also available in Spanish.

Core template with needed changes for Sockit: https://github.com/sockitfpga/Template_SoCkit
