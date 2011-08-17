CROSS=arm-none-eabi-
CC=$(CROSS)gcc
OBJCOPY=$(CROSS)objcopy
LD=$(CROSS)ld
AS=$(CROSS)as
STRIP=$(CROSS)strip

STM_LIB=../stm/FWLib/inc

CFLAGS = -Wall -Os -I. -Iinc  -Werror -fno-common -mcpu=cortex-m3 -mthumb -msoft-float -MD -I $(STM_LIB)
AFLAGS = -mcpu=cortex-m3   
LDFLAGS = -mcpu=cortex-m3 -lc -lnosys -mthumb -march=armv7 -mfix-cortex-m3-ldrd -msoft-float -lstm32 -nostartfiles 

OBJS = Calibrat.o Draw.o Files.o Function.o Ident.o Interrupt.o Main.o Menu.o Process.o BIOS.o startup.o
TARGETS = app1.hex app2.hex app3.hex

all: $(OBJS) $(TARGETS)

.PHONY: clean

clean:
	rm -rf $(OBJS) $(TARGETS)

.c.o:
	$(CC) $(CFLAGS) -c -o $@ $*.c

.S.o:
	$(CC) $(AFLAGS) -c -o $@ $*.S

%.elf: %.lds $(OBJS)
	$(CC) -o $@ $(OBJS) $(LDFLAGS) -T $<

%.bin: %.elf
	$(OBJCOPY) -O binary $< $@

%.hex: %.elf
	$(OBJCOPY) -O ihex $< $@
