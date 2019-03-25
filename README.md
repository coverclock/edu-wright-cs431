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

# Update (from correspondance dated 2019-03-17)

My co-author, colleague, old friend David Hemmendinger made the following
remarks.

> When I asked Dayton Clark about his role, he wrote:
> 
> _I certainly am among those who loved CS 431.  I still think of it
> fondly.  I taught the course once, I believe, in '78 or '79.  But to
> the best of my memory I did not rewrite the Kernel.  That was a time
> when I was not afraid to any code I came across, but I don't recollect
> doing so with this code.  The only version I remember is Joe's version
> and I do not know where any copies are.
> 
> John's and your version looks beautiful and I'm glad to see that
> someone has archived it._
> 
> On your remark that adding even a single instruction could disrupt
> the handling of data from high-speed devices:  This is actually due
> to a design flaw.  Running a null process when nothing else is ready,
> and having it do steady context switches, meant that the system was
> uninterruptible nearly all the time, allowing interrupts only at the
> end of its spin loop.  Wirth's Modula-2 provided primitives with which
> one could write similar kernels, and its way of handling an empty
> queue of ready processes was to provide a "listen" function that
> was a tight loop, resetting priority to 0 and setting it back to
> uninterruptible.  It thereby allowed interrupts while the kernel was
> waiting for a process to become ready.
> 
> I realized this when I was using Modula-2 in the mid-1980s.  Having a
> null process may have made it easier for students to understand who was
> minding the store, albeit less efficient.  I also found it interesting
> that all three of the M-2 compilers that I used, which implemented
> similar kernels, had errors in their implementations, perhaps because
> compiler writers weren't familiar with concurrency.

This resulted in David and I discussing other implementations for the
null process that I had used in other projects like board support
packages and microcontroller task loops, in which I used a
processor-specific machine instruction to wait in an interruptable
state until an interrupt occured. I couldn't remember if the PDP-11
had such an instruction. David almost immediately replied.

> I just checked -- it did.  Even simpler than clearing and setting
> priority bits.  The largest 11s also had a set-priority-level
> instruction.
>
> The place to use it would be in the kernel routine that gets the next
> process to run:
>
    Next:   while empty(readyQ) do
                  wait
          cp := get(readyQ)

David, I miss you. It is always a pleasure working with you.
