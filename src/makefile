IDIR=../include
CC=avr-gcc
MMCU=avr128da28
FCPU=24000000UL

PROGRAM_NAME=program

ODIR=obj

AVR_PACK_PATH=/home/cantrell/programming/avr/packs/avr_dx

LDIR=$(AVR_PACK_PATH)/include/
BDIR=$(AVR_PACK_PATH)/gcc/dev/$(MMCU)/

CFLAGS=-mmcu=$(MMCU) -B$(BDIR) -I$(LDIR) -I$(IDIR) -DF_CPU=$(FCPU) -Os

#LIBS=-lm -lasound

_DEPS =
DEPS = $(patsubst %,$(IDIR)/%,$(_DEPS))

_OBJ = main.o
OBJ = $(patsubst %,$(ODIR)/%,$(_OBJ))


$(ODIR)/%.o: %.c $(DEPS)
	@mkdir -p $(@D)
	$(CC) -c -o $@ $< $(CFLAGS)

$(PROGRAM_NAME): $(OBJ)
	$(CC) -o $@.elf $^ $(CFLAGS) $(LIBS)


.PHONY: clean bin all

clean:
	rm -f $(ODIR)/*.o *~ core $(IDIR)/*~ 

bin:
	make
	avr-objcopy -O binary $(PROGRAM_NAME).elf $(PROGRAM_NAME).bin

hex:
	make
	avr-objcopy -O ihex $(PROGRAM_NAME).elf $(PROGRAM_NAME).hex

all:
	make 
	make bin
	make hex