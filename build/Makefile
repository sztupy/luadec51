# makefile for installing Lua and Luadec
# see ../lua/Makefile, ../lua/src/Makefile and ../lua/src/luaconf.h for further
# customization

# == CHANGE THE SETTINGS BELOW TO SUIT YOUR ENVIRONMENT =======================

# Your platform. See PLATS for possible values.
PLAT= none

# Where to install. The installation starts in the src and doc directories,
# so take care if INSTALL_TOP is not an absolute path.
INSTALL_TOP= /usr/local
INSTALL_BIN= $(INSTALL_TOP)/bin
#

# How to install. If your install program does not support "-p", then you
# may have to run ranlib on the installed liblua.a (do "make ranlib").
INSTALL= install -p
INSTALL_EXEC= $(INSTALL) -m 0755
INSTALL_DATA= $(INSTALL) -m 0644
#
# If you don't have install you can use cp instead.
# INSTALL= cp -p
# INSTALL_EXEC= $(INSTALL)
# INSTALL_DATA= $(INSTALL)

# Utilities.
MKDIR= mkdir -p
CC= gcc
CFLAGS= -I../lua/src -O2 -Wall $(MYCFLAGS)
RM= rm -f
LIBS= -L../lua/src -lm -llua $(MYLIBS)

MYCFLAGS=
MYLDFLAGS=
MYLIBS=

# == END OF USER SETTINGS. NO NEED TO CHANGE ANYTHING BELOW THIS LINE =========

# Convenience platforms targets.
PLATS= aix ansi bsd freebsd generic linux macosx mingw posix solaris

# What to install.
TO_BIN= luadec

LUADEC_T= luadec
LUADEC_O= luadec.o StringBuffer.o guess.o ldprint.o output.o proto.o structs.o

default: $(PLAT)

all:	$(LUADEC_T)

luadec.o: ../luadec/luadec.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h
StringBuffer.o: ../luadec/StringBuffer.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h
ldprint.o: ../luadec/ldprint.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h
output.o: ../luadec/output.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h
proto.o: ../luadec/proto.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h
structs.o: ../luadec/structs.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h
guess.o: ../luadec/guess.c ../luadec/StringBuffer.h ../luadec/structs.h ../luadec/output.h ../luadec/proto.h ../luadec/print.h

o:	$(LUADEC_O)

$(LUADEC_T): $(LUADEC_O)
	$(CC) -o $@ $(MYLDFLAGS) $(LUADEC_O) $(LIBS)

$(LUADEC_O):
	$(CC) -c $(CPPFLAGS) $(CFLAGS) -o $@ ../luadec/$<

clean:
	cd ../lua && $(MAKE) $@
	$(RM) $(LUADEC_T) $(LUADEC_O)

install: dummy
	$(MKDIR) $(INSTALL_BIN)
	$(INSTALL_EXEC) $(TO_BIN) $(INSTALL_BIN)

aix:
	cd ../lua && $(MAKE) $@
	$(MAKE) all CC="xlc" CFLAGS="-O2 -DLUA_USE_POSIX -DLUA_USE_DLOPEN" MYLIBS="-ldl" MYLDFLAGS="-brtl -bexpall"

ansi:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS=-DLUA_ANSI

bsd:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS="-DLUA_USE_POSIX -DLUA_USE_DLOPEN" MYLIBS="-Wl,-E"

freebsd:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS="-DLUA_USE_LINUX" MYLIBS="-Wl,-E -lreadline"

generic:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS=

linux:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS=-DLUA_USE_LINUX MYLIBS="-Wl,-E -ldl -lreadline -lhistory -lncurses"

macosx:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS=-DLUA_USE_LINUX MYLIBS="-lreadline"
# use this on Mac OS X 10.3-
#	$(MAKE) all MYCFLAGS=-DLUA_USE_MACOSX

mingw:
	cd ../lua && $(MAKE) $@
	$(MAKE) "LUA_A=lua51.dll" "LUA_T=lua.exe" \
	"AR=$(CC) -shared -o" "RANLIB=strip --strip-unneeded" \
	"MYCFLAGS=-DLUA_BUILD_AS_DLL" "MYLIBS=" "MYLDFLAGS=-s" lua.exe
	$(MAKE) "LUAC_T=luac.exe" luac.exe

posix:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS=-DLUA_USE_POSIX

solaris:
	cd ../lua && $(MAKE) $@
	$(MAKE) all MYCFLAGS="-DLUA_USE_POSIX -DLUA_USE_DLOPEN" MYLIBS="-ldl"

none:
	@echo "Please do"
	@echo "   make PLATFORM"
	@echo "where PLATFORM is one of these:"
	@echo "   $(PLATS)"
	@echo "See INSTALL for complete instructions."

# make may get confused with test/ and INSTALL in a case-insensitive OS
dummy:

# list targets that do not create files (but not all makes understand .PHONY)
.PHONY: all $(PLATS) clean install o none local

# (end of Makefile)
