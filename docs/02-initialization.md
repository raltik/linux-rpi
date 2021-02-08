# Processor Initialization

## Exception Levels

The ARM v8 architecture has 4 exception levels. The exception level is a processor execution mode in which only a subset of operations and registers are available. 

![Exception Levels](/docs/images/exception-levels.png)

So, from least privileged to most privileged exception level:

- **EL0**
	
	It only uses general purpose register (**x0 - x30**) and the stack pointer register (**SP**).
	This level also allows using `STR` and `LDR` to store and load data from memory.
	
	The user process of the OS, uses this level because the user process should **NOT** be able to access other process's data.
	So, in this level, a process can only use it's own virtual memory.
        
- **EL1**
	
	The operating system itself, i.e. Linux, usually works at this level. 
	
	This exception level processor gets access to the registers that allows configuring virtual memory settings and some system registers.
	
- **EL2**
	
	It is used when we are using a hypervisor. In this case, host operating system runs at **EL2** and the guests operating systems only can use **EL1**.
	
	This allows host OS to isolate guest OSes like how OS isolates user processes.

- **EL3**

	Finally, this exception level is used for transitions from ARM `Secure world` to `Insecure world`. This level provides full hardware isolation between the software running in two different "worlds". [Security in ARMv8](https://developer.arm.com/documentation/100935/0100/)
