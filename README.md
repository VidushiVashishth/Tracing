# Tracing

This repository consists of parts of the tracing framework which will gradually enable generation of Common Trace Format trace output
for RTEMS applications. The test suitcase is the fileio sample which comes along with the RTEMS installation. 

## Pre-requisites:

- Install rtems 5 for sparc/erc32 architecture-bsp pair. The RTEMS repository with modifications for enabling CTF Tracing is https://github.com/VidushiVashishth/rtems

- Download the fileio INI file in this repository and save it on the top of the installed BSP (erc32) directory

- Change the values of `rtems-path` and `prefix` in the fileio INI file according to your installation.

The general Tracing process consists of the following steps:

1) Generation of RTEMS trace.
2) Transportation of the generated trace to the host machine.
3) Conversion of transported traces to CTF using babeltrace scripts.
4) Viewing the converted output (CTF).

## 1) Generation of RTEMS traces:

This step occurs on the RTEMS target (simulator).

### Alternatives:

There are two ways of generating RTEMS trace: Using printk generators or using trace buffering. The output of the printk generators is trace dumped on console. Whereas trace buffering can both be stored in the form of binary files or printed on console. The following are instructions to generate trace using trace buffering for the fileio sample testcase. This testcase is a part of the rtems installation. 

Copy the `Trace_Sample_fileio` directory on the top of the installed bsp directory. Change the values of the keys `prefix` and `rtems-path` of the filieo-trace.ini file according to your rtems installation. Also make alterations to the value of `LIBPATH` in the `Makefile` according to your installation. The B option in `LIBPATH` denotes the usage of full path to the lib folder. Run `make` and `make run` commands to execute trace enabled fileio executable. Use `rtrace -l` to see the available options of commands provided with `rtrace`. Use `rtrace stop` followed by `rtrace trace` to see the trace output on the console. Note that this example runs a precompiled sample test case. Any change to the code of the test case will require regeneration of the object and executable files.  

### Tools used:

RTEMS trace linker is used in this step to generate traces for applications. 

## 2) Transportation of the generated Trace to the host:

### Alternatives:

This step transfers the RTEMS generated trace output from the target (simulator) to the development host machine. This could be done using a number of alternatives:
 
1) Using socket programming. The client would be running on the target (simulator) and server on the host machine.

2) Creating a transportation API.

3) (quick fix) : Parsing the console trace output on the host machine.

## 3) Conversion of Transported Trace into CTF using babletrace scripts:

### Tools used:

This step executes on the host machine. The transported RTEMS format trace is converted to CTF using babeltrace scripts. 

### Lessons learnt:
RTEMS trace format can be saved in the form of binary files or printed on console. To convert the RTEMS trace from its binary format to CTF we would need to create a customised babeltrace plugin.  

## 4) Viewing the final output:

### Tools used:

The final output can be viewed using various tools like Trace Compass.

