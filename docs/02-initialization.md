# Processor Initialization

### Exception Levels

The ARM v8 architecture has 4 architectures. The exception level is a processor execution mode in which only a subset of operations and registers are available. 
So, from least privileged to most privileged exception level:

- **EL0**
        It only uses general purpose register (**__x0 - x30__**) and the stack pointer register (**__SP__**).
        This level also allows using **__STR__** and **__LDR__** to store and load data from memory.