Spuds
=====
**A Teensylu / Printrboard Mashup**
![Spuds-Board](/Images/Spuds-v0.6-Board.png)
Spuds was born from mashing together the concepts of both the Teensylu and Printrboard (itself a development of the Teensylu concept). The aim was to take the positives provided by the Printrboard design and incorporate some additions such as LED indicators on the MOSFETs, an additional PWM Fan header and an extra PWM Output header pin. It then reintroduced the modular Stepper Driver setup, as for many, the onboard Allegro drivers of the Printrboard are seen as a drawback as it limits options and replacement/repair. 

Spuds has expansion headers supporting I2C, SPI, UART, and ADC pins. All extra I/O ports of the AT90USB have been broken out to headers for prototyping and expansion. It follows the footprint for headers that the Printrboard introduced to allow compatibility with other expansions devices such as LCD's and the Extrudr board. 

The continued use of the AT90USB1286 used in the Teensylu and Printrboard means Spuds also has on-chip USB, removing the need for the FTDI UART (USB-to-serial) IC. On-chip USB means dramatically faster firmware upload times and communication. The AT90USB connects at any baud rate regardless of firmware configuration, and operates virtually free of serial communication errors/pauses.

This board is currently in pre-release design phases, so is subject to changes!

**Licence: _CC ShareAlike 3.0_**

**Attributions:**
* **_Teensylu_** (StephS 2011) http://reprap.org/wiki/Teensylu
* **_Printrboard_** (Laine Walker-Avina 2012) http://reprap.org/wiki/Printrboard

##Features
* Small design - board is 100mm x 60mm (4" x 2.4")
* Atmel AT90USB1286 Microcontroller (or AT90USB1287 drop-in compatible for 20mhz support)
 * Native USB interface. No FTDI serial-to-USB chip.
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

![Spuds-Schematic](/Images/Spuds-v0.6-Schematic.png)

####Benefits of this Design
* Allows modular use of Stepper Drivers, allowing:
 * User selection of driver used
 * The re-use of existing drivers
 * Replacement due to fault/failure.

* Integrated USB controller provides 12MBps bandwidth, instead of usual slower serial comms via FTDI. Result: Virtually no serial communication errors and interruptions due to PC Activity reduced.
* Integrated micro-SD Card slot
* Uses small standard Molex connectors for motors, heater, and endstops.

####Bill of Materials
Available via [GoogleDocs](https://docs.google.com/spreadsheet/ccc?key=0ArIeeziM0bp9dG5TbjlYaFVDQ0I5dkZXbHk2VjhtQlE&usp=sharing)

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

###Setup
####Stepper Motors
Connect the X, Y, Z axis, and extruder motors to the matching headers at the top of the Printrboard (X-MOT, Y-MOT, Z-MOT, E-MOT). Headers are 4 wire Molex KK series, part# 0022013047) with 2759 series crimp terminals, part# 0008550101. Motor pinout is:
1. A - Phase 1+
2. B - Phase 1-
3. C - Phase 2+
4. D - Phase 2-

####Endstops
Connect mechanical microswitches to the 3-pin Molex headers X-STOP, Y-STOP, Z-STOP at the bottom of the board. E-STOP is reserved for future use. Connect switches as follows:
#####Standard Microswitches
1. Switch NC
2. No connection
3. Switch COMMON

#####For optos:
1. Signal Output
2. +5V or +12V
3. GND

####Heaters
* LEDs are fitted to indicate when the MOSFET is active. These can be ommitted if desired. 
* Connect the heating element of your hotend (resistor or nichrome wire) to the 4-pin EXTRUDER header, positioned next to MOSFET Q1. 
* Connect your heatbed to the HOTBED header, next to MOSFET Q2. Polarity here is unimportant; pinout is as follows:

1. Positive
2. Positive
3. Negative
4. Negative

####Thermistors
Thermistor headers are 2-pin Molex headers at the right side of the board, located above the reset button.
* Connect the HBP thermistor to the header directly above the reset button. 
* The Extruder thermistor also connects above the reset button next to the HBP thermistor.

####Low Power Fan
A 2-pin Molex header labelled FAN is located on the right side of the board, above the thermistor headers. 
* This optional header can be used to power a fan or other small motor.

####Board Power
All power is supplied through a choice of connector at the upper left corner of the Spuds, labelled PWR:
* 4-pin ATX style header (Suitable for high current HBP)
* 5.08mm 2-Pin Screw Terminal (Suitable for low current HBP only)

Connect directly to any 12VDC power supply. 
* Ground terminals are closest to the edge of the board
* 12VDC+ terminals are located behind.

####USB
Choice of USB Connector (only one can be installed). The Type-B connector is a good choice for long cable runs, as you can easily acquire heavily sheilded thick gauge USB cables as used for Printers. Micro-USB is perhaps a good choice if a small compact connection is required, or for interconnection to another controller system such as a tablet or RPi:
* Micro-USB B Connector
* Type-B USB Connector

**Note that a jumper should _NOT_ be installed on the "BOOT" pins for normal operation (see _Bootloaders_ ).**
