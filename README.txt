This version of the code is optimized for x86_64 machine architectures. 
Some of the benchmarks run much better in machine architectures that natively
support Fetch&Add instructions(e.g., x86_64, etc.).
As a compiler, gcc is supported, but you may also try to use icc or clang.
The provided code is mostly developed and tested in x86_64 machine architectures 
(i.e., both Intel and Amd multiprocessors).
For compiling, it is highly recommended to use gcc of version 4.3.0 or greater. 
For getting the best performance, changes in Makefile may be needed (compiler flags etc).
Important parameters for the benchmarks and/or library are set in the config.h file..


COMPILING THE LIBRARY
=========================

In case that you just want to compile the library that provides all the implemented concurrent algorithms
execute one of the commands. This step is not necessary in case that you want to run benchmarks.

Make x86                 // Compiles the library/benchmarks for the x86 architecture using the gcc compiler. 

Make sparc               // Compiles the library/benchmarks for the SPARC architecture using the gcc compiler.
                         // The current version of the library/benchmarks are not tested  

Make icc                 // Compiles the library/benchmarks using the icc compiler. 

Make clang               // Compiles the library/benchmarks using the clang compiler.

Make clean               // Cleans all the binary files.


RUNNING BENCHMARKS
=========================
For running benchmarks use the bench.sh script file that is provided in the main directory of this source tree.
Example usage: ./bench.sh FILE.c OPTION1=NUM1  OPTION2=NUM2 ...

The following options are available:
    -t, --threads  set the number of threads (fiber threads also included, if any) to be used in the benchmark
    -f, --fibers   set the number of user-level threads per posix thread
    -c, --cores    set the number of cores to be used by the benchmark
    -b, --backoff  set a backoff value (only for simbench, simstack and simqueue benchmarks)
    -r, --repeat   set the number of times that the benchmark should be executed, default is 10 times
    -l, --list     displays the list of the available benchmarks
    -h, --help     display this help and exit

The current version of this library provides the following concurrent object implementations/benchmarks:

A) COMBINING TECHNIQUES
=========================
ccsynchbench.c           // A blocking Fetch&Multiply object based on the CC-Synch algorithm [1].
dsmsynchbench.c          // A blocking Fetch&Multiply object based on the DSM-Synch algorithm [1].
hsynchbench.c            // A blocking Fetch&Multiply object based on the H-Synch algorithm [1] suitable for Numa architectures.
simbench.c               // A wait-free Fetch&Multiply object based on the PSim algorithm [2].
oscibench.c              // A blocking Fetch&Multiply object based on the OSCI algorithm [3].
oyamabench.c             // A blocking Fetch&Multiply object based on the Oyama's algorithm [4].


B) CONCURRENT QUEUES
=========================
ccqueuebench.c           // A blocking concurrent queue implementation based on the CC-Synch algorithm [1].
dsmqueuebench.c          // A blocking concurrent queue implementation based on the DSM-Synch algorithm [1].
hqueuebench.c            // A blocking concurrent queue implementation based on the H-Synch algorithm [1] suitable for Numa architectures.
simqueuebench.c          // A wait-free concurrent queue implementation based on the SimQueue algorithm [2].
osciqueue.c              // A blocking concurrent queue implementation based on the OSCI algorithm [3].
clhqueuebench.c          // A blocking concurrent queue implementation based on CLH locks [5, 6].
msqueuebench.c           // A lock-free concurrent queue implementation based on the lock-free algorithm presented in [7].


C) CONCURRENT STACKS
=========================
ccstackbench.c           // A blocking concurrent stack implementation based on the CC-Synch algorithm [1].
dsmstackbench.c          // A blocking concurrent stack implementation based on the DSM-Synch algorithm [1].
hstackbench.c            // A blocking concurrent stack implementation based on the H-Synch algorithm [1] suitable for Numa architectures.
simstackbench.c          // A blocking concurrent stack implementation based on the SimStack algorithm [2].
oscistack.c              // A blocking concurrent stack implementation based on the OSCI algorithm [3].
lfstackbench.c           // A lock-free concurrent stack implementation based on the algorithm presented in [8].
clhstackbench.c          // A blocking concurrent stack implementation based on the CLH locks [5, 6].


D) LOCKS
=========================
clhbench.c               // A blocking Fetch&Multiply object based on the CLH locks [5, 6].


E) OTHER BENCHMARKS
=========================
lfuobjectbench.c         // A simple, lock-free Fetch&Multiply object implementation.
fadbench.c               // A benchmark that measures the throughput of Fetch&Add instructions on a multi-core machine.
activesetbench.c         // A simple implementation of an active-set.



REFERENCES
=========================
[1] Fatourou, Panagiota, and Nikolaos D. Kallimanis. "Revisiting the combining synchronization technique." 
    ACM SIGPLAN Notices. Vol. 47. No. 8. ACM, 2012.

[2] Fatourou, Panagiota, and Nikolaos D. Kallimanis. "A highly-efficient wait-free universal construction."
    Proceedings of the twenty-third annual ACM symposium on Parallelism in algorithms and architectures. ACM, 2011.

[3] Fatourou, Panagiota, and Nikolaos D. Kallimanis. "Lock Oscillation: Boosting the Performance of Concurrent Data Structures."
    Proceedings of the 21st International Conference on Principles of Distributed Systems. 2017.

[4] Oyama, Yoshihiro, Kenjiro Taura, and Akinori Yonezawa. "Executing parallel programs with synchronization bottlenecks efficiently."
    Proceedings of the International Workshop on Parallel and Distributed Computing for Symbolic and Irregular Applications. Vol. 16. 1999.

[5] T. S. Craig. Building FIFO and priority-queueing spin locks from atomic swap. 
    Technical Report TR 93-02-02, Department of Computer Science, University of Washington, February 1993

[6] Magnusson, Peter, Anders Landin, and Erik Hagersten. "Queue locks on cache coherent multiprocessors."
    Parallel Processing Symposium, 1994. Proceedings., Eighth International. IEEE, 1994
    
[7] Michael, Maged M., and Michael L. Scott. "Simple, fast, and practical non-blocking and blocking concurrent queue algorithms."
    Proceedings of the fifteenth annual ACM symposium on Principles of distributed computing. ACM, 1996.
    
[8] Treiber, R. Kent. "Systems programming: Coping with parallelism."
    International Business Machines Incorporated, Thomas J. Watson Research Center, 1986.


For any further information, please do not hesitate to
send an email at nkallima (at) ics.forth.gr. Feedback is always valuable.