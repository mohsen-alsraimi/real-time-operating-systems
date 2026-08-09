Day 12 — STM32 Peripherals and Data Movement

Today I studied the main hardware peripherals of the STM32F103 and how data moves between peripherals, memory, and the Cortex-M3 CPU.
I learned that peripherals are specialized hardware blocks that perform specific operations independently after being configured by 
the processor.

I studied hardware timers, which count clock events and can generate precise periodic events without requiring the CPU to continuously
count. Timers can be used for delays, periodic interrupts, frequency measurement, input capture, output compare, and PWM 
(Pulse Width Modulation). PWM generates repeating digital signals with adjustable duty cycles and can be used for applications such as controlling LED brightness and motors.

I learned about the ADC (Analog-to-Digital Converter), which converts analog voltage signals from sensors into digital numbers that 
the processor can understand. The STM32F103 provides 12-bit ADCs, giving up to 4096 possible digital levels for a conversion result.

I also studied the main communication peripherals. USART provides serial communication and can be used to exchange data with computers 
and other devices. SPI provides fast synchronous communication using clock and data lines and is commonly used with displays, sensors, 
and memory devices. I²C uses the SDA and SCL lines to allow multiple addressed devices to communicate over the same bus.

The most important concept was understanding the three main methods of handling peripheral data: polling, interrupts, and DMA. 
With polling, the CPU repeatedly checks the peripheral. With interrupts, the peripheral informs the CPU when an event requires 
attention. With DMA (Direct Memory Access), data can be transferred directly between peripherals and memory with much less CPU involvement.

I also learned that peripherals can operate concurrently with the processor. For example, while the CPU performs calculations, 
a timer can count, the ADC can perform conversions, DMA can transfer data to SRAM, and USART can transmit data. This hardware 
concurrency allows embedded systems to operate efficiently and prepares the foundation for later studying FreeRTOS and software 
multitasking.

A complete example I studied was: Timer → ADC → DMA → SRAM → Cortex-M3 → USART → Computer, where the CPU coordinates the system while 
specialized hardware performs much of the repetitive work.
