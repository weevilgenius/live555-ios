INCLUDES = -I../UsageEnvironment/include -I../groupsock/include -I../liveMedia/include -I../BasicUsageEnvironment/include
# Default library filename suffixes for each library that we link with.  The "config.*" file might redefine these later.
libliveMedia_LIB_SUFFIX = $(LIB_SUFFIX)
libBasicUsageEnvironment_LIB_SUFFIX = $(LIB_SUFFIX)
libUsageEnvironment_LIB_SUFFIX = $(LIB_SUFFIX)
libgroupsock_LIB_SUFFIX = $(LIB_SUFFIX)
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

MEDIA_SERVER = live555MediaServer$(EXE)

PREFIX = /usr/local
ALL = $(MEDIA_SERVER)
all: $(ALL)

.$(C).$(OBJ):
	$(C_COMPILER) -c $(C_FLAGS) $<
.$(CPP).$(OBJ):
	$(CPLUSPLUS_COMPILER) -c $(CPLUSPLUS_FLAGS) $<

MEDIA_SERVER_OBJS = live555MediaServer.$(OBJ) DynamicRTSPServer.$(OBJ)

live555MediaServer.$(CPP):	DynamicRTSPServer.hh version.hh
DynamicRTSPServer.$(CPP):	DynamicRTSPServer.hh

USAGE_ENVIRONMENT_DIR = ../UsageEnvironment
USAGE_ENVIRONMENT_LIB = $(USAGE_ENVIRONMENT_DIR)/libUsageEnvironment.$(libUsageEnvironment_LIB_SUFFIX)
BASIC_USAGE_ENVIRONMENT_DIR = ../BasicUsageEnvironment
BASIC_USAGE_ENVIRONMENT_LIB = $(BASIC_USAGE_ENVIRONMENT_DIR)/libBasicUsageEnvironment.$(libBasicUsageEnvironment_LIB_SUFFIX)
LIVEMEDIA_DIR = ../liveMedia
LIVEMEDIA_LIB = $(LIVEMEDIA_DIR)/libliveMedia.$(libliveMedia_LIB_SUFFIX)
GROUPSOCK_DIR = ../groupsock
GROUPSOCK_LIB = $(GROUPSOCK_DIR)/libgroupsock.$(libgroupsock_LIB_SUFFIX)
LOCAL_LIBS =	$(LIVEMEDIA_LIB) $(GROUPSOCK_LIB) \
		$(BASIC_USAGE_ENVIRONMENT_LIB) $(USAGE_ENVIRONMENT_LIB)
LIBS =			$(LOCAL_LIBS) $(LIBS_FOR_CONSOLE_APPLICATION)

live555MediaServer$(EXE):	$(MEDIA_SERVER_OBJS) $(LOCAL_LIBS)
	$(LINK)$@ $(CONSOLE_LINK_OPTS) $(MEDIA_SERVER_OBJS) $(LIBS)

clean:
	-rm -rf *.$(OBJ) $(ALL) core *.core *~ include/*~

install: $(MEDIA_SERVER)
	  install -d $(DESTDIR)$(PREFIX)/bin
	  install -m 755 $(MEDIA_SERVER) $(DESTDIR)$(PREFIX)/bin

##### Any additional, platform-specific rules come here:
