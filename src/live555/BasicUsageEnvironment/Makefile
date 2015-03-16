INCLUDES = -Iinclude -I../UsageEnvironment/include -I../groupsock/include
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

NAME = libBasicUsageEnvironment
LIB = $(NAME).$(LIB_SUFFIX)
ALL = $(LIB)
all:	$(ALL)

OBJS = BasicUsageEnvironment0.$(OBJ) BasicUsageEnvironment.$(OBJ) \
	BasicTaskScheduler0.$(OBJ) BasicTaskScheduler.$(OBJ) \
	DelayQueue.$(OBJ) BasicHashTable.$(OBJ)

libBasicUsageEnvironment.$(LIB_SUFFIX): $(OBJS)
	$(LIBRARY_LINK)$@ $(LIBRARY_LINK_OPTS) \
		$(OBJS)

.$(C).$(OBJ):
	$(C_COMPILER) -c $(C_FLAGS) $<       

.$(CPP).$(OBJ):
	$(CPLUSPLUS_COMPILER) -c $(CPLUSPLUS_FLAGS) $<

BasicUsageEnvironment0.$(CPP):	include/BasicUsageEnvironment0.hh
include/BasicUsageEnvironment0.hh:	include/BasicUsageEnvironment_version.hh include/DelayQueue.hh
BasicUsageEnvironment.$(CPP):	include/BasicUsageEnvironment.hh
include/BasicUsageEnvironment.hh:	include/BasicUsageEnvironment0.hh
BasicTaskScheduler0.$(CPP):	include/BasicUsageEnvironment0.hh include/HandlerSet.hh
BasicTaskScheduler.$(CPP):	include/BasicUsageEnvironment.hh include/HandlerSet.hh
DelayQueue.$(CPP):		include/DelayQueue.hh
BasicHashTable.$(CPP):		include/BasicHashTable.hh

clean:
	-rm -rf *.$(OBJ) $(ALL) core *.core *~ include/*~

install: install1 $(INSTALL2)
install1: libBasicUsageEnvironment.$(LIB_SUFFIX)
	  install -d $(DESTDIR)$(PREFIX)/include/BasicUsageEnvironment $(DESTDIR)$(LIBDIR)
	  install -m 644 include/*.hh $(DESTDIR)$(PREFIX)/include/BasicUsageEnvironment
	  install -m 644 libBasicUsageEnvironment.$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)
install_shared_libraries: libBasicUsageEnvironment.$(LIB_SUFFIX)
	  ln -s $(NAME).$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)/$(NAME).$(SHORT_LIB_SUFFIX)
	  ln -s $(NAME).$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)/$(NAME).so

##### Any additional, platform-specific rules come here:
