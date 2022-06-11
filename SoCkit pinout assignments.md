# HSMC GPIO Addon assignments

### HSMC J2 connector 

36 pin new Mister SDRAM module

### HSMC J2 connector prototype area

3 extra pins for old Mister SDRAM/SRAM modules:

pin 57 HSMC_TX _n[8] PIN_D1   SDRAM_CKE
pin 59 HSMC_TX _p[8] PIN_E1    SDRAM_DQMH
pin 58 HSMC_RX _n[8] PIN_E11  SDRAM_DQML



### HSMC J3 connector 

Note: Pin numbers are according to the position on the 2x20 connector

HSMC J3 connector pin 7   JOY1_B2_P9;    HSMC_TX _p[7] PIN_C3  USER_IO[6]  (sega C)
HSMC J3 connector pin 8   JOY1_B1_P6;    HSMC_RX _p[6] PIN_H8  USER_IO[2]  (sega B)
HSMC J3 connector pin 9   JOY1_UP;          HSMC_TX _n[6] PIN_D4  USER_IO[1]
HSMC J3 connector pin 10  JOY1_DOWN;  HSMC_RX _n[5] PIN_H7  USER_IO[0]
HSMC J3 connector pin 13  JOY1_LEFT;      HSMC_TX _p[6] PIN_E4   USER_IO[5]
HSMC J3 connector pin 14  JOY1_RIGHT;   HSMC_RX _p[5] PIN_J7    USER_IO[3]
HSMC J3 connector pin 15  JOYX_SEL_O;   HSMC_TX _n[5] PIN_E2   USER_IO[4]

HSMC J3 connector pin 16 / PMOD3[0];  HSMC_RX _n[4] PIN_K8    SDIO_DAT[3]
HSMC J3 connector pin 17 / PMOD3[1];  HSMC_TX _p[5] PIN_E3    SDIO_CMD
HSMC J3 connector pin 18 / PMOD3[2];  HSMC_RX _p[4] PIN_K7    SDIO_DAT[0]
HSMC J3 connector pin 19 / PMOD3[3];  HSMC_CLKOUT_n1  PIN_E6  SDIO_CLK
HSMC J3 connector pin 20 / PMOD3[4];  HSMC_RX _n[3] PIN_J9          SDIO_DAT[1]
HSMC J3 connector pin 21 / PMOD3[5];  HSMC_CLKOUT_p1  PIN_E7  SDIO_DAT[2]
HSMC J3 connector pin 22 / PMOD3[6];  HSMC_RX _p[3] PIN_J10        SDCD_SPDIF
HSMC J3 connector pin 23 / PMOD3[7];  HSMC_TX _n[4] PIN_C4   -->  not used

HSMC J3 connector pin 24 HSMC_RX _n[2] PIN_F10   AUDIO_SPDIF
HSMC J3 connector pin 25 HSMC_TX _p[4] PIN_D5    AUDIO_L
HSMC J3 connector pin 26 HSMC_RX _p[2] PIN_G10  AUDIO_R

HSMC J3 connector pin 27 HSMC_TX _n[3] PIN_C5   IO_SCL
HSMC J3 connector pin 28 HSMC_RX _n[1] PIN_J12  IO_SDA

HSMC J3 connector pin 31 HSMC_TX _p[3] PIN_D6    LED_USER
HSMC J3 connector pin 32 HSMC_RX _p[1] PIN_K12  LED_HDD
HSMC J3 connector pin 33 HSMC_TX _n[2] PIN_F6     LED_POWER

HSMC J3 connector pin 34 HSMC_RX _n[0]  PIN_G11  BTN_USER
HSMC J3 connector pin 35 HSMC_TX _p[2]  PIN_G7    BTN_OSD
HSMC J3 connector pin 36 HSMC_RX _p[0]  PIN_G12  provision for a future external reset button