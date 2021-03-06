# Makefile for libusb based examples
BTSTACK_ROOT = ../..
POSIX_ROOT= ${BTSTACK_ROOT}/platforms/posix

CORE += main.c stdin_support.c

COMMON += hci_transport_h2_libusb.c run_loop_posix.c remote_device_db_fs.c


include ${BTSTACK_ROOT}/example/embedded/Makefile.inc
# CC = gcc-fsf-4.9
CFLAGS  += -g -Wall 
# CFLAGS += -Werror

VPATH += ${BTSTACK_ROOT}/platforms/posix/src

ifeq ($(OS),Windows_NT)
LDFLAGS += -lws2_32
# assume libusb was installed into /usr/local
CFLAGS  += -I/usr/local/include/libusb-1.0
LDFLAGS += -L/usr/local/lib -lusb-1.0
else
# use pkg-config
CFLAGS  += $(shell pkg-config libusb-1.0 --cflags)
LDFLAGS += $(shell pkg-config libusb-1.0 --libs)
endif

# Command Line examples require porting to win32, so only build on other unix-ish hosts
ifneq ($(OS),Windows_NT)
EXAMPLES += ${EXAMPLES_CLI}
CFLAGS += -I${POSIX_ROOT}/src
endif

EXAMPLES += sam3u_benchmark

all: ${BTSTACK_ROOT}/include/btstack/version.h ${EXAMPLES}
