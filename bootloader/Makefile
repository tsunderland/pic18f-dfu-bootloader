###########################################################
# BEGIN CONFIGURATION
###########################################################

MCU=18f25k50

CC=sdcc
AS=gpasm
LD=gplink
SC=srec_cat

OUTPUT=bootloader

###########################################################
# END CONFIGURATION
###########################################################


OFLAGS=--use-non-free --optimize-cmp --optimize-df --denable-peeps --opt-code-size
CFLAGS=-S -mpic16 -p$(MCU) -Wall -I/usr/share/sdcc/include/pic16 -I. $(OFLAGS)
ASFLAGS=
LDFLAGS=-I/usr/share/sdcc/lib/pic16 -w -r -m -s $(MCU).lkr

CSRCS=vector.c main.c usb/usb.c usb/usb_descriptors.c usb/ep0.c dfu/dfu.c flash.c

ASMSRCS = $(CSRCS:.c=.asm)
OBJS = $(ASMSRCS:.asm=.o)

all: $(OUTPUT)_code.bin $(OUTPUT)_config.bin

$(OUTPUT)_code.bin: $(OUTPUT).hex
	$(SC) $(OUTPUT).hex -intel -crop 0x0 0x7FFF -o $(OUTPUT)_code.bin -binary

$(OUTPUT)_config.bin: $(OUTPUT).hex
	$(SC) $(OUTPUT).hex -intel -crop 0x300000 0x30000D -offset -0x300000 -o $(OUTPUT)_config.bin -binary

$(OUTPUT).hex: $(ASMSRCS) $(OBJS)
	$(LD) $(LDFLAGS) -o $(OUTPUT) $(OBJS) crt0i.o pic$(MCU).lib libsdcc.lib libio$(MCU).lib libc18f.lib

clean:
	rm -f *.o
	rm -f *.asm
	rm -f *.lst
	rm -f *.cod
	rm -f *.hex
	rm -f *.map
	rm -f *.bin
	rm -f usb/*.o
	rm -f usb/*.asm
	rm -f usb/*.lst
	rm -f dfu/*.o
	rm -f dfu/*.asm
	rm -f dfu/*.lst

%.asm : %.c
	$(CC) $(CFLAGS) $< -o $@

%.o : %.asm
	$(AS) $(ASFLAGS) -o $@ -c $<

