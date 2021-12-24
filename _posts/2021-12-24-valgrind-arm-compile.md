---
layout: post
title: "Run valgrind in ARM Hardware"
date: 2021-12-24
tags: performance development c++
---

## Cross compile valgrind for ARMv7

### Debian stretch:

  * Install build essentials and cross-compiling tools (gnueabihf for ARMv7)
  
``` bash
root@host:~# apt install libc6-armel-cross libc6-dev-armel-cross
root@host:~# apt install binutils-arm-linux-gnueabi
root@host:~# apt install libncurses5-dev
root@host:~# apt install gcc-arm-linux-gnueabihf
root@host:~# apt install g++-arm-linux-gnueabihf
```

* Download last valgrind version from http://valgrind.org/downloads/:

``` bash
user@host:~/Downloads/$ tar xvf valgrind-3.13.0.tar.bz2
```

### Valgrind compilation:
 
* Create configure file:

``` bash
user@host:~/Downloads/valgrind-3.13.0$ CC=arm-linux-gnueabihf-gcc-6 ./configure --host=armv7-unknown-linux-gnueabihf --target=arm-none-linux-gnueabihf --prefix=$HOME/valgrind CFLAGS='-Wl,-rpath=/lib/'
```

* Build and install:

``` bash
 user@host:~/Downloads/valgrind-3.13.0$ make
 user@host:~/Downloads/valgrind-3.13.0$ make install
```

* Copy the generated valgrind folder and all its contents:

``` bash
user@host:~/$ tar cvf valgrind.tar valgrind/
```

### Installation on device:

* Valgrind demands that ld-2.19-2014.04.so library contains debug symbols (see Stop compilation from removing symbols from critical shared libraries topic below)

* Copy the valgrind tarball to the home directory

``` bash
# tar xvf valgrind.tar
```

* Set the VALGRIND_LIB environment variable:

``` bash
# export VALGRIND_LIB=/data/root/valgrind/lib/valgrind
```

* Run valgrind:

``` bash
# /data/root/valgrind/bin/valgrind ./program_to_be_tested
```

* If the program is a daemon (without a debug mode), change the init line to run valgrind at start:

For example funcmng is initialized in inittab (sdk/rootfs/etc/inittab):

``` bash
ttyS0::respawn:/usr/bin/funcmng
```

changes to:

``` bash
ttyS0::respawn:/usr/bin/env VALGRIND_LIB=/data/root/valgrind/lib/valgrind /data/root/valgrind/bin/valgrind --log-file=/data/root/debug_file.log --trace-children=yes /usr/bin/funcmng
```

The option --trace-children=yes can be removed if there is no interest in checking the children of the process.
The output will be written in debug_file.log. If the daemon/program is not shutdown, the memory leak report will not be generated. If the service cannot be shutdown (like funcmng) one workaround is to shutdown the system with:

``` bash
# kill -TERM 1
```

Then shut it down and switch to emergencyOS via PartnerJET

Flash the device with a version of inittab without valgrind (otherwise it will overwrite the log) and restart it to get the log.
