Day 21 — Direct Memory Access (DMA)

Today I studied DMA (Direct Memory Access) and learned how the STM32F103 can move data between peripherals and memory with much less CPU involvement.

I learned that without DMA, the CPU often has to read data from a peripheral and then store it manually in SRAM. With DMA, the CPU mainly configures the transfer, while the DMA hardware moves the data directly. This allows the CPU to continue performing other operations at the same time.

I studied the main DMA transfer types: Peripheral-to-Memory, Memory-to-Peripheral, and Memory-to-Memory. For the ADC example, the transfer direction is Peripheral-to-Memory because ADC results are moved from the ADC data register into an SRAM buffer.

I learned how DMA uses channels and how peripherals are mapped to specific DMA channels. For example, ADC1 on the STM32F103 commonly uses DMA1 Channel 1. I also studied the main DMA configuration settings: source address, destination address, number of transfers, data width, transfer direction, priority, and whether memory or peripheral addresses should increment.

For ADC transfers, the peripheral address remains fixed because every conversion result comes from the same ADC data register, while the memory address increments so each new result is stored in the next element of the buffer. Since the ADC result is 12-bit, a uint16_t buffer is suitable for storing the samples.

I studied the difference between Normal mode and Circular mode. In Normal mode, DMA stops after the requested number of transfers is completed. In Circular mode, DMA automatically returns to the beginning of the buffer and continues transferring data, which is useful for continuous sensor sampling.

I also learned about half-transfer and transfer-complete events. These events allow the CPU to process part of a buffer while DMA continues filling another part, creating an efficient continuous data-processing system.

I configured ADC with DMA and studied the use of HAL_ADC_Start_DMA() to transfer ADC measurements directly into an SRAM buffer. I also learned how DMA can later be used with peripherals such as UART and SPI for larger data transfers.

I studied important DMA registers including CCR, CNDTR, CPAR, CMAR, ISR, and IFCR. CPAR stores the peripheral address, CMAR stores the memory address, CNDTR tracks the remaining number of transfers, and CCR controls settings such as direction, circular mode, address increment, data width, priority, and interrupts.

The main architecture I learned was: ADC → DMA → SRAM buffer, while the CPU performs other work. This showed me how DMA reduces CPU overhead and how peripherals, memory, interrupts, and the CPU can work together efficiently in a real embedded system.
