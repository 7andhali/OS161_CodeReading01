# OS161_CodeReading01
OS/161 Code Reading, Traps, Interrupts, System Calls, and Debugging Practice

**Questions**:

1. Traps and interrupts are mechanisms used to transfer control between user processes and the operating system. Tell us where we can find the first line of OS/161 code that is executed when a trap occurs. Then tell us where control gets transferred to from that point (i.e., what function services the trap). Be sure to describe the control flow for each type of trap that may occur (e.g., system calls, VM faults, and hardware interrupts).

> Answer: 
>  we can find the first line of OS/161 on the directory: kern/arch/mips/locore/exeption-mips1.S
> line 87 for general exception
> line 69 for UTLB exeption

> 1. Syscalls directed to syscall function and it occurs on kern/arch/mips/syscall.c
> 2. VM faults directed to vm_fault function and it occurs on kern/arch/mips/vm/dumbvm.c
> 3. for the hardware interrupts:
>   a. interrupts directed to mainbus_interrupts and it occures on kern/arch/sys161/dev/lambus_machdep.c
>   b  timer interrupts directed to hardclock and it ocuures to kern/thread/clock.c
>   c. general interrups directed to lamebus_interrup and it occures on kern/dev/lamebus.c
>   d. interprocessor interrupts directed to interprocessor_interrup and it occures on kern/thread/thread.c



2. Where is the first line of code for constructing a trapframe? Describe at a high level what the code is doing here.

> Answer: 
> The first line of code for constructing a trapframe is  kern/arch/mips/mips/
>
> The processor invokes this line " kern/arch/mips/mips/ " when the exceptions occurs to call into the operationg system and   >constract a trap frame.  



3. Each OS/161 exception has its own code. What are the exception codes for the exceptions: **interrupt**, **system call**, and **arithmetic overflow**?

> Answer: 
> 1. interrupt has Zero exception code
> 2. system call has 8 exception code
> 3. arithmetic overflow has 12 exception code


4. What information is saved in **struct trapframe**?

> Answer: 
>
> 



5. What is the name of the function that is the system-call handler in OS/161? In which directory is this function implementation located?

> Answer: 
>
> 



6. The kernel's main function is to provide support for user-level programs. Most such support is accessed via "system calls”. For example, consider the system call **reboot()**, which is implemented in the function **sys_reboot()** in *src/kern/main/main.c*. Using GDB, put a breakpoint on **sys_reboot** and run the "reboot" program (by typing "p /sbin/reboot" at the OS/161 menu prompt). Use "backtrace" to see how it got there. **Show the output of your debugging session as well as the output printed by the OS/161.**



> Answer: 
>
> 
