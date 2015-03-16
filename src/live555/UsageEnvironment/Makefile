INCLUDES = -Iinclude -I../groupsock/include
PREFIX = /usr/local
LIBDIR = $(PREFIX)/lib
##### Change the following for your environment:
# **Note: You must install the relevant "Command line tools (OSX *.*) for Xcode - Xcode *.*"
# for this configuration file to work.
#
# Change the following version number, if necessary, before running "genMakefiles iphoneos"
IOS_VERSION =		8.1

DEVELOPER_PATH =	/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer
TOOL_PATH =		$(DEVELOPER_PATH)/usr/bin
SDK_PATH =		$(DEVELOPER_PATH)/SDKs
SDK =	 		$(SDK_PATH)/iPhoneOS$(IOS_VERSION).sdk
COMPILE_OPTS =          $(INCLUDES) -I. $(EXTRA_LDFLAGS) -DBSD=1 -O2 -DSOCKLEN_T=socklen_t -DHAVE_SOCKADDR_LEN=1 -D_LARGEFILE_SOURCE=1 -D_FILE_OFFSET_BITS=64 -fPIC -arch armv7 --sysroot=$(SDK)
C =                     c
C_COMPILER =            /usr/bin/xcrun clang
C_FLAGS =               $(COMPILE_OPTS)
CPP =                   cpp
CPLUSPLUS_COMPILER =    /usr/bin/xcrun clang
CPLUSPLUS_FLAGS =       $(COMPILE_OPTS) -Wall
OBJ =                   o
LINK =                  /usr/bin/xcrun clang -o 
LINK_OPTS =             -v -L. -arch armv7 --sysroot=$(SDK) -L$(SDK)/usr/lib/system /usr/lib/libc++.dylib
CONSOLE_LINK_OPTS =     $(LINK_OPTS)
LIBRARY_LINK =          libtool -s -o 
LIBRARY_LINK_OPTS =
LIB_SUFFIX =            a
LIBS_FOR_CONSOLE_APPLICATION =
LIBS_FOR_GUI_APPLICATION =
EXE =			
##### End of variables to change

NAME = libUsageEnvironment
USAGE_ENVIRONMENT_LIB = $(NAME).$(LIB_SUFFIX)
ALL = $(USAGE_ENVIRONMENT_LIB)
all:	$(ALL)

OBJS = UsageEnvironment.$(OBJ) HashTable.$(OBJ) strDup.$(OBJ)

$(USAGE_ENVIRONMENT_LIB): $(OBJS)
	$(LIBRARY_LINK)$@ $(LIBRARY_LINK_OPTS) $(OBJS)

.$(C).$(OBJ):
	$(C_COMPILER) -c $(C_FLAGS) $<       

.$(CPP).$(OBJ):
	$(CPLUSPLUS_COMPILER) -c $(CPLUSPLUS_FLAGS) $<

UsageEnvironment.$(CPP):	include/UsageEnvironment.hh
include/UsageEnvironment.hh:	include/UsageEnvironment_version.hh include/Boolean.hh include/strDup.hh
HashTable.$(CPP):		include/HashTable.hh
include/HashTable.hh:		include/Boolean.hh
strDup.$(CPP):			include/strDup.hh

clean:
	-rm -rf *.$(OBJ) $(ALL) core *.core *~ include/*~

install: install1 $(INSTALL2)
install1: $(USAGE_ENVIRONMENT_LIB)
	  install -d $(DESTDIR)$(PREFIX)/include/UsageEnvironment $(DESTDIR)$(LIBDIR)
	  install -m 644 include/*.hh $(DESTDIR)$(PREFIX)/include/UsageEnvironment
	  install -m 644 $(USAGE_ENVIRONMENT_LIB) $(DESTDIR)$(LIBDIR)
install_shared_libraries: $(USAGE_ENVIRONMENT_LIB)
	  ln -s $(NAME).$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)/$(NAME).$(SHORT_LIB_SUFFIX)
	  ln -s $(NAME).$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)/$(NAME).so

##### Any additional, platform-specific rules come here:
