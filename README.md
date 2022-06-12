# Linux script to build a MiSTer SDcard for Arrow SoCkit FPGA

Adapted from https://github.com/michaelshmitty/SD-Installer-macos_MiSTer

* Execute the script [MiSTer-sd-installer-linux.sh](MiSTer-sd-installer-linux.sh) to build the MiSTer SD

* Copy MiSTer.ini to the root folder of SD card

* Copy the rbf cores to SD card (like template core mycore.rbf)

See [old_firmware/](old_firmware/) folder for ModernHackers port (old firmware/framework).



# SoCkit switches / buttons / leds

**Switches:** 

* Default position is all switches pointing towards outside the board
  * 0 means switch position towards outside of the board
  * 1 means switch position towards inside of the board

- SW0: Audio pins output selection
  - 0 Audio Sigma-Delta and SPDIF pins output 
  - 1 I2S output though the  sigma delta and SPDIF audio pins 
- SW1: 
  - 0  MIDI I2S input enabled. All User IO pins enabled for input. 
  - 1  three User IO pins are disabled as inputs.
- SW2: Not used.
- SW3: Switch has no effect in SoCkit. Internally is wired to 0 in the cores as it is necessary for VGA output mode.
  - SW3=1 is used in DE10-nano for MiSTer dual SDRAM mode and disables functions of analog IO board (VGA, SD card, Sigma/Delta audio, SPDIF audio, Leds)

**Keys:**

- KEY 0 = OSD   button
- KEY 1 = USER  button

- KEY 4 = RESET button

**Leds:**

- LED 0 = USER led

- LED 1 = HDD led

- LED 2 = POWER led

- LED 3 = LOCKED led




# SoCkit HSMC GPIO addon assignments

Read the [HSMC_GPIO_pinout_assignments.md](HSMC_GPIO_pinout_assignments.md).



# Porting cores to SoCkit

Check this [COMMIT](https://github.com/sockitfpga/Template_SoCkit/commit/c349aa28e03251e3225126e6f79496f1b9eeb9d7) changes.

This [guide](Portando_a_SoCkit.md) is also available in Spanish (necesita actualización a la nueva Template).

Core template with needed changes for Sockit: https://github.com/sockitfpga/Template_SoCkit
