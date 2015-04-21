DFU bootloader for PIC18F
=========================

Note
----
THIS SOFTWARE COMES WITHOUT ANY WARRANTY!
This code is based on a forked repository from krumboeck/pic18f-dfu-bootloader. Any mistakes are mine, and will be resolved as time permits. 

License
-------
LGPL v2.1 (DFU part use MIT)

Requirements
------------
* PIC18f25k50 (it may work on other MCU with little code changes)
* PICkit2 or any other Programmer
* SDCC
* GNU PIC Utilities (gputils)
* SRecord
* dfu-utils or any other DFU Software
* Python

Bootloader Configuration
------------------------
* Edit bootloader/config.h
* Edit bootloader/Makefile
* Edit bootloader/fuses.h
* Edit bootloader/usb/usb_descriptors.c

How to build
------------
* Type 'make' on project root directory

Install bootloader with PICkit2
-------------------------------
pk2cmd -PPIC18F25k50 -M -Fbootloader.hex -R

Flash application with dfu-utils
--------------------------------
dfu-util -D example.dfu

What works
----------
* Nothing at the moment! Work in progress...please check back later. 


ToDo
----
* Download application
* Upload
* Interrupts
* Leave bootloader and jump to application
* Fix various bugs
