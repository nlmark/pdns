
# Also see "include/polarssl/config.h"

CFLAGS	+= -I../include -D_FILE_OFFSET_BITS=64 -Wall -W -Wdeclaration-after-statement
OFLAGS	= -O

# MicroBlaze specific options:
# CFLAGS += -mno-xl-soft-mul -mxl-barrel-shift

# To compile on Plan9:
# CFLAGS += -D_BSD_EXTENSION

# To compile as a shared library:
CFLAGS += -fPIC

SONAME=libpolarssl.so.0

DLEXT=so
# OSX shared library extension:
# DLEXT=dylib

# Windows shared library extension:
# DLEXT=dll

OBJS=	aes.o		arc4.o		asn1parse.o		\
		base64.o	bignum.o	camellia.o		\
		certs.o		cipher.o	cipher_wrap.o	\
		ctr_drbg.o	debug.o		des.o			\
		dhm.o		entropy.o	entropy_poll.o	\
		error.o		havege.o					\
		md.o		md_wrap.o	md2.o			\
		md4.o		md5.o		net.o			\
		padlock.o	pem.o		pkcs11.o		\
		rsa.o		sha1.o		sha2.o			\
		sha4.o		ssl_cli.o	ssl_srv.o		\
		ssl_tls.o	timing.o	version.o		\
		x509parse.o	xtea.o
	
all: static

static: libpolarssl.a

shared: libpolarssl.$(DLEXT)

libpolarssl.a: $(OBJS)
	$(AR) r $@ $(OBJS)
	$(AR) s $@

libpolarssl.so: libpolarssl.a
	$(CC) ${LDFLAGS} -shared -Wl,-soname,$(SONAME) -o $@ $(OBJS)

libpolarssl.dylib: libpolarssl.a
	$(CC) ${LDFLAGS} -dynamiclib -o $@ $(OBJS)

libpolarssl.dll: libpolarssl.a 
	$(CC) -shared -Wl,-soname,$@ -o $@ $(OBJS) -lws2_32 -lwinmm -lgdi32 

.c.o:
	$(CC) $(CFLAGS) $(OFLAGS) -c $<

clean:
	rm -f *.o libpolarssl.*

