# OS161_CodeReading01
OS/161 Code Reading, Traps, Interrupts, System Calls, and Debugging Practice

**Questions**:

1. Traps and interrupts are mechanisms used to transfer control between user processes and the operating system. Tell us where we can find the first line of OS/161 code that is executed when a trap occurs. Then tell us where control gets transferred to from that point (i.e., what function services the trap). Be sure to describe the control flow for each type of trap that may occur (e.g., system calls, VM faults, and hardware interrupts).

> Answer: 

>The given data above have kern, archs, locore, mips and exception-mips.S has a code handling codes. There is an exception to >that, for example, the code has UTLB exception and therefore, the first code will be 69. in case of a general exception, the >first line will be 87. Both lines of the code, 69 and 87 have one thing is common as that are simple j common_exception. 
>A typeframe is usually created by common_exception which is passed to mips_trap found in kern/arch/,mips/locore/trap.c. which >from is then: 
>syscalls will be sent directly to syscall function in kern/arch/mips/syscall.c.
>VM faults will go directly or will be directed to vm_fault, which by now is kern/arch/mips/vm/dumbvm.c.
>Interrupts are usually directed to mainbus_interrupt which is kern/arch/sys161/dev/lamebus_machdep.c. There are interprocessor >interrupts that are taken to interprocessor_interrupt that is in the kern/thread/clock.c. Usually, the interrupts are mainly >handled outside arch directory. 
>Panic occurs when there is an invalid TLB entries or any other error. 



2. Where is the first line of code for constructing a trapframe? Describe at a high level what the code is doing here.

> Answer: 

>A trapefram is composed a code. It is kern/arch/sys161/conf/conf.arch. The code is usually more relatable to that of >mips/conf/conf.arch.
>We count 37 uint32_ts inside of the kern/arch/mips/include/trapeframe.h. Each of it is around 4 bytes, a total of 148 bytes. >This is the size of the trapframe because it is required to store around 37 registers such as general purpose, cause and EPC >registers. 




3. Each OS/161 exception has its own code. What are the exception codes for the exceptions: **interrupt**, **system call**, and **arithmetic overflow**?

> Answer: 
> 1. interrupt has Zero exception code
> 2. system call has 8 exception code
> 3. arithmetic overflow has 12 exception code

system call: src/kern/startup/main.c.
Interrupt: public InterruptedException()


4. What information is saved in **struct trapframe**?

> Answer: 

>Context is usually the set information that allows you to continue with the execution ofdf a task exactly where you left or >stopped at.  The trapframe struct contains uint edi that is the register for the string operations.  it has esi, which is the >string operations source index and ebx that base index. Hence the trapframe struct contains context and registers. 
> 



5. What is the name of the function that is the system-call handler in OS/161? In which directory is this function implementation located?

> Answer: 
>
>The name of the system call handler in the OS/161 is known as handler syscall.c 
>It is usually located in this folder os161/src/kern/arch/mips/mips




6. The kernel's main function is to provide support for user-level programs. Most such support is accessed via "system calls”. For example, consider the system call **reboot()**, which is implemented in the function **sys_reboot()** in *src/kern/main/main.c*. Using GDB, put a breakpoint on **sys_reboot** and run the "reboot" program (by typing "p /sbin/reboot" at the OS/161 menu prompt). Use "backtrace" to see how it got there. **Show the output of your debugging session as well as the output printed by the OS/161.**



> Answer: 
>
> of the system calls is usually accompanied with a unique identifier number, in OS/161 these system call are usually numbers >that are defined within in kern/include/kern/syscall.h:
>#define sys_reboot
>The library associated with the reboot() usually places the syscall reg. number in register (v0) and in turn issues trap to >the OS. Assembly language exceptions sends to syscall handler the data structure called trapframe which contains, among some >other information and the system number. 
>The system call number is usually used in a switch case statement to select the function 
>void syscall(struct trapframe *tf)
...
>switch (callno) {
>case sys_reboot:
>err = sys_reboot(tf->tf_a0);
>break;

> 
