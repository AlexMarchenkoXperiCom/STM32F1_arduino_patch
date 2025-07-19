# STM32F1_arduino_patch
Changes to the STM32F1 Arduino Studio library package to fix some bugs in OLED and Wire libs.

A location of the installed Arduino libraries, typical for the Windows 10(11):
    - Users\....\AppData\Local\Arduino\packages\stm32duino

Note: the package version and path - can be different, pay attention to that.


Changes to the STM32F1 library package:

1. OLED_I2C:
   - A TWI burst mode has been fixed;
   - Added definitions to choose the physical size of the display, see OLED_128x32, OLED_128x64.
   Arduino Studio parses the libraries first and if OLED_128x32 will be defined in your .ino - 
   compiler hangs with the error. Thus the size of the OLED temporarily defined inside OLED_I2C.h;
   - Removed static declaration of the TwoWire instance.

2. Wire:
   - Added handlers to simplify TWI buffer control;
   - Added factory method to construct the TwoWire instance at runtime, see Wire.setup();
   - Fixed bugs in work with the primary remapped TWI - "I2C2";
   - Changed IDs of TWI ports: primary - SDA0/SCL0, primary remapped - SDA1/SCL1, secondary - SDA2/SCL2;
   - Something was fixed in the SW implementation of TWI.


Installation:
   - enter the STM32F1 library package location;
   - compare target files with the patched ones;
   - resolve all diffs, or overwrite them.


Example:
   - Code example shows the work with 128x32 OLED (SED1306 based) connected to the primary redirected TWI port (PB8, PB9).


Known issues:
   - Secondary TWI still not works (SDA2/SCL2), use SW implementation instead.
