MODULE_HASH=fnv_32a
LIB_DIR=lib64
PREFIX=/usr/local

all: build

# Note: this file is not properly integrated with the configure script.
# A proper setup would have configure.ac and Makefile.ac
# and make use of the portable way to derive the -fPIC and
# other flags.

# CFLAGS=-g -O2
# CPPFLAGS=

# So we just set CFLAGS here, and you can override them
# when invoking make, for example
#  make "CFLAGS=-fPIC -g -c"


CFLAGS=-fPIC -O3 -c 

build:
	gcc $(CFLAGS) ${MODULE_HASH}.c
	gcc $(CFLAGS) ketama.c
	gcc $(CFLAGS) ketama_test.c
	gcc -shared -o libketama.so.1 ketama.o ${MODULE_HASH}.o
	gcc -o ketama_test ketama_test.o ketama.o ${MODULE_HASH}.o -lm

install:
	install -d $(PREFIX)/$(LIB_DIR) $(PREFIX)/include
	install libketama.so.1 $(PREFIX)/$(LIB_DIR)/
	install ketama.h $(PREFIX)/include/
	cd ${PREFIX}/$(LIB_DIR) && ln -sf libketama.so.1 libketama.so

clean:
	rm -f *.o
	rm -f libketama.so.1
	rm -f ketama_test
	rm -f build-stamp configure-stamp

uninstall:
	rm $(PREFIX)/$(LIB_DIR)/libketama.so.1
	rm $(PREFIX)/$(LIB_DIR)/libketama.so
	rm $(PREFIX)/include/ketama.h

deinstall: uninstall
