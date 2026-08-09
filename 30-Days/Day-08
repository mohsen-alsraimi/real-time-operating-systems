Day 8 — STM32 Memory System

Today I studied the memory system of the STM32F103 and learned how the CPU uses different memory regions to store programs, data, and 
hardware registers. The Cortex-M3 has a 32-bit address space, which provides addresses from 0x00000000 to 0xFFFFFFFF. This does not mean 
the STM32 has 4 GB of physical memory; instead, different ranges of this address space are assigned to Flash, SRAM, peripherals, and processor system components.
I learned that Flash memory stores the program instructions and keeps them even when power is removed. The STM32 Flash is normally mapped 
starting at 0x08000000. SRAM, starting at 0x20000000, is volatile working memory used for variables, buffers, the stack, heap, and other 
runtime data.
I also learned how a C program is organized in memory. The .text section mainly contains executable instructions, .data contains 
initialized global/static variables, and .bss contains uninitialized global/static variables. During startup, initialized data is copied 
into SRAM and the .bss section is cleared to zero.
The stack is an area of SRAM used for function calls, local data, saved registers, and interrupt context. It is controlled using the 
Stack Pointer studied on Day 7. The heap is another memory area that can be used for dynamic memory allocation. Understanding the stack 
is especially important for FreeRTOS because each task normally requires its own stack.
An important concept I learned was memory-mapped I/O. STM32 peripherals such as GPIO, timers, ADC, and USART contain hardware registers 
that are assigned addresses in the memory map. The peripheral region begins at 0x40000000. When the CPU reads or writes these addresses, 
it is actually reading or controlling physical hardware. This explains how C pointers and register operations can directly control STM32
peripherals.

Finally, I studied the vector table, which contains the initial stack information and addresses of exception and interrupt handlers. After 
reset, the processor obtains its initial state from the vector table, executes startup code, initializes memory, and eventually reaches main().

This helped me understand the complete connection between
C code → machine instructions → CPU → memory addresses → hardware registers → physical hardware.
