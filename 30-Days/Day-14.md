Day 14 — STM32CubeIDE, Build, Flashing, and Debugging

Today I studied the complete STM32 development workflow using STM32CubeIDE. I learned how a C program written on the computer is transformed
into firmware that can run on the STM32F103. The process includes compilation, assembly, linking, flashing, and debugging.

I learned that the compiler translates C code into ARM machine instructions, while the linker combines the different object files and places
program sections into the correct memory regions according to the linker script. The final executable is usually generated as an ELF file,
which also contains debugging information.

I studied the main project files created by STM32CubeIDE. main.c contains the main application code, main.h contains declarations and 
definitions, stm32f1xx_it.c contains interrupt handlers, and the startup assembly file contains the vector table and Reset Handler. 
I also learned that the .ioc file stores the STM32CubeMX hardware configuration and that the Drivers folder contains HAL and CMSIS libraries.

I learned that HAL (Hardware Abstraction Layer) provides higher-level C functions for controlling STM32 peripherals, while the actual 
hardware is still controlled through memory-mapped registers. STM32CubeMX helps configure the microcontroller by generating initialization
code for clocks, GPIO, peripherals, and other hardware.

I also studied how firmware is transferred to the STM32. The compiled program is written into Flash using an ST-LINK programmer/debugger
through the SWD interface. Flashing stores the program permanently in the STM32 Flash memory so that it can run again after power is
removed and restored.

Finally, I learned the main debugging features of STM32CubeIDE, including breakpoints, Step Into, Step Over, Resume, register inspection,
variable inspection, peripheral register views, and memory inspection. I connected this with previous hardware topics by observing
registers such as the PC and SP, SRAM addresses around 0x20000000, Flash around 0x08000000, and hardware peripheral registers.

This helped me understand the complete path from C source code → compiler → linker → ELF firmware → ST-LINK/SWD → STM32 Flash
→ Cortex-M3 execution → debugging and hardware observation.
