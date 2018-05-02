# CANopenNode PIC32 Flash driver

This is a small extension of https://github.com/CANopenNode/CANopenNode which provides an excellent CANopen stack.
These files should provide an extension to the PIC32 device drivers. CANopenNode comes with PIC32 drivers and EEPROM drivers. Users who would like to use PIC32MX with CANopenNode and store CO_OD_ROM in the program flash memory of the PIC32 may find this useful. The files CO_Flash.c/h are based on the SAM3X flash drivers written by Olof Larsson

# Use
Set up your project e.g. the PIC32 Explorer16 development board example of CANopenPIC.
Include CO_Flash.h in your PIC32 CO_Driver.h and include CO_Flash.h in you main.c

Adjust your NVM_STARTADDRESS and BYTE_PAGE_SIZE according to your memory layout and target device. 

Adjust the default linker script procdefs.ld to reserve 2 memory pages (this example uses the last two program memory pages). The default linker script is located at e.g. (..\xc32\v1.44\pic32mx\pic32mx\lib\proc\32MXGENERIC\). Copy the default linker script to your project folder and adjust it, then right click in the MPLABX Projects Tree on the Linker Files folder and "add existing".
Copy the file elf32pic32mx.x from  ..\xc32\v1.44\pic32mx\lib\ldscripts\ to your project folder and also include it as existing linker file as described before.

Insert the function CO_FlashInit(); in the initialization section of main.c
Insert the function CO_FlashRegisterODFunctions(CO); after e.g. CO_init(ADDR_CAN1, nodeId, CANBitRate); in main.c

Make sure to set your Programmer/Debugger to preserve the memory region where the parameters are stored. (Project Properties->Your Configuration->Your Programmer/Debugger->Memories to Program - Preserve Program Memory Range(s)(hex))
One page is for the default parameter set and the second page is for the runtime parameter set a user may want to save to the flash. At bootup if the data is valid the runtime parameter set of type CO_OD_ROM is loaded.

License
-------
CANopenNode is distributed under the terms of the GNU General Public
License version 2 with the classpath exception.

CANopenNode is free and open source software: you can redistribute
it and/or modify it under the terms of the GNU General Public License
as published by the Free Software Foundation, either version 2 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see http://www.gnu.org/licenses/.

### GPL linking exception
CANopenNode can be easely used also in commercial embedded projects.
Following clarification and special
[linking exception to the GNU General Public License](https://en.wikipedia.org/wiki/GPL_linking_exception)
is included to the distribution terms of CANopenNode:

Linking this library statically or dynamically with other modules is
making a combined work based on this library. Thus, the terms and
conditions of the GNU General Public License cover the whole combination.

As a special exception, the copyright holders of this library give
you permission to link this library with independent modules to
produce an executable, regardless of the license terms of these
independent modules, and to copy and distribute the resulting
executable under terms of your choice, provided that you also meet,
for each linked independent module, the terms and conditions of the
license of that module. An independent module is a module which is
not derived from or based on this library. If you modify this
library, you may extend this exception to your version of the
library, but you are not obliged to do so. If you do not wish
to do so, delete this exception statement from your version.
