Day 13 — Complete STM32 Hardware System

Today I completed my study of the main STM32F103 hardware architecture and learned how the different components studied during the 
previous days work together as one complete embedded system.

I studied the power architecture, including VDD and VSS for the main digital circuitry, VDDA and VSSA for analog circuitry, and 
VBAT for the backup domain. I learned that the backup domain can allow components such as the RTC (Real-Time Clock) to continue 
operating when the main system power is unavailable.

I also learned about the IWDG and WWDG watchdog timers, which improve system reliability. The software periodically refreshes the 
watchdog while operating correctly. If the program freezes or fails to refresh it within the required time, the watchdog can reset 
the microcontroller automatically.

I studied the STM32 debugging hardware, particularly SWD (Serial Wire Debug) and JTAG. Using an ST-LINK debugger through SWD allows 
firmware to be programmed into Flash and makes it possible to pause execution, use breakpoints, execute code step by step, and inspect 
CPU registers, memory, variables, and peripheral registers.

I also learned about additional communication hardware such as USB and CAN. USB allows the STM32 to communicate with USB hosts through 
its USB peripheral. CAN is designed for reliable communication between multiple embedded devices and is widely used in automotive and 
industrial systems. I learned that using a physical CAN bus normally requires an external CAN transceiver in addition to the STM32's CAN controller.

Finally, I connected everything studied during Days 6–13 into one complete system. The Cortex-M3 CPU executes instructions from Flash, 
SRAM stores runtime data and stacks, RCC provides and controls clocks, AHB/APB buses connect hardware blocks, peripherals perform 
specialized operations, DMA transfers data, and NVIC manages interrupts. GPIO and communication peripherals then connect the internal system to the physical world.

I can now understand the STM32 as an interconnected hardware system rather than simply a CPU. A complete operation can involve 
power → clock → CPU → buses → peripheral registers → peripheral hardware → physical pins, while interrupts, DMA, memory, watchdogs, 
and debugging hardware operate alongside it. This completed my eight-day study of the main STM32 hardware architecture and prepared me to begin practical STM32 programming.
