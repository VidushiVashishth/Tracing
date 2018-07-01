# Tracing

This repository consists of parts of the tracing framework which will gradually enable generation of Common Trace Format trace output
for RTEMS applications. The test suitcase is the fileio sample which comes along with the RTEMS installation. 

#Pre-requisites:

- Install rtems 5 for sparc/erc32 architecture-bsp pair. The rtems file that I have made changes to is `main_rtrace.c` which lies in
rtems/cpukit/libmisc/shell/ directory. It is a part of this repository too with the same name (main_rtrace.c). 

- Download the fileio INI file in this repository and save it on the top of the installed BSP (erc32) directory

- Change the values of `rtems-path` and `prefix` in the fileio INI file according to your installation.

#Instructions on how to run tracing:

After installing rtems and the application INI (fileio) file, `cd` to the top of the installed BSP directory and run the following
commands.

1) configure command:

`$HOME/development/rtems/kernel/rtems/configure --prefix=$HOME/development/rtems/5 --target=sparc-rtems5 --enable-rtemsbsp=erc32 --enable-posix`

2) application link commands:

`sparc-rtems5-gcc -B/home/vidushi/development/rtems/5/sparc-rtems5/erc32/lib/ \
-specs bsp_specs -qrtems -mcpu=cypress -O2 -g -ffunction-sections -fdata-sections \
-Wall -Wmissing-prototypes -Wimplicit-function-declaration -Wstrict-prototypes \
-Wnested-externs -Wl,--gc-sections -mcpu=cypress -o sparc-rtems5/c/erc32/testsuites/samples/fileio.exe \
sparc-rtems5/c/erc32/testsuites/samples/fileio/fileio-init.o`

The -B option indicates the full path to the respective file. Make changes to the path values of the fileio.exe, fileio-init.o and 
the lib directory according to your installation

`rtems-tld -C fileio-trace.ini -W fileio-wrapper -- -B/home/vidushi/development/rtems/5/sparc-rtems5/erc32/lib/ \
-specs bsp_specs -qrtems -mcpu=cypress -O2 -g -ffunction-sections -fdata-sections -Wall -Wmissing-prototypes \
-Wimplicit-function-declaration -Wstrict-prototypes -Wnested-externs -Wl,--gc-sections -mcpu=cypress -o \
sparc-rtems5/c/erc32/testsuites/samples/fileio.exe sparc-rtems5/c/erc32/testsuites/samples/fileio/fileio-init.o`

3) run the application:

`sparc-rtems5-run sparc-rtems5/c/erc32/testsuites/samples/fileio.exe`

quickly hit `s`, `root` and `pwd` as soon as you enter the command. Use `rtrace -l` option to list the available options with rtrace.

enter `rtrace stop`, `rtrace ctftrace <filename>` to save ctf traces inside `filename` provided by you. 
