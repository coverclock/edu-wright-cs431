edu-wright-cs431
================

This is a simple kernel for the PDP-11 written in MACRO-11 assembly
language. It provides a rudimentary standalone multiprogramming
environment upon which a real-time operating system may be built. Kernel
services include process synchronization through counting semaphores,
inter-process communication through asynchronous queued message passing,
and dynamic process creation and destruction.

The evolution of the kernel began long long ago when Professors Robert
Dixon and Joseph Kohler of the Computer Science Department at Wright
State University first developed the CS431/631 "Advanced Programming"
course sometime (probably) in the 1970s and based on (perhaps) the IBM
1130. This kernel's design owes much to a later version for the PDP-11
implemented by Dayton Clark around 1980. Finally, the present version
was cleaned up, enhanced, and documented by David Hemmendinger and
John Sloan in 1982, by which time the course had morphed into CEG431/631
"Real-Time Software Design" as part of the more hardware-oriented Computer
Engineering program.

The kernel has been in production for several years, and has found its
way into a variety of undergraduate and graduate courses; it has been
ported to several different processors; it has been embedded in other
research systems such as SLICK (Simple LSI-11 Interprocessor Communication
Kernel), TASK4TH (a real-time multitasking FORTH interpreter), and FPS
(Functional Programming System). Rumor has it that it found its way into
other PDP-11-based real-time systems implemented by former students
working in the commercial and defense realms, and was even ported to
early microprocessor systems.

The kernel is in the public domain provided credit is acknowledged to
the Computer Science Department of Wright State University. No warranty
is expressed or implied by the authors, the department, the University,
or indeed anyone else.

The algorithms presented in pseudo-C code should be considered guidelines
or aids to assist in understanding the corresponding assembler code. In
most cases, the analogy is only approximate.
