# SoCkit MiSTer

## Linux script to build a MiSTer SDcard for Arrow SoCkit FPGA

Adapted from https://github.com/michaelshmitty/SD-Installer-macos_MiSTer

* Execute the script [MiSTer-sd-installer-linux.sh](MiSTer-sd-installer-linux.sh) to build the MiSTer SD

* Copy MiSTer.ini to the root folder of SD card

* Copy the rbf cores to SD card (like template core mycore.rbf)

See [old_firmware/](old_firmware/) folder for ModernHackers port (old firmware/framework).



## SoCkit Switches / Buttons / Leds

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

-  available in SpanishLED 0 = USER led

- LED 1 = HDD led

- LED 2 = POWER led

- LED 3 = LOCKED led




## SoCkit HSMC GPIO addon assignments

Read the [HSMC_GPIO_pinout_assignments.md](HSMC_GPIO_pinout_assignments.md).



## Porting cores to SoCkit

Check this [COMMIT](https://github.com/sockitfpga/Template_SoCkit/commit/c349aa28e03251e3225126e6f79496f1b9eeb9d7) changes.    This [guide](Portando_a_SoCkit.md) is available in Spanish .

Core template with needed changes for Sockit: https://github.com/sockitfpga/Template_SoCkit

New files (green) and changed files (orange):

![port_files](port_files.png)



## Guia para portar cores de MiSTer a SoCkit

*  [Guía de portado de cores MiSTer a SoCkit](Portando_a_SoCkit.md).

  

## Pasos en GitHub para portar un core

- Busco el core a portar en  https://github.com/orgs/MiSTer-devel/repositories 

- Forkeo el core de MiSTer desde la web del repopisotorio en mi GitHub personal

- Clono el fork en mi ordenador: `git clone ssh://url`   

- Borro los rbf de la carpeta releases (dejo el resto de ficheros como rom y mra)

- Porto el core según el último commit de Template. 

  - Personalmente uso el programa Meld para comparar todos los ficheros del core Template versus los del core a portar

- Modifico el archivo README.md del core

- Sintetizo en Quartus y testeo el rbf

- Pongo el rbf en la carpeta releases/  con la fecha de creación (ejemplo core_20220702.rbf)

- Cierro Quartus y limpio los ficheros inútiles que genera Quartus con el script clean.bat / clean.sh

- Subo a GitHub:

  ```sh
  #antes de subir a GitHub comprobar los archivos que han cambiado y las diferencias
  git status
  git diff
  #subir archivos
  git add .
  git commit -am "Sockit port"
  git push
  ```

  
