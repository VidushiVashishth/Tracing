# This is a make file for generating traces in the sample application.
# The application object file and executable are pre compiled. Any change in the
# application would require regeneration of the .exe and .o files

LIBPATH = B/home/vidushi/development/rtems/5/sparc-rtems5/erc32/lib/

filio.exe: fileio-init.o
	rtems-tld -C fileio-trace.ini -W fileio-wrapper -- -$(LIBPATH) -specs bsp_specs -qrtems -mcpu=cypress -O2 -g -ffunction-sections -fdata-sections -Wall -Wmissing-prototypes -Wimplicit-function-declaration -Wstrict-prototypes -Wnested-externs -Wl,--gc-sections -mcpu=cypress -o fileio.exe fileio/fileio-init.o


fileio-init.o:
	sparc-rtems5-gcc -$(LIBPATH) -specs bsp_specs -qrtems -mcpu=cypress -O2 -g -ffunction-sections -fdata-sections -Wall -Wmissing-prototypes -Wimplicit-function-declaration -Wstrict-prototypes -Wnested-externs -Wl,--gc-sections -mcpu=cypress -o fileio.exe fileio/fileio-init.o

run:
	sparc-rtems5-run fileio.exe 


