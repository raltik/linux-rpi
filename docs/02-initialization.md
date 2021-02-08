# Processor Initialization

## Exception Levels

The ARM v8 architecture has 4 exception levels. The exception level is a processor execution mode in which only a subset of operations and registers are available. 

![Exception Levels](/docs/images/exception-levels.png)

So, from least privileged to most privileged exception level:

- **EL0**
	
	It only uses general purpose register (**x0 - x30**) and the stack pointer register (**SP**).
	This level also allows using [`STR`](/docs/instructions.md) and [`LDR`](/docs/instructions.md) to store and load data from memory.
	
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

---
## Switching to EL1

In this section, we will see the system registers which set and controls all the exception levels of the processor.

- **SCTLR_EL1** (System Control Register)

	Provides top level control of the system, including its memory system, at `EL1` and `EL0`.
	This register is mapped to AArch32 System Register in booth architectures(32 or 64).

	First of all, the field bits that are marked as reserved (*RES1*) needs to be initialized with `1`, in the 	***ARMv8.0*** architecture those fields are the bits 29, 28, 23, 22, 20 and 11.
	
	In addition, we'll disable all the caches of the processor (instruction and data cache) and the memory 		management unit.
	
	So, we need to initialize the following fields:
		
	1. **EE**, bit 25
		
		Defines the endianess of explicit data acces at EL1. So, the processor is configured to work only with little-endian format.
	
	2. **E0E**, bit 24
	
		Defines the endianess of explicit data acces at EL0.
		
	3. **I**, bit 12
	
		Controls the instruction cache. We will disable this cache, i.e. '0'.
		
	4. **C**, bit 2
		
		Controls the data cache. We'll disable this cache too.
	
	5. **M**, bit 0
		
		Controls the MMU (*Memory Management Unit*) for EL1 and EL0.
		
		
			




