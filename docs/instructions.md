# Instructions of ARMv8 architecture

**LDR** 
	
Load data from an address into a register
		
`LDR X0, <addr>` *Load from addr into register X0*
	
---
**STR**

Store data from a register into a address

`STR X0, <addr>` *Store contents from X0 to addr*

---
**SVC**

Causes an exception. The processor mode changes to Supervisor, the `CPSR`(*Current Program Status Register*) is saved to the Supervisor mode `SPSR`(*Save Program Status Register*), and finally the execution branches (*jumps*) to the SVC vector.

`SVC imm16`

---
