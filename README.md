Spuds
=====

A Teensylu / Printrboard Mashup


##Features

* Small design - board is 100mm x 60mm (4" x 2.4")
* Atmel AT90USB1286 Microcontroller (or AT90USB1287 drop-in compatible for 20mhz support)
 * Native USB interface. No FTDI serial-to-USB chip!
 * 128kb Flash
* Modular Stepper Driver Support (Add/Replace as needed)
* Solder Jumper Microstepping Selection
* Thermistor Connectivity: 2
* N-MOSFETs for Extruder and Heatbed control
 * LED Status Indicators for Power, HBP and Extruder (Troubleshooting, PID Monitoring)
* 2 N-MOSFET for low power Fan or motor
* 6 2-Pin Header 12V Connections for additional features such as LEDs, Cooling Fans, etc
* Onboard SD card slot
* Four Endstop connectors 
 * User selectable via Solder Jumpers 5V or 12v Rails.
 * Includes X, Y, Z, and fourth endstop called E-Stop to be used as an emergency stop, or extruder stop (to be added in firmware).
* Supports multiple power configurations (Carried from Sanguinololu)
 * Logic & Motors supplied by ATX or laptop power supply (12-20V 120W minimum)
 * Logic supplied by USB bus (if enabled by solder jumper)
 * Logic supplied by on-board voltage regulator
 * On-board USB connectivity
* Edge connectors enabling use of vertical or right-angle connections
* 15 Extra pins available for expansion and development, with the following capabilities
 * UART1 (RX and TX)
 * I2C (SDA and SCL)
 * SPI (MOSI, MISO, SCK)
 * PWM pin (2)
 * Analog I/O (6)
 * JTAG (uses some of the ADC pins)
 * Additional 14 pin header with remaining I/O for prototyping
 * SMT Components sized at 0805, and no QFNs for easier soldering.
 * 2-Layer PCB to reduce manufacture cost & complexity

####Revision History
* V0.5 [July 2013]: Internal pre-production design.

####Compatible Firmwares
* Sprinter: http://reprap.org/wiki/Sprinter
* Marlin: No official support yet, but works with Lincomatic's fork (https://github.com/lincomatic/Marlin) or the Unofficial Solidoodle Firmware (https://github.com/mlaws/solidoodle2-marlin)
* Repetier List_of_Firmware#Repetier-Firmware: Supported, use MOTHERBOARD == 8. (https://github.com/repetier/Repetier-Firmware)
* grbl: No official support yet, but works with Lincomatic's fork. (http://blog.lincomatic.com/?p=564)

(Other firmwares are currently untested but any firmware for an arduino mega should work with proper pin setup.)

####Alternate Bootloader
If you have an ISP or JTAG cable, you can also program an alternate bootloader from the LUFA project that allows you to potentially program with the standard Arduino software.
* Download BootloaderCDC.zip
* Unzip to get BootloaderCDC.hex
* Program using your favorite ISP/JTAG cable.
 * The command for avrdude is avrdude -p at90usb1286 -c <your programmer here> -U flash:w:BootloaderCDC.hex
