INCLUDES = -I../include/

#CROSS_COMPILE := /usr/eldk/usr/bin/mips_4KC-
#CC			  := $(CROSS_COMPILE)gcc
#CFLAGS		  := -O -G 0 -mno-abicalls -fno-builtin -Wa,-xgot -Wall -fPIC
#LD			  := $(CROSS_COMPILE)ld
# For embedding one program in another

USERLIB := printf.o \
		print.o \
		libos.o \
		fork.o \
		pgfault.o \
		syscall_lib.o \
		ipc.o \
		string.o \
		fd.o \
		pageref.o \
		file.o \
		pipe.o \
		fsipc.o \
		console.o \
		fprintf.o

CFLAGS += -nostdlib -static

#all: idle.x $(USERLIB) entry.o syscall_wrap.o

#%.x: %.b.c
#	echo cc1 $<
#	$(CC) $(CFLAGS) -c -o $@ $<

#%.b.c: %.b
#	echo create $@
#	echo bintoc $* $< > $@~
#	chmod +x ./bintoc
#	./bintoc $* $< > $@~ && mv -f $@~ $@
##	grep \. $@
	
#%.b: entry.o syscall_wrap.o %.o $(USERLIB)
#	echo ld $@
#	$(LD) -o $@ $(LDFLAGS) -G 0 -static -n -nostdlib -T ./user.lds $^

all: idle.bin fktest.bin pingpong.bin

%.bin: %.elf
	$(LD) -r -b binary -o $@ $<

%.elf: syscall_wrap.o entry.o %.o $(USERLIB)
	$(LD) -o $@ -e _start -T user.lds -G 0 -static -n -nostdlib $^

%.o: %.c
	echo user1 cc $<
	$(CC) $(CFLAGS) $(INCLUDES) -c -o $@ $<

%.o: %.S
	echo as $<
	$(CC) $(CFLAGS) $(INCLUDES) -c -o $@ $<

%.o: lib.h

.PHONY: clean

clean:
	rm -rf *~ *.o *.b.c *.x *.b *.bin
	echo nizaiyanwo


include ../include.mk
