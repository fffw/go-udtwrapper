C++ = g++

ifndef os
   os = LINUX
endif

ifndef arch
   arch = IA32
endif

CCFLAGS = -fPIC -Wall -Wextra -D$(os) -finline-functions -O3 -fno-strict-aliasing -fvisibility=hidden

ifeq ($(arch), IA32)
   CCFLAGS += -DIA32
endif

ifeq ($(arch), POWERPC)
   CCFLAGS += -mcpu=powerpc
endif

ifeq ($(arch), SPARC)
   CCFLAGS += -DSPARC
endif

ifeq ($(arch), IA64)
   CCFLAGS += -DIA64
endif

ifeq ($(arch), AMD64)
   CCFLAGS += -DAMD64
endif

OBJS = api_$(os)_$(arch).o buffer_$(os)_$(arch).o cache_$(os)_$(arch).o ccc_$(os)_$(arch).o channel_$(os)_$(arch).o common_$(os)_$(arch).o core_$(os)_$(arch).o epoll_$(os)_$(arch).o list_$(os)_$(arch).o md5_$(os)_$(arch).o packet_$(os)_$(arch).o queue_$(os)_$(arch).o window_$(os)_$(arch).o
DIR = $(shell pwd)

all: ../libudt_$(os)_$(arch).a

%_$(os)_$(arch).o: %.cpp %.h udt.h
	$(C++) $(CCFLAGS) -o $@ $< -c

libudt_$(os)_$(arch).a: $(OBJS)
	ar -rcs $@ $^

../libudt_$(os)_$(arch).a: libudt_$(os)_$(arch).a
	cp libudt_$(os)_$(arch).a ../

clean:
	rm -f *.o *.a ../libudt*.a

install:
	export LD_LIBRARY_PATH=$(DIR):$$LD_LIBRARY_PATH
