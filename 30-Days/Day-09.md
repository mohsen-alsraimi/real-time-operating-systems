Day 9 — STM32 Clock, Reset, and Boot System
Today I studied the clock, reset, and boot systems of the STM32F103. I learned that the microcontroller requires a clock signal to 
synchronize the CPU and other hardware components. The STM32F103 can operate at up to 72 MHz, meaning the processor receives up to 
72 million clock cycles per second.
I learned about the main clock sources. HSI (High-Speed Internal) is an internal 8 MHz oscillator built into the microcontroller, 
while HSE (High-Speed External) uses an external clock source such as the crystal on the development board. The PLL 
(Phase-Locked Loop) can multiply the clock frequency; for example, an 8 MHz HSE clock multiplied by 9 can produce a 72 MHz system clock (SYSCLK).
I also studied the STM32 clock tree. SYSCLK passes through clock dividers and is distributed through the AHB, APB1, and APB2 buses. 
A common configuration uses 72 MHz for AHB, 36 MHz for APB1, and 72 MHz for APB2. Different peripherals are connected to these buses, 
so their operating clocks depend on the bus and clock configuration.
The RCC (Reset and Clock Control) is responsible for configuring clock sources, PLL settings, bus prescalers, peripheral clocks, 
and peripheral resets. I learned that many peripherals must first have their clock enabled through RCC before they can be configured 
and used.
I also studied the reset system. A reset returns the microcontroller to a defined starting state and can occur because of power-on, 
the external reset pin/button, software, or watchdog events. Resetting the microcontroller restarts execution but does not erase the 
program stored in Flash.
Finally, I learned about the boot process. Boot configuration determines whether the STM32 starts from the main Flash memory, system 
memory containing the built-in bootloader, or SRAM. During normal operation, the program boots from Flash. After reset, the processor 
obtains the initial stack pointer and Reset Handler from the vector table, executes startup code, initializes memory and the system, 
and eventually calls main().
This helped me understand the complete startup path from power → reset → clock → boot selection → vector table → Reset Handler → system initialization → main().
