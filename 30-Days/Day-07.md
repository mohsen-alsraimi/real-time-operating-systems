Day 7 — ARM Cortex-M3 CPU Architecture

Today I studied the ARM Cortex-M3 CPU, which is the processor core used inside the STM32F103. I learned that the CPU is responsible for 
executing the program instructions stored in Flash memory and that instruction execution can be understood through the Fetch, Decode, 
and Execute cycle. The processor fetches an instruction from memory, decodes what operation is required, and then executes it.
I learned about the CPU's registers, which are small and very fast storage locations used while instructions are being executed. Registers 
R0–R12 are mainly general-purpose registers. R13 is the Stack Pointer (SP), which points to the current stack location. R14 is the Link 
Register (LR) and is important for returning from function calls. R15 is the Program Counter (PC) and is responsible for instruction-flow addressing.
I also studied the ALU (Arithmetic Logic Unit), which performs operations such as addition, subtraction, comparisons, shifts, and logical 
operations. The xPSR contains processor status information, including condition flags such as Zero, Negative, Carry, and Overflow.
Another important concept was ARM's load/store architecture. Data is normally loaded from memory into CPU registers, processed using the 
registers and ALU, and then stored back into memory when necessary. I also learned that Cortex-M3 uses the Thumb/Thumb-2 instruction 
architecture, with instructions such as MOV, ADD, SUB, LDR, STR, CMP, and branch instructions.
I studied how the processor uses pipelining to improve instruction throughput by overlapping stages of different instructions. I also 
learned about the two processor execution modes: Thread Mode for normal program execution and Handler Mode for handling exceptions and interrupts.
Finally, I learned that Cortex-M3 provides two stack pointers: the Main Stack Pointer (MSP) and Process Stack Pointer (PSP). These concepts 
are especially important for operating systems and FreeRTOS because multitasking requires managing the processor state, registers, stacks, 
and context of different tasks.
