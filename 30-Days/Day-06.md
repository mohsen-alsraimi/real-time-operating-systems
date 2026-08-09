Today I studied the overall hardware architecture of the STM32F103 microcontroller. I learned that the STM32 is not only a processor,
but a complete microcontroller containing a CPU, memory, communication interfaces, timers, and other hardware peripherals integrated into a single chip.
The main processor inside the STM32F103 is the 32-bit ARM Cortex-M3 CPU. It is responsible for executing the instructions stored in the 
Flash memory. Flash memory keeps the program even when the microcontroller is powered off, while SRAM is used as temporary memory for variables, buffers, the stack, and other data while the program is running.
I learned that GPIO provides the connection between the microcontroller and external hardware such as LEDs, buttons, and sensors. The 
STM32 also contains hardware timers for counting, timing operations, generating PWM signals, and producing periodic events. The ADC converts analog voltage signals from sensors into digital values that the processor can work with.
I also studied the main communication peripherals. USART can be used for serial communication, while SPI and I²C allow the STM32 to 
communicate with sensors, displays, memory chips, and other devices. The STM32F103 also provides interfaces such as USB and CAN.
The different components communicate through internal AHB and APB buses, which act as communication paths between the CPU, memory, and 
peripherals. I also learned about the RCC, which manages and distributes clock signals throughout the microcontroller, and the NVIC, which manages hardware interrupts and their priorities.
Finally, I learned about DMA (Direct Memory Access), which allows data to be transferred between peripherals and memory without requiring 
the CPU to manually move every piece of data. This showed me that many hardware components inside the STM32 can perform work independently after being configured by the CPU.
Overall, I learned how the CPU, Flash, SRAM, buses, GPIO, timers, ADC, communication peripherals, RCC, NVIC, and DMA form one connected 
hardware system inside the STM32F103.
