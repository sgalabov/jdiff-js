#
# Makefile
#
.DEFAULT: default

OBJS=JDebug.o JDiff.o JFileAhead.o JFileIStream.o JFileIStreamAhead.o JHashPos.o JMatchTable.o JOutAsc.o JOutBin.o JOutRgn.o main.o

default:	linux
all: 		linux
full:		clean linux
linux:		jdiff jptch
debug:		jdifd jptcd

CC=gcc
CPP=g++
CFLAGS=-Os -Wall
NATIVE=-march=native

debug:DBG=-g -D_DEBUG
linux:CFLAGS+=-D_FILE_OFFSET_BITS=64 -U_LARGEFILE64_SOURCE -m32 -Wno-literal-suffix -static

%.o: %.cpp
	$(CPP) $(CFLAGS) $(DBG) -o $@ -c $<

clean:
	rm -f jdiff jptch jdifd jptcd *.exe $(OBJS)

jdiff: $(OBJS)
	$(CPP) $(CFLAGS) $(DBG) $(OBJS) -o jdiff

jptch: jpatch.cpp
	$(CPP) $(CFLAGS) $(DBG) -o jptch jpatch.cpp

jdifd: $(OBJS)
	$(CPP) $(CFLAGS) $(DBG) $(OBJS) -o jdifd

jptcd: jpatch.cpp
	$(CPP) $(CFLAGS) $(DBG) -o jptcd jpatch.cpp

js:
	emcc -Wno-reserved-user-defined-literal JDebug.cpp JDiff.cpp JFileAhead.cpp JFileIStream.cpp JFileIStreamAhead.cpp JHashPos.cpp JMatchTable.cpp JOutAsc.cpp JOutBin.cpp JOutRgn.cpp main.cpp -Isrc/ -s NO_EXIT_RUNTIME=0 -s ALLOW_MEMORY_GROWTH=1 -l nodefs.js -o ../jdiff.js
