# Como portar cores MiSTer de DE10-nano a SoCkit



## Ejemplo de commit con los cambios realizados para portar el core de Minimig de MiSTer de DE10-nano a SoCkit:

https://github.com/sockitfpga/Minimig-AGA_SoCkit/commit/7d8dc81285769225788ccfd990858f4c1b4fee2c



## Pasos a realizar para  portar cores de MiSTer de DE10-nano a SoCkit

* Clonar el repositorio del core  MiSTer de https://github.com/MiSTer-devel/

  * Opcionalmente bajar el zip del repositorio (CODE > download zip) 

* Borrar del directorio releases/ todos los archivos xxxxxxx.rbf

* Editar el **fichero .qsf del directorio principal** del core (por ejemplo Minimig.qsf)

  ```tcl
  #reemplazar estas líneas
  set_global_assignment -name MIN_CORE_JUNCTION_TEMP "-40"
  set_global_assignment -name MAX_CORE_JUNCTION_TEMP 100
  
  #por estas otras
  set_global_assignment -name MIN_CORE_JUNCTION_TEMP 0
  set_global_assignment -name MAX_CORE_JUNCTION_TEMP 85
  ```

  

  ```tcl
  #añadir las siguientes líneas hacia el final después de "source files.qip"
  
  set_global_assignment -name VERILOG_FILE sys/I2C_Controller.v
  set_global_assignment -name VERILOG_FILE sys/I2C_AV_Config.v
  
  set_global_assignment -name ENABLE_OCT_DONE OFF
  set_global_assignment -name STRATIXV_CONFIGURATION_SCHEME "PASSIVE SERIAL"
  set_global_assignment -name USE_CONFIGURATION_DEVICE ON
  set_global_assignment -name CRC_ERROR_OPEN_DRAIN ON
  set_global_assignment -name OUTPUT_IO_TIMING_NEAR_END_VMEAS "HALF VCCIO" -rise
  set_global_assignment -name OUTPUT_IO_TIMING_NEAR_END_VMEAS "HALF VCCIO" -fall
  set_global_assignment -name OUTPUT_IO_TIMING_FAR_END_VMEAS "HALF SIGNAL SWING" -rise
  set_global_assignment -name OUTPUT_IO_TIMING_FAR_END_VMEAS "HALF SIGNAL SWING" -fall
  set_global_assignment -name ACTIVE_SERIAL_CLOCK FREQ_100MHZ
  ```

  

En los siguientes pasos puedes tomar los ficheros indicados del core Template https://github.com/sockitfpga/Template_SoCkit/tree/master/sys

* Añadir los siguientes ficheros en la carpeta sys/

  * **sys/I2C_AV_Config.v**
  * **sys/I2C_Controller.v**

* Sobrescribir los siguientes ficheros de la carpeta sys/

  * **sys/sys.tcl**
  * **sys/sys_analog.tcl**
  * **sys/sys_dual_sdram.tcl**

  Nota: Personalmente sigo comparando estos ficheros antes de sobrescribirlos por si hubiera alguna cosa especial, pero en la mayoría de casos se pueden sobrescribir sin problemas.

* Editar el fichero **sys/sys_top.v** de  la carpeta sys/

  Como ejemplo de los cambios a realizar puedes revisar este [commit](https://github.com/sockitfpga/Minimig-AGA_SoCkit/commit/7d8dc81285769225788ccfd990858f4c1b4fee2c#diff-13d67b12937a9342f615921495251467cd222055cd33b8728f0449fd1b070d1f)

  En resumen solo hay que modificar 3 zonas de este extenso fichero.

  * Zona inicial de definición de ports del module sys_top

    ```verilog
    # Modificar los siguientes puertos del módulo sys_top
    
    	//////////// VGA ///////////
    # Donde ponga un 5 modificarlo por un 7 ( [5:0]  pasa a  [7:0] )
    	//DE10-nano board implementation contained 6 / color
    	//output  [5:0] VGA_R,
    	//output  [5:0] VGA_G,
    	//output  [5:0] VGA_B,
    	//SoCkit, DE10-standard, DE1-SoC implementation need to contain 8 bit color otherwise the brightness is low on the DAC
    	output  [7:0] VGA_R,
    	output  [7:0] VGA_G,
    	output  [7:0] VGA_B,
    # Comentar la línia siguiente 
    	//input      VGA_EN,  // active low
    # Añadir a continuación las nuevas señales para SoCkit
    	//SoCkit, DE10-standard, DE1-SoC implementation for on-board VGA DAC route - additional pins
    	output 		  VGA_CLK,
    	output 		  VGA_BLANK_N,
    	output 		  VGA_SYNC_N,
    
    # Añadir en la sección de ports de AUDIO las nuevas señales para SoCkit
    	/////////// AUDIO //////////
    	//SoCkit, DE10-standard, DE1-SoC implementation for on-board Audio CODEC
    	// Audio CODEC
    	inout wire    AUD_ADCLRCK,  // Audio CODEC ADC LR Clock
    	input wire    AUD_ADCDAT,   // Audio CODEC ADC Data
    	inout wire    AUD_DACLRCK,  // Audio CODEC DAC LR Clock
    	output wire   AUD_DACDAT,   // Audio CODEC DAC Data
        inout wire    AUD_BCLK,     // Audio CODEC Bit-Stream Clock
        output wire   AUD_XCK,      // Audio CODEC Chip Clock
        output wire   AUD_MUTE,		// Audio CODEC Mute (active low)
    
    	// I2C Audio CODEC
        inout wire    AUD_I2C_SDAT,     // I2C Data
        output wire   AUD_I2C_SCLK,     // I2C Clock
    
    # Modificar la sección MB SWITCH según lo descrito
    	////////// MB SWITCH ////////
    	//SoCkit, DE10-standard, DE1-SoC board implementation
    	//input   [3:0] SW,
    	inout   [3:0] SW,				
    
    # Modificar la sección MB LED según lo descrito
    	////////// MB LED ///////////
    	//output  [7:0] LED
    	output LED0
    ```

    

    ```verilog
    # Comentar los ports no utilizados 
        //////////// HDMI //////////
        // output        HDMI_I2C_SCL,
    	// inout         HDMI_I2C_SDA,
    	// output        HDMI_MCLK,
    	// output        HDMI_SCLK,
    	// output        HDMI_LRCLK,
    	// output        HDMI_I2S,
    	// output        HDMI_TX_CLK,
    	// output        HDMI_TX_DE,
    	// output [23:0] HDMI_TX_D,
    	// output        HDMI_TX_HS,
    	// output        HDMI_TX_VS,
    	// input         HDMI_TX_INT,
    
    	//////////// VGA ///////////
    	//input      VGA_EN,  // active low
    
    	/////////// AUDIO //////////
    	// output		  AUDIO_L,
    	// output		  AUDIO_R,
    	// output		  AUDIO_SPDIF,
    
    	//////////// SDIO ///////////
    	// inout   [3:0] SDIO_DAT,
    	// inout         SDIO_CMD,
    	// output        SDIO_CLK,
    
    	////////// I/O ALT /////////
    	// output        SD_SPI_CS,
    	// input         SD_SPI_MISO,
    	// output        SD_SPI_CLK,
    	// output        SD_SPI_MOSI,
    
    	// inout         SDCD_SPDIF,
    	// output        IO_SCL,
    	// inout         IO_SDA,
    
    	////////// ADC //////////////
    	// output        ADC_SCK,
    	// input         ADC_SDO,
    	// output        ADC_SDI,
    	// output        ADC_CONVST,
    
    	///////// USER IO ///////////
    	//inout   [6:0] USER_IO
    ```

    Añadir lo siguiente justo después del final de la definición de ports de sys_top  (después de la línea que pone ""**;)**"" aprox. línea 155 )

    ```verilog
    // DE10-Standard / DE1-SoC / Arrow SoCKit VGA mode
    assign SW[3] = 1'b0;		//necessary for VGA mode
    
    // DE10-Standard / DE1-SoC / SoCKit implementation for on-board VGA DAC route - this will be overrided by code to set value to 0
    wire   VGA_EN;  // active low
    assign VGA_EN = 1'b0;		//enable VGA mode when VGA_EN is low
    
    wire        HDMI_TX_CLK;
    wire        HDMI_TX_DE;
    wire [23:0] HDMI_TX_D;
    wire        HDMI_TX_HS;
    wire        HDMI_TX_VS;
    wire        HDMI_TX_INT;
    wire        HDMI_I2C_SCL;
    wire        HDMI_I2C_SDA;
    wire        HDMI_MCLK;
    wire        HDMI_SCLK;
    wire        HDMI_LRCLK;
    wire        HDMI_I2S;
    
    wire        ADC_SCK;
    wire        ADC_SDO;
    wire        ADC_SDI;
    wire        ADC_CONVST;
    
    wire		AUDIO_L;
    wire		AUDIO_R;
    wire		AUDIO_SPDIF;
    
    wire        SD_SPI_CS;
    wire        SD_SPI_MISO;
    wire        SD_SPI_CLK;
    wire        SD_SPI_MOSI;
    
    wire        SDCD_SPDIF;
    wire        IO_SCL;
    wire        IO_SDA;
    
    wire   [3:0] SDIO_DAT;
    wire         SDIO_CMD;
    wire         SDIO_CLK;
    
    wire   [6:0] USER_IO;
    
    wire   [7:0] LED;
    
    assign LED0 = LED[0];
    
    ```

    

  * Zona asignaciones VGA hacia el final del documento (sobre la línia 1410, puede variar según la versión de framework)

    ```verilog
    #modificar las siguientes líneas de ejemplo pero solo lo expresamente indicado a continuación
    #donde ponga 6'bZZZZZZ  modificar por  8'bZZZZZZZZ
    #donde ponga [23:18] modificar por [23:16]
    #donde ponga [15:10] modificar por [15:8]
    #donde ponga [7:2] modificar por [7:0]
    
    #Ejemplo. Estas líneas del core original de MiSTer
    
    assign VGA_R  = (VGA_EN | SW[3]) ? 6'bZZZZZZ :   (vga_fb | vga_scaler) ? vgas_o[23:18] : vga_o[23:18];
    	assign VGA_G  = (VGA_EN | SW[3]) ? 6'bZZZZZZ :   (vga_fb | vga_scaler) ? vgas_o[15:10] : vga_o[15:10];
    	assign VGA_B  = (VGA_EN | SW[3]) ? 6'bZZZZZZ :   (vga_fb | vga_scaler) ? vgas_o[7:2]   : vga_o[7:2]  ;
    
    #cambian a lo siguiente para el port de SoCkit
    
    	//DE10-standard / DE1-SoC / SoCkit implementation for on-board VGA DAC route - additional 2 bit per color
    	assign VGA_R  = (VGA_EN | SW[3]) ? 8'bZZZZZZZZ :   (vga_fb | vga_scaler) ? vgas_o[23:16] : vga_o[23:16];
    	assign VGA_G  = (VGA_EN | SW[3]) ? 8'bZZZZZZZZ :   (vga_fb | vga_scaler) ? vgas_o[15:8]  : vga_o[15:8] ;
    	assign VGA_B  = (VGA_EN | SW[3]) ? 8'bZZZZZZZZ :   (vga_fb | vga_scaler) ? vgas_o[7:0]   : vga_o[7:0]  ;
    
    #Añadir las siguientes líneas a continuación
    
    	//DE10-standard / DE1-SoC / SoCkit implementation for on-board VGA DAC route - additional pins
    	assign VGA_BLANK_N = VGA_HS && VGA_VS;  //VGA DAC additional required pin
    	assign VGA_SYNC_N = 0; 					//VGA DAC additional required pin
    	assign VGA_CLK = HDMI_TX_CLK; 			//has to define a clock to VGA DAC clock otherwise
    ```

    

  * Zona Audio

    ```verilog
    # Añadir las siguientes líneas antes de la sección  User I/O (USB 3.0 connector) situada hacia el final del archivo (sobre la línia 1550, puede variar según la versión de framework)
    
    //// DE10-Standard / DE1-SoC / SoCkit Audio CODEC
    
    assign AUD_MUTE    = 1'b1;
    assign AUD_XCK     = HDMI_MCLK;
    assign AUD_DACLRCK = HDMI_LRCLK;
    assign AUD_BCLK    = HDMI_SCLK;
    assign AUD_DACDAT  = HDMI_I2S;
    
    // I2C audio config
    I2C_AV_Config audio_config (
      // host side
      .iCLK         (clk_audio        ),
      .iRST_N       (!reset           ),
      // i2c side
      .oI2C_SCLK    (AUD_I2C_SCLK         ),
      .oI2C_SDAT    (AUD_I2C_SDAT         )
    );
    ```

    





