edu-wright-cs431
================

This is a simple kernel that provides a rudimentary standalone
multiprogramming environment upon which a real-time operating system
may be built. Kernel services include process synchronization through
counting semaphores, inter-process communication through asynchronous
queued message passing, and dynamic process creation and destruction.

The evolution of the kernel began long long ago when Professors Robert
Dixon and Joseph Kohler of the Computer Science Department at Wright
State University first developed the Real-Time Software Design course
(CEG431/631) around 1967. This kernel's design owes much to a later
version implemented by Dayton Clark around 1980. Finally, the present
version was cleaned up, enhanced, and documented by David Hemmendinger
and John Sloan in 1982.  The kernel has been in production for several
years, and has found its way into a variety of undergraduate and
graduate courses; it has been ported to several different processors;
it has been embedded in other research systems such as SLICK (Simple
Lsi-11 Interprocessor Communication Kernel) and TASK4TH (a real-time
multitasking FORTH interpreter).

The kernel uses the EMulator Trap machine instruction. The EMT instruction
cannot be used for any other purpose. If the use of EMT is inappropriate,
the symbol KSR can be changed to use the TRAP instruction. No other
machine instruction can be used.

WARNING! The kernel service routines must run in an uninterruptable
state. The code that implements these routines must be as short
and as efficient as possible if real-time applications are to run
successfully. For example, the addition of even a single instruction
to the EMT decoding in the Kernel Service Request Handler can result
in timing errors on high speed devices such as communication lines and
card readers.

Only two processes are specifically created by the kernel: the
initialization process (INI.PR) and the null process (NU.PR).  NU.PR is
always in the ready state so that the READY queue is never devoid of
something to run. It is defined inside the kernel module itself, even
though it is not conceptually a part of the kernel itself. INI.PR has
the responsibility of creating all other processes in the system. It
must be defined by the user, and its entry point must be labelled with
the global symbol INI.PR. Typically, INI.PR can self-destruct via the
EOP kernel service call when initialization is complete.

The kernel is in the public domain provided credit is acknowledged to
the Computer Science Department of Wright State University. No warranty
is expressed or implied by the authors, the department, the University,
or indeed anyone else.

The algorithms presented in pseudo-C code should be considered guidelines
or aids to assist in understanding the corresponding assembler code. In
most cases, the analogy is only approximate.
