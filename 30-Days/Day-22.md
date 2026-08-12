Day 22 — I²C Communication

Today I studied I²C (Inter-Integrated Circuit) communication and learned how the STM32F103 can communicate with external devices such as sensors, EEPROMs, real-time clocks, and displays using only two main communication lines: SDA (Serial Data) and SCL (Serial Clock).

I learned that I²C is a synchronous, addressed communication bus. Unlike UART, which normally uses separate TX and RX lines, I²C uses SDA for bidirectional data and SCL for the clock. Multiple devices can share the same SDA and SCL lines because each target device normally has its own address.

I studied 7-bit I²C addressing and the additional read/write bit used during communication. The controller first sends the address of the device it wants to communicate with and specifies whether it wants to read or write. I also learned that STM32 HAL functions commonly expect a 7-bit device address shifted left by one bit, for example 0x68 << 1.

I learned how an I²C transaction is organized using START, address, R/W, ACK/NACK, data, and STOP conditions. A START condition indicates the beginning of communication, while STOP indicates its end. ACK confirms that a byte was received, while NACK indicates that it was not acknowledged or can be used by the controller to indicate the end of a read operation. I also studied the Repeated START, which is commonly used when reading registers from sensors.

I studied how many I²C devices contain internal registers. The STM32 can first specify which register it wants and then read or write its contents. I learned how HAL_I2C_Master_Transmit() and HAL_I2C_Master_Receive() perform basic transfers, while HAL_I2C_Mem_Read() and HAL_I2C_Mem_Write() are useful for accessing registers inside sensors and similar devices.

I also learned about the electrical design of I²C. SDA and SCL normally use open-drain outputs, meaning devices actively pull the lines LOW but normally do not actively drive them HIGH. Pull-up resistors return the lines to HIGH when no device is pulling them LOW. This design allows multiple devices to safely share the same communication bus.

I studied common I²C speeds such as 100 kHz Standard Mode and 400 kHz Fast Mode, and learned that pull-up resistance and bus capacitance affect the signal rise time and therefore the reliability and maximum practical communication speed.

I configured I2C1 in STM32CubeMX and studied how pins such as PB6 and PB7 can be connected to the I2C1 peripheral through the GPIO alternate-function system. I also learned how an I²C scanner can test different addresses using HAL_I2C_IsDeviceReady() to discover which devices are connected to the bus.

I studied important STM32 I²C registers including CR1, CR2, DR, SR1, SR2, CCR, and TRISE. These registers control the peripheral, communication timing, START/STOP generation, data transmission and reception, status flags, and other I²C operations.

Finally, I connected I²C with concepts from previous days. I²C can operate using polling, interrupts, or DMA. A complete sensor system can therefore work as: external sensor → SDA/SCL → STM32 I²C peripheral → CPU/DMA → SRAM → application → UART → computer.

The main concept I learned is that a simple function such as HAL_I2C_Mem_Read() represents a much larger hardware process underneath: HAL → I²C registers → peripheral state machine → GPIO alternate functions → SDA/SCL signals → START → device address → ACK → register/data transfer → STOP.
