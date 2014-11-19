# USIMM: the Utah SImulated Memory Module
## Version 1.3

------------------------------------------------------------------------------
USIMM is distributed under the CRAPL (see CRAPL-LICENSE.txt
in this directory).  In spite of the tongue-in-cheek terms of
the license, we will be supporting the USIMM infrastructure.  
The src/utlist.h file was obtained from http://uthash.sourceforge.net
and is subject to the terms of the BSD license.
For questions to the USIMM developers, email usimm@cs.utah.edu 
For updates or discussions, email usimm-users@cs.utah.edu,
or visit this blog post: http://utaharch.blogspot.com/2012/02/usimm.html

USIMM was developed by members of the Utah Arch group:
Niladrish Chatterjee, Rajeev Balasubramonian, Manjunath Shevgoor,
Seth H. Pugsley, Aniruddha N. Udipi, Ali Shafiee, Kshitij Sudan, Manu Awasthi.

We also received traces and suggestions from other JWAC MSC organizers:
Zeshan Chishti (Intel), Alaa R. Alameldeen (Intel), Eric Rotenberg (NC State)

* Code download: http://www.cs.utah.edu/~rajeev/usimm-v1.3.tar.gz
* USIMM Tech Report: http://www.cs.utah.edu/~rajeev/pubs/usimm.pdf
* The JWAC MSC website: http://www.cs.utah.edu/~rajeev/jwac12/

------------------------------------------------------------------------------


# GETTING STARTED
------------------------------------------------------------------------------

If you've reached this far, you've already been able to unzip and
untar the distribution with:
gunzip usimm-v1.3.tar.gz
tar xvf usimm-v1.3.tar

The root directory has the following directories and files:
* src/      : Code source files
* bin/      : Houses the usimm executable
* obj/      : Houses the intermediate object files for the source files
* input/    : Has the (simulated) system configuration files and input traces
* output/   : Store the simulation outputs
* runsim    : A script to execute a few example simulations
* README.md: this file!
* usimm.pdf : The USIMM tech report
* parse.perl: This is for parsing the simulation result into `stats.csv`.
* CRAPL-LICENSE.txt: The CRAPL license.

## Fast development build
1. Modify the file __./runsim__ to suit your needs
2. Make an output directory by `mkdir output`
3. `cd src/` Enter source diectory
4. Run `make execute` to build, execute, and parse

## Build the sources
1. `cd src/` The src directory.
2. `make clean`
3. `make` Build binaries.

This produces a usimm executable in the bin/ directory.  To run the 
example simulation script.

4. Go to repository root directory by `cd ../`
5. Download input from .... It's your bussiness!
6. Modify __./runsim__ to suit your needs.
7. Run executable `./runsim` to check whether the environment is set correctly.
8. Execute `ps` to check whether it's running in the background.

If you want to know how to add your new scheduler algorithm, it's very easy!! 
All you need to do is __name your .c file__ by __scheduler-XXXX.c__ `XXXX` is 
your algorithm's name. Makefile will automatically compile it! 

The simulation should finish in tens of minutes.  Use a truncated version of
the trace files for shorter tests.  To examine the simulation outputs,
view output/*

The input/ directory contains the system and DRAM chip configuration
files that are read by USIMM.  Do not rename this directory or
the DRAM chip configuration files.  The input/ directory also
contains 13 trace files for 10 different benchmarks.  Please see
Appendix C of the USIMM Tech report for details on these benchmarks.

# CODE ORGANIZATION
------------------------------------------------------------------------------
More detail at http://www.cs.utah.edu/%7Erajeev/jwac12/

The src/ directory has the following files:

main.c : Handles the main program loop that retires instructions,
fetches new instructions from the input traces, and calls update_memory().

memory_controller.c : Implements update_memory(), a function that checks
DRAM timing parameters to determine which commands can issue in this cycle.

scheduler.c : Function provided by the user to select a command for each
channel in every memory cycle.  The provided default is a simple FCFS 
algorithm with periodic write drains.

scheduler.h : Header file for the user's scheduler function.

configfile.h : Header file to enable reading input system config files.

memory_controller.h : Header file to enable DRAM timing management.

params.h : Header file for all system parameters.

processor.h : Header file for the ROB structure that controls the processor.

utils.h : A few utility functions.

utlist.h : Utility functions to manage linked lists.


# SAMPLE SCHEDULERS
------------------------------------------------------------------------------

The src/ directory also includes the following example simple schedulers:

scheduler-fcfs.c/h    : Basic FCFS, plus a periodic write drain mechanism.

scheduler-close.c/h   : Precharges banks during idle cycles soon after a column rd/wr.


If you want to know how to add your new scheduler algorithm, it's very easy!! 
All you need to do is __name your .c file__ by __scheduler-XXXX.c__ `XXXX` is 
your algorithm's name. Makefile will automatically compile it! 

